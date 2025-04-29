#### Checks

- [ ] Check version for exploits

- [ ] Check mails for the presence of credentials

#### Commands

manually login to the application:

```
#connect and check for banner 
telnet $TARGET 110 

#guess login credentials 
USER $Username 
PASS $Password

#list all emails 
list 

#retrieve email number 5 for example 
retr 5
```

#### Other Commands: 
```bash - kali
telnet $TARGET
```

```bash  - kali
nmap -p 23 --script=telnet-ntlm-info.nse $TARGET
```

#### Bruteforce:

```bash 
sudo nmap --script pop3-brute -p110 <RHOST> auxiliary/scanner/pop3/pop3_login 
```

```bash - kali
hydra $TARGET -l root -P /usr/share/seclists/Passwords/xato-net-10-million-passwords-1000000.txt telnet
```

