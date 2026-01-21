###### Linux Post Exploitation Modules for enumeration 

The MSF provides us with various post exploitation modules for both Windows
and Linux.

- We can utilize these post exploitation modules to enumerate information about
the Linux system we currently have access to:
+ Enumerate system configuration
+ Enumerate environment variables
+ Enumerate network configuration
+ VM check
+ Enumerate user history

```bash 
msf > use post/linux/gather/enum_configs
#check all Linux configrations 

msf > use post/multi/gather/env

msf > use post/linux/gather/enum_network

msf > use post/linux/gather/enum_protections

msf > use post/linux/gather/enum_system
#Linux Gather system and user information 

msf > use post/linux/gather/checkcontainer

msf > use post/linux/gather/checkvm
#Check target system is a virtual mahine or not

msf > use post/linux/gather/enum_users_history

msf > use post/multi/manage/system_session

msf > use post/linux/manage/download_exec

msf > notes
```


##### Automation script:
LinEnum script:
https://github.com/rebootuser/LinEnum/blob/master/LinEnum.sh
