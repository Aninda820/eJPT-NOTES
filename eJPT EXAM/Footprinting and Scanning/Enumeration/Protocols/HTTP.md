
The question hints that sensitive directories might contain critical information, and the `http-enum` script from the `nmap` scan indicates that a `passwords` directory exists on the server.

#### HTTP Enumeration
1. `http_version` : get the adject version
2. `http_header` : get the uncommon headers
3. `robots_txt` : get you the robots.txt
4. `dir_scanner` : dir enumeration module in msf
	-> /usr/share/metasploit-framework/data/wmap/wmap_dirs.txt
5. `files_dir` : file enumeration just like dir enum
	-> /usr/share/metasploit-framework/data/wmap/wmap_files.txt
6. `http_login` : BF the creds of a HTTP website 
	*user lists*
	-> /usr/share/metasploit-framework/data/http_default_users.txt
	-> /usr/share/metasploit-framework/data/wordlists/namelist.txt
	*pass lists*
	-> /usr/share/metasploit-framework/data/http_default_pass.txt
	-> /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 
7. `http_userdir_enum` : get the potential usernames form apache website.

Exploitation of [[Http File Server (Rejetto)]], [[Apache Tomcat]]
