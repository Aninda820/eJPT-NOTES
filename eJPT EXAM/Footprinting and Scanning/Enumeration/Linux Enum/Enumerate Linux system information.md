###### What we are looking for
- Hostname 
- Distribution & distribution release version 
- Kernel version & architecture
- CPU information 
- Disk information & mounted drives
- Installed packages/Software

Hostname 
```bash
hostname 
```

Distribution & distribution release version 
```bash
cat /etc/*release
```

Kernel version & architecture
```bash
uname -a
uname -r 
```

CPU information 
```bash
lscpu
```

Disk information & mounted drives
```bash
df -h

or 

lsblk
```

Installed packages/Software
```bash
dpkg -l 
```