


OFFsec: all metasploit payload and intro
https://www.offsec.com/metasploit-unleashed/msfcli/


## 📦 **8. List All Modules (brute-force method)**

**8. List All Modules (brute-force method)**
```
show auxiliary
show payloads
show exploits
show encoders
show nops
```


Search for Exploits by Service or Port:
```
search port:445
search name:samba
search name:apache
```

Search by OS / Platform:
```
search platform:linux
search platform:windows
search platform:android
search platform:osx
```

Specific category:
```
search auxiliary/scanner/smb
```

General auxiliary modules:
```
search type:auxiliary
```

Search Syntax Format:
```
search auxiliary:ftp
search payload:windows
search os:android
```


Search version or login something:
```
search type:auxiliary name:version
search type:auxiliary name:ftp
```



#### Create Workspace 
```
service postgresql start

msfconsole -q

workspace -h

workspace -a pentest_1

workspace

db_status 

workspace pentest_1 #change workspace
```

##### Import Data into workspace
```
db_import nmap.xml
```

##### List the host
```
hosts
```

##### List the services running on the host
```
services
```

https://www.offsec.com/metasploit-unleashed/pivoting/


Download `autopwn` plugin 
```
wget https://raw.githubusercontent.com/hahwul/metasploit-autopwn/master/db_autopwn.rb 
```

```
sudo mv db_autopwn.rb /usr/share/metasploit-framework/plugins
```

```
msfconsole -q
load db_autopwn 

db_autopwn #Display help manu
```

```
db_autopwn -p -t -PI <port number> #find exploit for a spacific port
```

Analyze
```
msf6 > analyze #Help find proper exploitable acording to vulnerbility 
```

Vulns
```
msf6 > vulns # determine the potensitial vulnarbility on tergate IP
```

kiwi
```
msf6 > load kiwi #Dump the hash from SAM
msf6 > lsa_dump_sam #Get NTLM cradencials 
```



### WMAP scan vulnerability of a website 

```
load wmap #Load the plugin 

wmap_sites -h

wmap_sites -a <target_ip> #For a target or site

wmap_targets -h

wmap_targets -t http://ip

wmap_targets -l #list all the targets

wmap_run -h

wmap_run -t #for show all enable modules

wmap_run -e #For run vulnerability scan agains all the targets


wmap_vulns -l #List all the vulnerabilitys detect by this tool
```