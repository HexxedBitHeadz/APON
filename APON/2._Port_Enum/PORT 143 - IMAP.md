#### IMAP Commands

|**Command**|**Description**|
|---|---|
|`1 LOGIN username password`|User's login.|
|`1 LIST "" *`|Lists all directories.|
|`1 CREATE "INBOX"`|Creates a mailbox with a specified name.|
|`1 DELETE "INBOX"`|Deletes a mailbox.|
|`1 RENAME "ToRead" "Important"`|Renames a mailbox.|
|`1 LSUB "" *`|Returns a subset of names from the set of names that the User has declared as being `active` or `subscribed`.|
|`1 SELECT INBOX`|Selects a mailbox so that messages in the mailbox can be accessed.|
|`1 UNSELECT INBOX`|Exits the selected mailbox.|
|`1 FETCH <ID> all`|Retrieves data associated with a message in the mailbox.|
|`1 CLOSE`|Removes all messages with the `Deleted` flag set.|
|`1 LOGOUT`|Closes the connection with the IMAP server.|

#### OpenSSL - TLS Encrypted Interaction IMAP
```
openssl s_client -connect $TARGET:imaps

```

If you are able to connect using openssl type the following commands to login and read Inbox:
```
a001 LOGIN username password
```
Once Logged in type the following to list the content
```
a002 LIST "" *
```

If you find a the inbox use this command to access it"
```
a003 select INBOX
```

If there is an email that exist run the following command to display the content:
```
a004 FETCH 1 BODY.PEEK[]
```


```shell-session
curl -k 'imaps://$TARGET' --user username:pasword -v
```

This example will show with existing found creds, jonas : SicMundusCreatusEst
#### Reading emails
```bash - kali
nc $TARGET 143
```

```bash - kali
tag login jonas@localhost SicMundusCreatusEst
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

```
sendemail -f 'jonas@localhost' \
                       -t 'mailadmin@localhost' \
                       -s $TARGET:25 \
                       -u 'Your spreadsheet' \
                       -m 'Here is your requested spreadsheet' \
                       -a calc.ods
```




