
Base64 encode each line of file:
```bash - kali
while read line; do echo -n -i $line | base64 >> outputfile.txt; done < /usr/share/seclists/Passwords/Common-Credentials/best15.txt
```