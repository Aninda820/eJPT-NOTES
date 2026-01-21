###### What we are looking for?
- Current IP address & network adapter 
- Internal networks 
- TCP/UDP services running and there respective ports 
- Other hosts on the network 

Current IP address & network adapter
```sh
ifconfig
ip address
```

TCP/UDP services running and there respective ports 
```sh
netstat -ano
ss -tulpn
```

List the Routing table by typing the bellow command
```sh
route
```

Display a list of interfaces 
```sh
cat /etc/networks 
```

List all the hosts on the system 
```sh 
cat /etc/hosts
```

Find DNS information and configurations /
Linux commands can be used to display the primary nameserver that will be used by default
```sh
cat /etc/resolv.conf
```

List all the systems connected to the same network which you compromise 
```sh
arp -a 
```
