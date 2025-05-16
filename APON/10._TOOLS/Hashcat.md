#### Examples
https://hashcat.net/wiki/doku.php?id=example_hashes
https://github.com/frizb/Hashcat-Cheatsheet/blob/master/README.md

#### Device selection
Try to list devices.
```
hashcat -I
```

-d $DEVICE
```
hashcat.exe -m 0 hashes.txt -a3 ?a?a?a?a?a?a?a ‐‐increment-min 5 -O -d 1
```

#### Show cracked
Just append `--show` to existing command, like:
```
hashcat.exe -m 0 hashes.txt rockyou.txt -O --show
```

#### Hashcat Utilities
[[8.3.4._Hashcat Utilities]]

#### Brute force mode
- ?a == represents all possible characters (lowercase, uppercase, digit, special)
- --increment-min=5 will start at 5 characters and work its way up.
-
![[image-10 1.png]]
```bash - kali
hashcat.exe -m 0 hashes.txt -a3 ?a?a?a?a?a?a?a -i ‐‐increment-min 5 -O
```

#### MD5
```bash - kali
hashcat.exe -m 0 hashes.txt rockyou.txt -O
```

#### Sha1
```bash - kali
hashcat.exe -m 100 hashes.txt rockyou.txt -O
```

##### MySQL 4.1 / 5
```bash - kali
hashcat.exe -m 300 hashes.txt rockyou.txt -O
```

#### MD5crypt
```bash - kali
hashcat.exe -m 500 hashes.txt rockyou.txt -O
```

#### NTLM
```bash - kali
hashcat.exe -m 1000 hashes.txt rockyou.txt -O
```

#### Sha256
```bash - kali
hashcat.exe -m 1400 hashes.txt rockyou.txt -O
```

#### descrypt, DES (Unix), Traditional DES
```bash - kali
hashcat.exe -m 1500 hashes.txt rockyou.txt -O
```

#### WebDav
```bash - kali
hashcat.exe -m 1600 hashes.txt rockyou.txt -O
```

#### Ansible
```bash - kali
hashcat.exe -m 16900 hashes.txt rockyou.txt -O
```

#### MSSQL (2012, 2014)
```bash - kali
hashcat.exe -m 1731 hashes.txt rockyou.txt -O
```

#### Sha512
```bash - kali
hashcat.exe -m 1800 hashes.txt rockyou.txt -O
```

#### Domain Cached Creds
```bash - kali
hashcat.exe -m 2100 hashes.txt rockyou.txt -O
```

#### LM
```bash - kali
hashcat.exe -m 3000 hashes.txt rockyou.txt -O
```

#### Bcrypt
```bash - kali
hashcat.exe -m 3200 hashes.txt rockyou.txt -O
```

#### NetNTLMv2
```bash - kali
hashcat.exe -m 5600 hashes.txt rockyou.txt -O
```

#### Kerberos TGS-REP
```bash - kali
hashcat.exe -m 13100 hashes.txt rockyou.txt -O
```

#### FileZilla >= 0.9.55
```bash - kali
hashcat.exe -m 1500 hashes.txt rockyou.txt -O
```

If older, use:
```
git clone https://github.com/l4rm4nd/FileZilla-Password-Decryptor
```

>If salt has single quotes, try wrapping value in double quotes to avoid issues
```
salt = "0'?dQF]h~Y0`\Q=sFUO?v!1HAZ/6hGcY1`W~O3hyQ?h]h'fg\{HXu-Ef^BwA4.7!".encode('utf-8')
```

The XML escapes the special characters in the following way, don't put them in the code as is but convert the back to the original characters:

```python
&amp; = &
&lt; = <
&apos; = '
&quot; = "
```

#### Kerberos AS-REP
```bash - kali
hashcat.exe -m 18200 hashes.txt rockyou.txt -O
```

#### rar file
```bash - kali
rar2john RAR_FILE.rar > output.txt
```

Had to edit the file to only include the hash!
`$rar5$16$53blacf5cd3d02dafdf50f1cb79e46e5$15$a8761ee8467302d9ee19284F60713dd$8$514688cebd7cab7b`

```bash - kali
hashcat.exe -m 13000 hashes.txt rockyou.txt -O
```

#### Kerberos 5
``` bash - kali
hashcat.exe -m 19700 hashes.txt rockyou.txt -O
```

#### sshng
``` bash - kali
hashcat.exe -m 22931 hashes.txt rockyou.txt -O
```