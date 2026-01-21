
_NOTE_ :
	: while a *non-privileged* user , NMAP by defaults do a TCP Connect Scan.
		-> it is very _LOUD_ (does 3 way handshake) and not preferable 
		-> can only be useful if there's a consent for no detection on network & accuracy is required as it does 3 Way Handshake
	: While a *root* user : NMAP do a _SYN ACK_ scan


_tip_ : 
	-> always use `-sS` SYN ACK Ping flag explicitly with a not privileged used.
	-> it is the most efficient scan because 
		-> SYN is not an UNCOMMMON packet so , it won't raise any alarm
		-> doesn't make any connection logs on target side as  not settuping full connection , send RST after getting SYN ACK
		->  SYN is NOT blocked also acceptable by almost every OS , firewall as it is necessary to do 3 way handshake.

#UDP : In case of not found anything open or usefull it's worth checking the UDP ports
	-> `nmap -sU IP`
	-> `nmap -sU IP -p 53,137,138,139`


##### Usage

1. Version Intensity of services :
	-> `nmap -p- -sV --version-intensity [0-9] IP -Pn -T4`
	-> higher the number , higher the possibility to a correct service & version.

2. OS guess (aggressively) :
	-> `nmap -p- -O --osscan-guess IP -Pn -T4`


##### Nmap Scripting Engine

_dir_ : _/usr/share/nmap/scripts_

1. `nmap --script-help=SCRIPT`
	-> tells about the script status whether is a default script & if it is safe to use

2. `nmap --script=SCRIPT,SCRIPT,SCRIPT IP`
	-> manually running Multiple scripts.

3. `nmap --script=ftp-* IP`
	-> will run all script start from _ftp-_


TIP : adding all these three together in a single `flag` , `-A`
	-> service & version scans
	-> OS Scan
	-> Common Scripts

### LAB Commands
```bash
nmap 192.118.107.3 -p- -T4 -sS -sV --version-intensity 8 -O --osscan-guess

nmap 192.118.107.3 -p- -T4 -sS -sV --version-intensity 8 -O --osscan-guess -sC

nmap 192.118.107.3 -p- -T4 -sS -A
```





### Port Scan using Metasploit
##### For TCP scan
```
search portscan
use auxiliary/scanner/portscan/tcp
setg rhosts <target_ip>
run
```

##### UDP Scan
```
search udp_sweep
use auxiliary/scanner/discovery/udp_sweep

```


Bash Script for Port scan
```
#!/bin/bash
for port in {1..1000}; do
 timeout 1 bash -c "echo >/dev/tcp/$1/$port" 2>/dev/null && echo "port $port is open"
done
```