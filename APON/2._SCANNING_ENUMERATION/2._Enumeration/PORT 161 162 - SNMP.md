### Dangerous Settings

Some dangerous settings that the administrator can make with SNMP are:

|**Settings**|**Description**|
|---|---|
|`rwuser noauth`|Provides access to the full OID tree without authentication.|
|`rwcommunity <community string> <IPv4 address>`|Provides access to the full OID tree regardless of where the requests were sent from.|
|`rwcommunity6 <community string> <IPv6 address>`|Same access as with `rwcommunity` with the difference of using IPv6.|

```bash
cat /etc/snmp/snmpd.conf | grep -v "#" | sed -r '/^\s*$/d'
```

#### snmp-check
```
snmp-check $TARGET
```


```bash - kali
sudo apt install snmp-mibs-downloader
```

#### SNMPwalk


```bash - kali
snmpwalk -Os -c public -v 1 $TARGET
```

```shell-session
snmpwalk -v2c -c public $TARGET
```
 
 If output is needed 
```bash
snmpwalk -v1 -c public $TARGET >> snmp-output.txt
```

```
snmpwalk -v 2c -c public $TARGET  NET-SNMP-EXTEND-MIB::nsExtendOutputFull
```

Enumerating the Entire MIB Tree:
```bash - kali
snmpwalk -c public -v1 -t 10 $TARGET
```

Enumerating Windows Users
```bash - kali
snmpwalk -c public -v1 $TARGET 1.3.6.1.4.1.77.1.2.25
```

Enumerating Running Windows Processes
```bash - kali
snmpwalk -c public -v1 $TARGET 1.3.6.1.2.1.25.4.2.1.2
```

Enumerating Open TCP Ports
```bash - kali
snmpwalk -c public -v1 $TARGET 1.3.6.1.2.1.6.13.1.3
```

Enumerating Installed Software
```bash - kali
snmpwalk -c public -v1 $TARGET 1.3.6.1.2.1.25.6.3.1.2
```
Enumerating Installed Software and version
```bash - kali
snmpwalk -v 2c -c public $TARGET 1.3.6.1.2.1.1.5.0
```

#### onsixtyone single target
```bash - kali
onesixtyone $TARGET
```

```bash
onesixtyone -c /usr/share/seclists/Discovery/SNMP/snmp-onesixtyone.txt $TARGET
```

```bash
onesixtyone -c /usr/share/seclists/Discovery/SNMP/snmp.txt $TARGET
```

```bash
onesixtyone -c /usr/share/seclists/Discovery/SNMP/common-snmp-community-strings-onesixtyone.txt $TARGET
```

```bash
onesixtyone -c /usr/share/seclists/Discovery/SNMP/common-snmp-community-strings.txt $TARGET
```


#### onesixtyone range
```bash - kali
echo public > community
```

```bash - kali
echo private >> community
```

```bash - kali
echo manager >> community
```

```bash - kali
for ip in $(seq 1 254); do echo 10.11.1.$ip; done > ips
```

```bash - kali
onesixtyone -c community -i ips
```

### braa
To brute-force the individual OIDs and enumerate the information behind them.

```bash
sudo apt install braa
```

``` bash
braa <community string>@<IP>:.1.3.6.*   # Syntax
```

```bash
braa public@0.0.0.0:.1.3.6.*
```
