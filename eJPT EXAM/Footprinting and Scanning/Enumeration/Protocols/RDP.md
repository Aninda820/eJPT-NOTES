Default Port number is 3389
##### NMAP scan for find RDP port
```
nmap -sV -sC -sS <target_ip> -v
```

If wanna you see any unknown port number and there no service name displayed that moment use this `msfconsole module` called `rdp_scanner`  
This module confirm this port running RDP or not
```
search rdp-scanner
use auxiliary/scanner/rdp/rdp_scanner
show options
setg rhosts <target_ip>
set rpost <target_port>
run
```


#### Bruteforce the `username` and `password` for RDP authentication 
```
hydra -L /usr/share/metasploit-framework/data/wordlists/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt rdp://<target_ip> -s <port>
```


##### Exploitation of RDP
[[eJPT EXAM/Exploitation/Exploit RDP|Exploit RDP]]
[[eJPT EXAM/Host & Network Penetration Testing System Host Based Attacks/Windows/A Exploiting Windows Vulnerabilities/Exploit RDP|Exploit RDP]]
