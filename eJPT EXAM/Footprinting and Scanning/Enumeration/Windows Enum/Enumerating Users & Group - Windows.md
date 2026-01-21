###### What are we looking for?
- Current user & privileges
- Additional user information 
- Other users on the system
- Groups 
- Members of the built-in administrator group 


Gather Windows logged on user information 
```rc
use post/windows/gather/enum_logged_on_users
```

Enumerate current user
```powershell
whoami
```

Check the privileges we have 
```powershell
whoami /priv
```

List current logged on user
```sh
query user
```

Display all of the accounts on the system
```powershell
net user
```

Learn about a specific user like Administrator
```powershell
net user administrator
```



List all the available groups on the target system
```powershell
net localgroup 
```

Check which users have access of admin group
```powershell
net localgroup administrators 
```

`icacls` is a **Windows command-line tool** used to:
- View file/folder permissions (ACLs)
- Add, remove, or modify permissions
```
icacls <directory name>
```


Remove any permission
```
icacls <file/directory> /remove:d "NT AUTHORITY\SYSTEM"
```
Ex: `icacls flag /remove:d "NT AUTHORITY\SYSTEM"`
