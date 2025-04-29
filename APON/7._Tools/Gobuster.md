#### VHOST discovery
```bash - kali
gobuster vhost -u http://forge.htb -w /usr/share/seclists/Discovery/DNS/subdomainstop1million-5000.txt | grep -v 302
```

```bash - kali
gobuster vhost -u http://inlanefreight.htb:37816 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain

```


#### https with php extension
```bash - kali
gobuster -w directory-list-2.3-medium.txt -t 50 -k -u https://administrator1.friendzone.red/ -x php
```