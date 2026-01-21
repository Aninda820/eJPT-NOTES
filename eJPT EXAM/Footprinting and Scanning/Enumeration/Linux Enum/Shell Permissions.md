
To check the permissions each shell has
```sh
cat /etc/shells | while read shell; do ls -l $shell 2>/dev/null; done
```

