
Convert noninteractive shell to interactive shell
```sh
/bin/bash -i
export TERM=xterm
export SHELL=bash
PATH=/usr/loacl/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```
List all the environment variable 
```bash
env
```


Using Python
```sh
python -c 'import pty;pty.spawn("/bin/bash")'

python3 -c 'import pty;pty.spawn("/bin/bash")'
```


