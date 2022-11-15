#### snmp-check
```bash - kali
snmp-check $TARGET
```

#### SNMPwalk
```bash - kali
sudo apt install snmp-mibs-downloader
```

```bash - kali
snmpwalk -Os -c public -v 1 $TARGET
```

Enumerating the Entire MIB Tree:
```bash - kali
snmpwalk -c public -v1 -t 10 $TARGET
```

Enumerating Windows Users
```bash - kali
snmpwalk -c public -v1 $TARGET 1.3.6.1.4.1.77.1.2.25
```

Enumerating Running Windows Processes
```bash - kali
snmpwalk -c public -v1 $TARGET 1.3.6.1.2.1.25.4.2.1.2
```

Enumerating Open TCP Ports
```bash - kali
snmpwalk -c public -v1 $TARGET 1.3.6.1.2.1.6.13.1.3
```

Enumerating Installed Software
```bash - kali
snmpwalk -c public -v1 $TARGET 1.3.6.1.2.1.25.6.3.1.2
```

![[Pasted image 20220125182150.png | 1200]]

![[Pasted image 20220125182347.png | 1200]]

#### onsixtyone single target
```bash - kali
onesixtyone $TARGET
```

#### onesixtyone range
```bash - kali
echo public > community
```

```bash - kali
echo private >> community
```

```bash - kali
echo manager >> community
```

Fill in first 3 octets of IP
```bash - kali
for ip in $(seq 1 254); do echo xxx.xxx.xxx.$ip; done > ips
```

```bash - kali
onesixtyone -c community -i ips
```

