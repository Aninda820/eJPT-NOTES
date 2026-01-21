
Install Samba on Linux
```bash
sudo apt install samba -y
```

Enable SMB server on Linux
```bash
sudo systemctl enable smbd
```

Now add this line at the end of the file `/etc/samba/smb.conf`
```bash
[share]
   path = /srv/samba/share
   browseable = yes
   read only = no
   guest ok = yes
```

Create a share directory 
```bash
sudo mkdir -p /srv/samba/share
sudo chmod 777 /srv/samba/share
```


--------------------
###### Access the file
List the shares 
```bash
smbclient -L  //<ip>/

enum4linux -a <ip>
```

Access the shares
```bash
smbclient \\\\<ip>\\<share_name>
```