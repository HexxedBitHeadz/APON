#### Commands
```bash - kali
sudo nikto -h http://$TARGET:80
```
```bash - kali
sudo uniscan -qwedsu http://$TARGET:80
```
#### Proxy usage
```bash - kali
sudo proxychains nikto -h http://$TARGET:80
```
```bash - kali
sudo proxychains uniscan -qwedsu http://$TARGET:80
```
#### Nikto SSL Auth
```
sudo nikto -h http://$TARGET.com -id username:password -ssl
```