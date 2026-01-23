
Gather privileges enumeration of your current user
```msfconsole
use post/windows/gather/win_privs
```

Gather information about currently logged on user via the windows Registry 
```msfconsole
use post/windows/gather/enum_logged_on_users
```

Check the target machine is a virtual machine or not
```msfconsole
use post/windows/gather/checkvm
```

List all Installed application on the target system
```msfconsole
use post/windows/gather/enum_applications
```

Check for other computers on your same network
```msfconsole
use post/windows/gather/enum_computers
```

Enumerate installed patches on the target system
```msfconsole
use post/windows/gather/enum_patches
```

Gather SMB shares enumeration on target system or network
```msfconsole
use post/windows/gather/enum_shares
```


##### Automation script for windows privilege escalation 
https://github.com/411Hall/JAWS

