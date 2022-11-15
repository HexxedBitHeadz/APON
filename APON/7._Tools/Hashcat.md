https://hashcat.net/wiki/doku.php?id=example_hashes

Formatted for Windows host GPU usage.
#### MD5
```command prompt - Windows
hashcat.exe -m 0 hashes.txt rockyou.txt -O
```

#### Sha1
```command prompt - Windows
hashcat.exe -m 100 hashes.txt rockyou.txt -O
```

##### MySQL 4.1 / 5
```command prompt - Windows
hashcat.exe -m 300 hashes.txt rockyou.txt -O
```

#### MD5crypt
```command prompt - Windows
hashcat.exe -m 500 hashes.txt rockyou.txt -O
```

#### IPMI2 RAKP HMAC-SHA1
```command prompt - Windows
hashcat.exe -m 7300 hash /usr/share/wordlists/rockyou.txt -O
```

#### NTLM
```command prompt - Windows
hashcat.exe -m 1000 hashes.txt rockyou.txt -O
```

#### Sha256
```command prompt - Windows
hashcat.exe -m 1400 hashes.txt rockyou.txt -O
```

#### descrypt, DES (Unix), Traditional DES
```command prompt - Windows
hashcat.exe -m 1500 hashes.txt rockyou.txt -O
```

#### WebDav
```command prompt - Windows
hashcat.exe -m 1600 hashes.txt rockyou.txt -O
```

#### MSSQL (2012, 2014)
```command prompt - Windows
hashcat.exe -m 1731 hashes.txt rockyou.txt -O
```

#### Sha512
```command prompt - Windows
hashcat.exe -m 1800 hashes.txt rockyou.txt -O
```

#### Domain Cached Creds
```command prompt - Windows
hashcat.exe -m 2100 hashes.txt rockyou.txt -O
```
#### NetNTLMv2
```command prompt - Windows
hashcat.exe -m 5600 hashes.txt rockyou.txt -O
```

#### Kerberos TGS-REP
```command prompt - Windows
hashcat.exe -m 13100 hashes.txt rockyou.txt -O
```

#### FileZilla >= 0.9.55
```command prompt - Windows
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
```command prompt - Windows
hashcat.exe -m 18200 hashes.txt rockyou.txt -O
```

#### rar file
```command prompt - Windows
rar2john RAR_FILE.rar > output.txt
```

Had to edit the file to only include the hash!

![[Pasted image 20220408105918.png]]

```command prompt - Windows
hashcat.exe -m 13000 hashes.txt rockyou.txt -O
```

#### Kerberos 5
```
hashcat.exe -m 19700 hashes.txt rockyou.txt -O
```

