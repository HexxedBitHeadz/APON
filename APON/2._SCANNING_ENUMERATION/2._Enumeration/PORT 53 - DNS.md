
### **Checks**

- [ ] Try zone transfer
- [ ] Brute force subdomains

![[tooldev-dns.webp]]

#### DNS Record
|**DNS Record**|**Description**|
|---|---|
|`A`|Returns an IPv4 address of the requested domain as a result.|
|`AAAA`|Returns an IPv6 address of the requested domain.|
|`MX`|Returns the responsible mail servers as a result.|
|`NS`|Returns the DNS servers (nameservers) of the domain.|
|`TXT`|This record can contain various information. The all-rounder can be used, e.g., to validate the Google Search Console or validate SSL certificates. In addition, SPF and DMARC entries are set to validate mail traffic and protect it from spam.|
|`CNAME`|This record serves as an alias for another domain name. If you want the domain www.hackthebox.eu to point to the same IP as hackthebox.eu, you would create an A record for hackthebox.eu and a CNAME record for www.hackthebox.eu.|
|`PTR`|The PTR record works the other way around (reverse lookup). It converts IP addresses into valid domain names.|
|`SOA`|Provides information about the corresponding DNS zone and email address of the administrative contact.|

#### Misconfiguration and Vulnerabilities 

| **Option**        | **Description**                                                                |
| ----------------- | ------------------------------------------------------------------------------ |
| `allow-query`     | Defines which hosts are allowed to send requests to the DNS server.            |
| `allow-recursion` | Defines which hosts are allowed to send recursive requests to the DNS server.  |
| `allow-transfer`  | Defines which hosts are allowed to receive zone transfers from the DNS server. |
| `zone-statistics` | Collects statistical data of zones.                                            |

#### enumeration
```
nmap -A $TARGET
```

Look for Domain info:  `MAILMAN.com`

add to /etc/hosts:

```bash - target
sudo echo '$TARGET MAILMAN.com' | sudo tee -a /etc/hosts
```

```bash - target
sudo mousepad /etc/hosts
```

```bash - target
host -l MAILMAN.com $TARGET
```

```
Aliases: MAILMAN.com name server dc.MAILMAN.com. 
_msdcs .MAILMAN.com name server dc.MATLMAN.com. 
dc.MATLMAN.com has address 192.168.145.149 
DomainDnsZones.MAILMAN.com has address 192.168.50.149 
DomainDnsZones .MAILMAN.com has address 192.168.120.149 
ForestDnsZones .MAILMAN.com has address 192.168.50.149 
ForestDnsZones.MAILMAN.com has address 192.168.120.149
```

```bash - target
dig axfr MAILMAN.com @$TARGET
```

```bash - target
#### for loop for host things (replace 'x' with your first 3 target octets)
for ip in $(seq 1 254); do host -t PTR xxx.xxx.x.$ip $TARGET; done | grep "name pointer"
```

#### dig

| **Command**                                                                                                                                                                                                                             | **Description**                          |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| `dig ns <domain.tld> @<nameserver>`                                                                                                                                                                                                     | NS request to the specific nameserver.   |
| `dig any <domain.tld> @<nameserver>`                                                                                                                                                                                                    | ANY request to the specific nameserver.  |
| `dig axfr <domain.tld> @<nameserver>`                                                                                                                                                                                                   | AXFR request to the specific nameserver. |
| `dnsenum --dnsserver <nameserver> --enum -p 0 -s 0 -o found_subdomains.txt -f ~/subdomains.list <domain.tld>`                                                                                                                           | Subdomain brute forcing.                 |
| `for sub in $(cat /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt);do dig $sub.domain.tld @$TARGET \| grep -v ';\|SOA' \| sed -r '/^\s*$/d' \| grep $sub \| tee -a subdomains.txt;done<br>` |                                          |
| `dnsenum --dnsserver $TARGET --enum -p 0 -s 0 -o subdomains.txt -f /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt <domain.tld>`
| 

### Common dig Commands

|Command|Description|
|---|---|
|`dig domain.com`|Performs a default A record lookup for the domain.|
|`dig domain.com A`|Retrieves the IPv4 address (A record) associated with the domain.|
|`dig domain.com AAAA`|Retrieves the IPv6 address (AAAA record) associated with the domain.|
|`dig domain.com MX`|Finds the mail servers (MX records) responsible for the domain.|
|`dig domain.com NS`|Identifies the authoritative name servers for the domain.|
|`dig domain.com TXT`|Retrieves any TXT records associated with the domain.|
|`dig domain.com CNAME`|Retrieves the canonical name (CNAME) record for the domain.|
|`dig domain.com SOA`|Retrieves the start of authority (SOA) record for the domain.|
|`dig @1.1.1.1 domain.com`|Specifies a specific name server to query; in this case 1.1.1.1|
|`dig +trace domain.com`|Shows the full path of DNS resolution.|
|`dig -x 192.168.1.1`|Performs a reverse lookup on the IP address 192.168.1.1 to find the associated host name. You may need to specify a name server.|
|`dig +short domain.com`|Provides a short, concise answer to the query.|
|`dig +noall +answer domain.com`|Displays only the answer section of the query output.|
|`dig domain.com ANY`|Retrieves all available DNS records for the domain (Note: Many DNS servers ignore `ANY` queries to reduce load and prevent abuse, as per [RFC 8482](https://datatracker.ietf.org/doc/html/rfc8482)).|
```
dig @$TARGET -x $TARGET
```

Look for something like:
`120.168.192.in-addr.arpa. 604800 IN     SOA     matrimony.off. `

```bash - kali
dig axfr @$TARGET matrimony.off 
```



---

>
domain.local 
ns1.domain.local
admin.domain.local

www.domain.local

>Add  your findings to /etc/hosts

```bash - kali
$TARGET domain.local ns1.domain.local admin.domain.local www.domain.local
```

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
 
DNS Transfer
```
nslookup -type=any -query=axfr domain.com $IP
```




#### Gobuster
```bash - kali
gobuster dns -d domain.local -w /usr/share/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt 
```

If any more are found from gobuster, add also to /etc/hosts.


#### Manual
```
host www.megacorpone.com
```

```
host -t mx megacorpone.com
```

```
host -t txt megacorpone.com
```

#### DNS recon
```
dnsrecon -d megacorpone.com -t axfr
```

#### DNS enum
```
dnsenum megacorpone.com
```

```bash
dnsenum --enum domain.com -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -r
```


Subdomain brute forcing 
```bash 
dnsenum --dnsserver <nameserver> --enum -p 0 -s 0 -o found_subdomains.txt -f ~/subdomains.list <domain.tld>
```

#### nmap zone transfer
```
nmap --script=dns-zone-transfer -p 53 ns2.megacorpone.com
```

