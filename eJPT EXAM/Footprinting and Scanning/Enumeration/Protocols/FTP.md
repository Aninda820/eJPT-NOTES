#### FTP Enumeration
1. `ftp_version` : to check FTP version
2. `ftp_login` : to BF login credentials
	-> user : */usr/share/metasploit-framework/data/wordlists/common_users.txt*
	-> pass : */usr/share/metasploit-framework/data/wordlists/unix_passwords.txt*
	
	NOTE : BF can cause a DOS attack on target and make it down.
	
3. `anonymous` : this module helps to check whether we can login it as anonymous user or NOT.

4. nmap script to Brute Force :
	-> `echo 'sysadmin' > users`
	-> `nmap -p 21 --script=ftp-brute 192.237.183.3 --script-args userdb=./users` 


```bash
hydra -L /usr/share/metasploit-framework/data/wordlists/unix_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt <target_IP> ftp
```

#### Wordlists
[[Wordlists]]
