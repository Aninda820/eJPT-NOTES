another source [[All Services]], [[Exploit SMB]]
Wordlists: [[All Services]]

#### SMB ENUMERATION CHECKLIST
- List SMB version  
- List users  
- List shares  
- List permissions  
- List OS  
- Null-session test  
- Brute-force users  
- Map drives  
- Look for vulnerabilities (SMBv1, anonymous access)

---

##### 1. Nmap Enumeration (Most Important)

###### Basic SMB script scan
```bash
nmap -sV -p445,139 <target-ip>
```
###### Deep SMB enumeration
```bash
nmap --script smb-enum-shares,smb-enum-users,smb-enum-domains -p445 <target-ip>
```


 List SMB security mode
`nmap --script smb-security-mode -p445 <target-ip>`

Check SMB version & vulnerabilities
`nmap --script smb-vuln* -p445 <target-ip>`

---

##### 2. enum4linux (BEST for SMB users)

###### Full Enumeration
```sh
enum4linux -a <target-ip>
```
######  Enumerate SMB Users Only
```sh
enum4linux -U <target-ip> 
#without cradentials

enum4linux -u <user> -p <password> -U <targetip> 
#with cradentials 
```
###### Enumerate Shares Only
```sh
enum4linux -S <target-ip>
```

---

##### 3. smbclient (Windows-style manual enumeration)

###### List Shares (Anonymous Login)
```sh
smbclient -L //<target-ip>/ -N
```
###### If anonymous doesn’t work:
```sh
smbclient -L //<target-ip>/ -U username
```
###### Access a share
```sh
smbclient //<target-ip>/sharename -N
```
###### Inside SMB prompt:
```sh
ls get file.txt put file.txt
```

---

##### 4. smbmap (Best for permissions)

## ✔ List all shares with permissions

`smbmap -H <target-ip>`

## ✔ Enumerate with credentials

`smbmap -H <target-ip> -u <user> -p <pass>`

## ✔ List directories inside a share

`smbmap -H <target-ip> -r share_name`

---

##### 5. CrackMapExec (Powerful for full network audits)

## ✔ Enumerate users + shares

`crackmapexec smb <target-ip>`
or
`crackmapexec smb <IP> — shares`

## ✔ With credentials

`crackmapexec smb <target-ip> -u <user> -p <pass> --shares`

## ✔ List sessions

`crackmapexec smb <target-ip> --sessions`

---

##### 6. RPC Enumeration (For user info)

If “Null Session” is allowed:

## ✔ Query user list

`rpcclient -U "" -N <target-ip>`

Inside RPC:

`enumdomusers queryuser <RID> enumdomgroups`

---

##### 7. Manual Null Session Check

## ✔ Classic test

`smbclient -L //<target-ip>/ -N`

#### Take access of the anonymous share
```
rpcclient -U "" -N demo.ine.local
```

If shares appear → **ANONYMOUS SMB ENABLED (vulnerability)**.

---

##### 8. Enumerate SMB OS Version

`nmap -O <target-ip>`
or:
`smbclient -L //<target-ip>/ -N | grep -i "server"`

---

##### 9. Check for SMBv1

SMBv1 is vulnerable to EternalBlue.

```
nmap --script smb-protocols -p445 <target-ip>
```

If it prints SMBv1 → **VULNERABLE SERVICE RUNNING**.

---

##### 10. Bruteforce SMB Users
###### Hydra
```sh
hydra -L users.txt -P passwords.txt smb://<target-ip>
```
###### Medusa
```sh
medusa -h <target-ip> -U users.txt -P pass.txt -M smbnt
```


### Take access of SMB using `psexec.py`
```sh
python3 psexec.py Administrator@10.5.25.42   # press enter then enter password
```
---

### Bonus — Vulnerabilities to Test on Your Network
You mentioned you want to test all weaknesses. Test these:

|Vulnerability|Tool to Test|
|---|---|
|SMBv1 enabled|nmap smb-protocols|
|Null session|smbclient -N|
|Weak passwords|hydra / medusa|
|Open writeable shares|smbmap|
|Server misconfig|enum4linux|
|OS outdated|nmap -sV -O|

---

### Enumerate SMB 

```
#!/bin/bash

# Obtain the target and wordlist from command-line arguments
target="$1"
wordlist="$2"

# Check if both arguments are provided
if [ -z "$target" ] || [ -z "$wordlist" ]; then
    echo "Usage: $0 <target> <wordlist>"
    exit 1
fi

# Check if the wordlist file exists
if [ ! -f "$wordlist" ]; then
    echo "Error: Wordlist file '$wordlist' not found."
    exit 1
fi

# Initialize an array to store successful shares
successful_shares=()

# Loop through each share in the wordlist
while read -r share; do
    echo -e "Testing share: \e[34m$share\e[0m"
    smbclient "//$target/$share" -N -c "ls" &>/dev/null

    if [ $? -eq 0 ]; then
        successful_shares+=("$share")
    fi
done < "$wordlist"

# Output the results
if [ ${#successful_shares[@]} -gt 0 ]; then
    echo -e "\n\e[32m[+] Successfully accessed shares:\e[0m"
    for share in "${successful_shares[@]}"; do
        echo -e "\e[32m[+] \e[34m$share\e[0m"
    done
else
    echo -e "\e[31m[-] No accessible shares found.\e[0m"
fi

echo -e "\n[+] SMB enumeration completed."

```
Save this file `smbenumshare.sh`
wordlist: /root/Desktop/wordlists/shares.txt

Walkthrough link:
https://0xdf.gitlab.io/cheatsheets/smb-enum

https://systemweakness.com/how-to-enumerate-smb-for-ethical-hackers-and-pentesters-29e4ac4da3c4

https://medium.com/@mpotisambo8/smb-enumeration-8793abac9ce0


User brute force SMB  
```bash
msfconsole -q
use auxiliary/scanner/smb/smb_login
set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
set RHOSTS demo.ine.local
set VERBOSE false
exploit
```