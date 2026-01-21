
###### What are we looking for?
- Hostname
- OS name
- OS build & service pack 
- OS Architecture
- Installed updates / Hotfixes 

```sh
hostname
```

```sh
systeminfo
```

The following Windows commands can be used to enumerate a list of installed updates in addition to the HotFix URL
```
wmic qfc get Caption,Description,HotFixID,InstalledOn
```

```
type c:\windows\system32\eula.txt
```