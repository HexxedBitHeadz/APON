```bash - kali
telnet $TARGET
```

```bash  - kali
nmap -p 23 --script=telnet-ntlm-info.nse $TARGET
```

![[Hydra#Hydra against telnet]]