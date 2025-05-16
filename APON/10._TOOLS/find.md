### File finding
```
find / -type f -iname "secretsdump.py" 2>/dev/null
```
#### History hunting
```bash - linux
find / -iname .bash_history 2>/dev/null
```
#### Hunting for config files.
```bash - linux
find / -iname *config* 2> /dev/null
```
```bash - linux
find / -iname *conf* 2> /dev/null
```
```bash - linux
find / -iname *.cnf 2> /dev/null
```
Hunting for config files that contain 'password'
```bash - linux
find / -iname '*config*' -exec grep -rli 'password' {} \; 2> /dev/null
```
Hunting for config php files that contain 'password'
```bash - linux
find / -iname '*config*.php' -exec grep -rli 'password' {} \; 2> /dev/null
```
```bash - linux
find / -iname '*config*.php' -exec grep -rli 'DBPASS' {} \; 2> /dev/null
```
Find files by group (network group in example):
```bash - kali
find / -xdev -group network 2>/dev/null
```
#### whereis
```bash - kali
whereis phpmyadmin
```
#### Find local.txt file
```bash - linux
find / -iname local.txt 2> /dev/null
```
