#### SMTP Enumeration
-> `search type:auxiliary name:smtp`
-> Port : 25 , 465 , 587 

### Our Main gole 
We can bruteforce username using `smtp` protocol and then we can obtain those username for login `ssh` if enable on the target system and brute force password for take remote access of the target system

We can enumerate the version of SMTP as well as user accounts on the target system.


1. `smtp_version` : get the version of SMTP -> also give email/domain of the version
2. `smtp_enum` : enumerate users , emails on the SMTP.

-> `nc demo.ine.local 25` : connect with SMTP
-> `EHLO openmailbox.xyz` : Start with SMTP (this mail comes on banner when you try to connect with `nc` or `telnet`.
-> `EHLO openmailbox.xyz` : pop up all the commands present on the server
-> `VRFY user` : replace user with actual user like admin : to check whether a user is present on the server or not !!

--> command to enumerate users 
		`smtp-user-enum -t demo.ine.local -U /usr/share/commix/src/txt/usernames.txt -M VRFY`

-> Commands to send mail on the server to any user 
```bash
telnet demo.ine.local 25
HELO attacker.xyz
mail from: admin@attacker.xyz
rcpt to:root@openmailbox.xyz
data
Subject: Hi Root
Hello,
This is a fake mail sent using telnet command.
From,
Admin
.
```

-> `sendmail` : command to send mails over SMTP though Terminal 
	-> `sendemail -f admin@attacker.xyz -t root@openmailbox.xyz -s demo.ine.local -u Fakemail -m "Hi root, a fake from admin" -o tls=no`
	-> `-f` : FROM
	-> `-t` : TO
	-> `-s` : SMTP Server (IP)	
	-> `-u` : subject
	-> `-m` : message body
	-> `-o` : setting the TLS off 

##### Exploitation of SMTP
[[SMTP exploitation]]
