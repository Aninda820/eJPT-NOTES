#### MySQL Enumeration
-> `search type:auxiliary name:mysql`

1. `mysql_version` : to get the version
2. `mysql_login` : perform a BF 
3. `mysql_enum` : help to enumerate DB, *need USER/PASS*
4. `mysql_sql` : used to execute SQL queries on the server *need USER/PASS* 
5. `mysql_schemadump` : dump all the tables of inside schema.
6. `mysql_writable_dirs` : check which directory is writable in system *need USER/PASS*
	-> /usr/share/metasploit-framework/data/wordlists/directory.txt

-> `mysql -h IP -u root -p`  : connect to the SQL DB without pass

###### `mysql_version` : to get the version
```
msfconsole -q
use auxiliary/scanner/mysql/mysql_version
set RHOSTS <target_ip>
run
```

### Wordlists
```
username root

Directory /usr/share/metasploit-framework/data/wordlists/directory.txt

Sensitive Files /usr/share/metasploit-framework/data/wordlists/sensitive_files.txt

Password File /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt

/usr/share/wordlists/metasploit/unix_passwords.txt
```

###### `mysql_login` : perform a BF 
```
use auxiliary/scanner/mysql/mysql_login
set RHOSTS demo.ine.local
set USERNAME root
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
set VERBOSE false
run
```


Exploitation:
[[Exploit MySQL]]
[[Exploit WAMP]]