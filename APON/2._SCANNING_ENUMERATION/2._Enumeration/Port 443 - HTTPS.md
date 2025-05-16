#### Heartbleeed
```bash - kali
nmap -p 443 --script ssl-heartbleed $TARGET
```
```
sudo nikto -h http://$TARGET:443 -ssl
```
```
dirsearch -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://$TARGET:443 -o $PWD/dirsearch-MEDIUIM.txt -r
```
```bash - kali
curl https://$TARGET:443/ -k
```
```
ffuf -c -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt:FUZZ -u https://nunchucks.htb:443 -H "Host: FUZZ.nunchucks.htb"
```
```
ffuf -c -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt:FUZZ -u https://nunchucks.htb:443 -H "Host: FUZZ.nunchucks.htb" -fs 30589
```
```
gobuster vhost -u https://nunchucks.htb -w /usr/share/wordlists/dirbuster/directory-
list-2.3-medium.txt -k
```
