
##### Main purpose
To manage and monitor network devices



SNMP is an application layer protocol that typically use UDP for transport 

###### port use:
port 161 (UDP)
port 162 (UDP)

SNMP v1: Use community strings (essentially username and password)
SNMP v2: username and password
SNMP v3: Introduced security features, including encryption, message integrity and user-based authentication.

##### SNMP enumeration:
Extract system information: collect system related information like `Device name`, `Operating system`, `Software versions`, `Network interfaces` and more 

Identify SNMP Community Strings: Test for default or week community strings, which can grant unauthorized access to dive information

Retrieve Network Configurations: Gather information about `routing tables`, `Network interfaces`, `IP addresses` and other network-specific details

Collect user and Group Information: In some cases, SNMP can reveal `user account information` and `access permissions`.

Identify Services and Applications: Find out which services and applications are running on the target devices, potentially leading to further attack vectors


###### Check the SNMP port open or not
```
nmap -sU -p161 <target_ip>
```

###### List nse scripts for SNMP
```
ls /usr/share/nmap/scripts | grep -e "snmp"
```

###### Bruteforce SNMP using nmap for community strings 
```
nmap -sU -p61 --script=snmp-brute <target_ip>
```

###### Find the version of SNMP
```
nmap -sU -p161 -sV <taarget_ip>
```

###### To extract more information from SNMP we will use `snmpwalk`
```
snmpwalk -v 1 -c <community_string> <target_ip>
```
v1 is the version hear, it could be anything first check the snmp version first


###### We run all the SNMP scripts
```
nmap -sU -p161 --script snmp-* <target_ip> > snmp_info
```