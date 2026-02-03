## **Target Information**

- **Hostname**: puppy.htb
- **IP Address**: 10.129.246.71   10.10.11.70
- Creds: levi.james / KingofAkron2025!
## **Initial Nmap Scan**

- **Command**: `sudo nmap --top-ports=3000 -Pn -n 10.129.246.71 --reason`
- **Scan Date**: 2025-05-21
- **Result Summary**:    - Host is up (0.11s latency
    - 2985 filtered ports
    - 15 open ports:
        - 53/tcp - domain
        - 88/tcp - kerberos-sec
        - 111/tcp - rpcbind
        - 135/tcp - msrpc
        - 139/tcp - netbios-ssn
        - 389/tcp - ldap
        - 445/tcp - microsoft-ds
        - 464/tcp - kpasswd5
        - 593/tcp - http-rpc-epmap
        - 636/tcp - ldapssl
        - 2049/tcp - nfs
        - 3260/tcp - iscsi
        - 3268/tcp - globalcatLDAP
        - 3269/tcp - globalcatLDAPssl
        - 5985/tcp - wsman
**Detailed Service Enumeration (Nmap -sC -sV -A)**
- **Command**: `sudo nmap -sC -sV -A -p53,88,111,135,139,389,445,464,593,636,2049,3260,3268,3269,5985 -Pn -n 10.129.246.71`
- **Services Detected**:
    - **53/tcp**: Simple DNS Plus
    - **88/tcp**: Microsoft Windows Kerberos (server time: 2025-05-21 23:01:19Z)
    - **111/tcp**: rpcbind v2-4 (includes mountd, nlockmgr, status)
    - **135/tcp**: Microsoft Windows RPC  
    - **139/tcp**: Windows NetBIOS-SSN
    - **389/tcp**: LDAP - Active Directory (Domain: `PUPPY.HTB0.`)
    - **445/tcp**: Microsoft-DS (SMB) [Security Mode: signing required]
    - **464/tcp**: Kerberos kpasswd5 (no version details)
    - **593/tcp**: Microsoft RPC over HTTP 1.0
    - **636/tcp**: TCP wrapped (possibly LDAPS)
    - **2049/tcp**: NFS/NLockMgr services active (v1-v4)
    - **3260/tcp**: iSCSI service (bug in `iscsi-info` script)
    - **3268/tcp**: Global Catalog LDAP - AD
    - **3269/tcp**: TCP wrapped (possibly GC over LDAPS)
    - **5985/tcp**: Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP), title: Not Found
- **OS Detection**: Likely Microsoft Windows Server 2022 / 2012 R2 / 2016
- **Clock Skew**: +7h02m34s
- **Traceroute**:
    - Hop 1: 10.10.14.1
    - Hop 2: 10.129.246.71

# SMB
```bash
smbmap -H 10.10.11.70 -u levi.james -p 'KingofAkron2025!'
```
## Enumerating AD

```
rpcclient $> enumdomusers
user:[Administrator] rid:[0x1f4]
user:[Guest] rid:[0x1f5]
user:[krbtgt] rid:[0x1f6]
user:[levi.james] rid:[0x44f]
user:[ant.edwards] rid:[0x450]
user:[adam.silver] rid:[0x451]
user:[jamie.williams] rid:[0x452]
user:[steph.cooper] rid:[0x453]
user:[steph.cooper_adm] rid:[0x457]
```

```
rpcclient $> querygroup 0x201
        Group Name:     Domain Users
        Description:    All domain users
        Group Attribute:7
        Num Members:8
rpcclient $> querygroup 0x454
        Group Name:     HR
        Description:
        Group Attribute:7
        Num Members:1
rpcclient $> querygroup 0x459
        Group Name:     DEVELOPERS
        Description:
        Group Attribute:7
        Num Members:4
rpcclient $>
---

```



Adam Silver
HJKL2025!

Antony c edwards
ant.edwards Antman2025!

Jamie williamson
JamieLove2025!

steve tucker
Steve2025!

samuel blake
ILY2025!



- **ANT.EDWARDS** es miembro del grupo **SENIOR DEVS**.
    
- El grupo **SENIOR DEVS** tiene permiso **GenericAll** sobre el usuario **ADAM.SILVER**.

./keepass4brute.sh ../recovery.kdbx /usr/share/wordlists/rockyou.txt  
liverpool


```bash
ldapsearch -x -H ldap://10.10.11.70 -D "ANT.EDWARDS@PUPPY.HTB" -W -b "DC=puppy,DC=htb" "(sAMAccountName=ADAM.SILVER)"   
```


steph.cooper:ChefSteph2025!