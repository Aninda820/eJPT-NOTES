#### SSH Enumeration
-> `search type:auxiliary name:ssh` 

1. `ssh_version` : get the adject version

-> if the target is configured to authenticate by a USER:PASS pair then use this
2. `ssh_login` : perform a BF for USER/PASS

->  if the target is configured to authenticate by a PUBKEY pair then use this
3. `ssh_login_pubkey` : perform a BF for PUBLIC KEYS.

4. `ssh_enumusers` : used to enumerate users.
	-> /usr/share/metasploit-framework/data/http_default_users.txt
	->/usr/share/metasploit-framework/data/wordlists/common_users.txt
	-> usr/share/metasploit-framework/data/wordlists/common_passwords.txt


#### Exploitation
[[metasploit 2 full exploitation]], [[Vulnerable SSH server]]
