---
id: File Upload Attacks
aliases: []
tags: []
---

## Client-Side Validation

[[Front-end]] Validation it could be done in javascript and in html
## Whitelisting Extensions

## Blacklisting Extensions

https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/web-extensions.txt

## Content-Type
https://github.com/danielmiessler/SecLists/blob/master/Miscellaneous/Web/content-type.txt

## MIME-Type

MIME-Type. Multipurpose Internet Mail Extensions (MIME) is an internet standard that determines the type of a file through its general format and bytes structure.
This is usually done by inspecting the first few bytes of the file's content, which contain the [File Signature](https://en.wikipedia.org/wiki/List_of_file_signatures) or [Magic Bytes](https://opensource.apple.com/source/file/file-23/file/magic/magic.mime).

## Limited File Uploads

While file upload forms with weak filters can be exploited to upload arbitrary files, some upload forms have secure filters that may not be exploitable with the techniques we discussed. However, even if we are dealing with a limited (i.e., non-arbitrary) file upload form, which only allows us to upload specific file types, we may still be able to perform some attacks on the web application.

SVG, HTML, XML, and even some image and document files, may allow us to introduce new vulnerabilities to the web application by uploading malicious versions of these files. This is why fuzzing allowed file extensions is an important exercise for any file upload attack. It enables us to explore what attacks may be achievable on the web server.

### [[XSS]]

Many file types may allow us to introduce a Stored XSS vulnerability to the web application by uploading maliciously crafted versions of them.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="1" height="1">
    <rect x="1" y="1" width="1" height="1" fill="green" stroke="black" />
    <script type="text/javascript">alert(window.origin);</script>
</svg>
```

### XXE

Similar attacks can be carried to lead to XXE exploitation. With SVG images, we can also include malicious XML data to leak the source code of the web application, and other internal documents within the server. The following example can be used for an SVG image that leaks the content of (/etc/passwd):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<svg>&xxe;</svg>
```
this allows us to read the source code of the program like this

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg [ <!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=index.php"> ]>
<svg>&xxe;</svg>
```
 
Once the SVG image is displayed, we should get the base64 encoded content of index.php, which we can decode to read the source code.

Using XML data is not unique to SVG images, as it is also utilized by many types of documents, like PDF, Word Documents, PowerPoint Documents, among many others. All of these documents include XML data within them to specify their format and structure. Suppose a web application used a document viewer that is vulnerable to XXE and allowed uploading any of these documents. In that case, we may also modify their XML data to include the malicious XXE elements, and we would be able to carry a blind XXE attack on the back-end web server.

Another similar attack that is also achievable through these file types is an SSRF attack. We may utilize the XXE vulnerability to enumerate the internally available services or even call private APIs to perform private actions.


### [[DoS]]

Finally, many file upload vulnerabilities may lead to a Denial of Service (DOS) attack on the web server. For example, we can use the previous XXE payloads to achieve DoS attacks, as discussed in the Web Attacks module.

Furthermore, we can utilize a Decompression Bomb with file types that use data compression, like ZIP archives. If a web application automatically unzips a ZIP archive, it is possible to upload a malicious archive containing nested ZIP archives within it, which can eventually lead to many Petabytes of data, resulting in a crash on the back-end server.

Another possible DoS attack is a Pixel Flood attack with some image files that utilize image compression, like JPG or PNG. We can create any JPG image file with any image size (e.g. 500x500), and then manually modify its compression data to say it has a size of (0xffff x 0xffff), which results in an image with a perceived size of 4 Gigapixels. When the web application attempts to display the image, it will attempt to allocate all of its memory to this image, resulting in a crash on the back-end server.

In addition to these attacks, we may try a few other methods to cause a DoS on the back-end server. One way is uploading an overly large file, as some upload forms may not limit the upload file size or check for it before uploading it, which may fill up the server's hard drive and cause it to crash or slow down considerably.

If the upload function is vulnerable to directory traversal, we may also attempt uploading files to a different directory (e.g. ../../../etc/passwd), which may also cause the server to crash. Try to search for other examples of DOS attacks through a vulnerable file upload functionality.

## [[Injections]] in File Name

A common file upload attack uses a malicious string for the uploaded file name, which may get executed or processed if the uploaded file name is displayed (i.e., reflected) on the page. We can try injecting a command in the file name, and if the web application uses the file name within an OS command, it may lead to a [[Command injection]] attack.

For example, if we name a file file$(whoami).jpg or file`whoami`.jpg or file.jpg||whoami, and then the web application attempts to move the uploaded file with an OS command (e.g. mv file /tmp), then our file name would inject the whoami command, which would get executed, leading to remote code execution. You may refer to the Command Injections module for more information.

Similarly, we may use an XSS payload in the file name (e.g. <script>alert(window.origin);</script>), which would get executed on the target's machine if the file name is displayed to them. We may also inject an SQL query in the file name (e.g. file';select+sleep(5);--.jpg), which may lead to an SQL injection if the file name is insecurely used in an SQL query.
