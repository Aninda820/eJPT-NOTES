
#### DNS Zone Transfer
#zone-interrogation #zone-transfer 

-> Tools : 
1. `dnsrecon`  : `dnsrecon -d DOMAIN.com`
2. `dnsenum` : 
3. `dig` :
4. `fierce` : `fierce -dns DOMAIN.com`



#### Host Discovery 

###### nmap
1. `-sn` : flag to deny port scan and scan host/IPs on the target
	-> `sudo nmap -sn IP`
	->  

###### netdiscover (scan hosts on LOCAL network)
1.  `netdiscover` : tool which is used to discover host on network 
	-> it also captures ARP request to get MAC to IP & IP to Mac.
		-> `netdiscover -i INTERFACE` 
		-> `netdiscover -n 20` -> will only scan first 20 hosts.
		-> `netdiscover -l` -> list available network interface.
		-> `netdiscover -i INTERFACE -r network/subnet` 

#### Port Scanning

1. `nmap -Pn -F IP` : -F will scan common 100 ports
2. `nmap -Pn -sU IP` : default scan will only scan TCP ports, scan UDP ports
3. 