
###### What we are looking for 
- Current user & privileges 
- Other users on the system 
- Groups

Groups
```bash
groups <user_name>
```
List all groups in  system
```
getent group

or 

cat /etc/group
```

Other users on the system 
```bash
cat /etc/passwd | grep home
ls /home
```


Create a new user
```bash
useradd -m bob -s /bin/bash
```
Add that user to the root group
```bash
usermod -aG root bob #add to the root group 
```


Find out which user when login on the system
```bash
last
lastlog
```