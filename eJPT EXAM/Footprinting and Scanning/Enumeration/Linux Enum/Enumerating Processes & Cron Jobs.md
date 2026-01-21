###### What are we looking for?
- Running services 
- Cron Jobs 

Direct Link for more info and privilege escalation: [[eJPT EXAM/Privilege Escalation WINDOWS & LINUX/Linux Privilege Escalation/CRON JOB|CRON JOB]]


Check any CRON jobs running for the user 
```sh
crontab -l
```

List all the CRON jobs files 
```sh
ls -la /etc/cron*
```

Read the CRON jobs contents 
```sh
cat /etc/cron*
```