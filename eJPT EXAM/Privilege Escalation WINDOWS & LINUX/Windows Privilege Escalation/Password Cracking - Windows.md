
Crack `NTLM` hashes using `john`
```sh
john --format=NT hash.txt --wordlist=/usr/share/wordlists/rockyou.txt 
```

Crack `NTLM` hashes using `hashcat`
```sh
hashcat -a3 -m 1000 hash.txt /usr/share/wordlists/rockyou.txt
```