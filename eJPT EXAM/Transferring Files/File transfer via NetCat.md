
Sender 
```bash
nc 192.168.0.106 4444 < file.bin
```

Receiver 
```bash
nc -lvnp 4444 > file.bin
```
-------------

Sender
```bash
cat file.txt | nc 192.168.0.106 4444
```

Receiver
```sh
nc -lvnp 4444
```

