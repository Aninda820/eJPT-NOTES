
What we are looking for?
- Running processes & services 
- Scheduled tasks

List all the processes running on the target system
```meterpreter
ps
```

List the process id of a particular process 
```meterpreter
pgrep <process_name>
Ex: pgrep explorer.exe
```

Command to get a list of started services (These are all background services)
```powershell
net start
```

```
wmic service list brief
```

List running tasks and also list running task those are running under another process
```
tasklist /SVC
```


##### List the schedule tasks 
```
schtasks /query /fo LIST /v
```

