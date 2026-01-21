1. Nessus 
	-> `nessus` essentials (free can scan upto 16 IPs)
	-> import it's output to MSF to increase effeciency

2. WMAP :
	-> Can be used as plugin in MSF
	-> `load wmap`
	-> `wmap_sties <SITE.COM>`
	-> `wmap_targets <SITE.COM>`
	-> `wmap_run -t` :to create a new target
	-> `wmap_run -e` : to run the scan and exploitation

```
load wmap #Load the plugin 

wmap_sites -h

wmap_sites -a <target_ip> #For a target or site

wmap_targets -h

wmap_targets -t http://ip

wmap_targets -l #list all the targets

wmap_run -h

wmap_run -t #for show all enable modules

wmap -e #For run vulnerability scan agains all the targets


wmap_vulns -l #List all the vulnerabilitys detect by this tool
```