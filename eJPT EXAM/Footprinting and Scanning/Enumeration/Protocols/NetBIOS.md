`nbtscan` is a **network reconnaissance tool** used to **scan IP networks for NetBIOS information**. It queries NetBIOS Name Service to discover Windows machines and their details
scan networks for NetBIOS name information
```
nbtscan <target_ip or Target_ip subnet range>

or 

nmblookup -a <Target_ip>
```

##### Check the name-server or NetBIOS running on the system 
```bash
nmap -sU -p137 <target_ip>
```
or
```bash
nmap -sU -sV -T4 --script nbstat.nse -p137 -Pn -n <ip>
```

```bash
nmap -sV -p 139,445 <ip or Domain>
```


###### Run the Scan for find what version of SMB running on the system 
```bash
nmap -p445 --script smb-protocols <ip>
```
###### Its tell the security level of the SMB
```
nmap -p445 --script smb-security-mode <ip>
```
###### Find the username of the target system by SMB user enumeration 
```
nmap -p445 --script smb-enum-users.nse <target_ip>
```


### Take access of the SMB using `psexec.py`
```
python3 psexec.py Administrator@10.5.25.42   # press enter then enter password 
```


