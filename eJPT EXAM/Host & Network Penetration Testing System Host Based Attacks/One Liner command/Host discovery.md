Command for Host discovery work on Linux 
```
for i in $(seq 254); do ping 192.88.66.${i} -c1 -W1 & done | grep from
```


## ✅ **Basic Host Discovery (Ping Sweep)**

`1..254 | % { if (Test-Connection -Count 1 -Quiet 192.168.1.$_) { "Host alive: 192.168.1.$_" } }`

🔹 Change `192.168.1.` to your target subnet.

---

## ⚡ **Faster Version (Timeout Reduced)**

`1..254 | % { if (Test-Connection 192.168.1.$_ -Count 1 -Quiet -TimeoutSeconds 1) { "UP: 192.168.1.$_" } }`

---

## 🔥 **Host Discovery via TCP (Stealthier than ICMP)**

Useful when **ICMP is blocked** (common in CTFs):

`1..254 | % { try { (New-Object Net.Sockets.TcpClient).Connect("192.168.1.$_",80); "Host alive: 192.168.1.$_" } catch {} }`

(Change port `80` to `445`, `22`, `3389` depending on target.)

---

## 🧠 **Ultra-short version (for notes)**

`1..254|%{Test-Connection 192.168.1.$_ -Quiet -Count 1 && echo 192.168.1.$_}`