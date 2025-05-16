#### Feroxbuster
Run with `-n` for non recursive, get a layout idea.
Run with `-k` for https.
```bash - kali
feroxbuster -u http://$TARGET:80 -t 5 -L 5 -q -w /usr/share/wordlists/dirb/common.txt -n
```
Then start running recursively, outputting to file(s).
```bash - kali
feroxbuster -u http://$TARGET:80 -t 5 -L 5 -q -w /usr/share/wordlists/dirb/common.txt -o feroxbuster-COMMON.txt --extract-links
```
```bash - kali
feroxbuster -u http://$TARGET:80 -t 5 -L 5 -q -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o feroxbuster-MEDIUM.txt --extract-links
```
How to add authentication?
add headers:
```bash - kali
-H Accept:application/json "Authorization: Bearer {token}"
```
