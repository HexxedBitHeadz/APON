#### enumeration
```bash - kali
nmap -A $TARGET
```

![[Pasted image 20221109111431.png]]

Look for Domain info:  `MAILMAN.com`

add to /etc/hosts:

```bash - target
sudo echo '$TARGET MAILMAN.com' | sudo tee -a /etc/hosts
```

```bash - target
host -l $DOMAIN $TARGET
```

```bash - target
dig axfr $DOMAIN @$TARGET
```

```bash - target
#### for loop for host things (replace 'x' with your first 3 target octets)
for ip in $(seq 1 254); do host -t PTR xxx.xxx.x.$ip $TARGET; done | grep "name pointer"
```

#### dig
```
dig @$TARGET -x $TARGET
```

Look for something like:
`120.168.192.in-addr.arpa. 604800 IN     SOA     matrimony.off. `

```bash - kali
dig axfr @$TARGET matrimony.off 
```

---

>domain.local 
ns1.domain.local
admin.domain.local

www.domain.local

>Add  your findings to /etc/hosts

```bash - target
sudo echo '$TARGET domain.local ns1.domain.local admin.domain.local www.domain.local' | sudo tee -a /etc/hosts
```

![[Pasted image 20220823161951.png]]

#### dnsrecon
```
dnsrecon -r $TARGET/24 -n $TARGET
```

#### nslookup
```bash - kali
nslookup
```

```bash - kali
$TARGET
```

```bash - kali
name = xxx.domain.local
```

#### Gobuster
```bash - kali
gobuster dns -d domain.local -w /usr/share/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt 
```

If any more are found from gobuster, add also to /etc/hosts.

