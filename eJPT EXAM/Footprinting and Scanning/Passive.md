
#### General 
1. to know the IP of website 
	-> */robots.txt*
	-> */sitemap.xml*

--------
#### DNS Recon
-> Tool : *DNSRecon*
-> Website : *dnsdumpster.com* -> get you subdomains , NS , TXT , Mail Servers ,   *nmap scans* etc.

-------
#### Foot-printing Tools / Plugins 
1. `Wappalyzer` -> built-in technologies of the web site
2. `whatweb` -> command line version of wappalyzer
3. `webhttrack` -> tool to download a whole site in a local dir recursively
4. `whois` -> provide information of a website domain also *NAME SERVERS*
5. `host DOMAIN-NAME` -> will give IP of that site 
6. `Netcraft` -> A *one man army* tool for all mention tools above

----
#### WAF Foot-printing 
1. `wafw00f` -> used to see the WAF behind the web application.
	1. `waf00f IP/DOMAIN -a`

---
#### Subdomain Enumeration
1. `sublist3r` -> amazing tool to *passively* get the subdomains
	1. in case of you request is getting blocked , use a *VPN*.

----
#### Google Dorks
resource :  https://www.exploit-db.com/google-hacking-database.

1. inurl:
```
inurl: auth_user_file.txt  -> passwd file
inurl: passwd.txt
inurl: wp-config.bak 
	-> DB pass basckup file which devs prolly forgot to delete.
```
3. intitle:
```
*.site.com -> to get the subdomain  
index of -> get the lsiting dir of any website
```
5. site:
6. cache:

-----
#### Email / Passwords Harvesting 
-> tool : `theHarvester`
	finds *emails, names, subdomains, IPs, URLs,*

-> Leaked password databases
	-> http://haveibeenpwned.com
	-> harvest the emails and try to get the password from this site

