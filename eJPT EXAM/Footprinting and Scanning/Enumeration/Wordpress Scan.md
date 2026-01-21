
we used the WPScan on the application in the enumeration mode to extract the various plugins, users, and other possible information.
```bash
wpscan --url http://blog.thm/ -e
```

used the WPScan again to Bruteforce the users by providing the usernames in the form of a dictionary.
```bash
wpscan --url http://blog.thm -P /usr/share/wordlists/rockyou.txt -U user.txt
```


List all plugins
```sh
wpscan --url http://TARGET --enumerate ap

or 

wpscan --url http://TARGET --enumerate p
```

List the plugins
```bash
gobuster dir -u http://target2.ine.local/wpcontent/plugins/ -w /usr/share/nmap/nselib/data/wp-plugins.lst
```