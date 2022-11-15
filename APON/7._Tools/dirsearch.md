#### Quickstart

recursive, extensions, include status codes, follow redirects - options to append to commands below:
` -r -e sh,txt,htm,php,cgi,html,pl,bak,old,asp,aspx -i 200,302 `

Quick common search:
```bash - kali
dirsearch -w /usr/share/wordlists/dirb/common.txt -u http://$TARGET:80 -o $PWD/dirsearch-COMMON.txt -r
```

Longer list search:
```bash - kali
dirsearch -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://$TARGET:80 -o $PWD/dirsearch-MEDIUIM.txt -r
```

Web Quick Hits:
```bash - kali
dirsearch -w /usr/share/seclists/Discovery/Web-Content/quickhits.txt -u http://$TARGET:80 -o $PWD/dirsearch-WebQuickHits.txt -r
```

How to add authentication?


add headers:

` -H "Cookie: connect.sid=s%3A2eEH6hm37SX13aaVlDfG_Pb6nqbplZe6.yQVdodM9I3Xae4TZ9XgNtbuFe3toKo1I5LM5HOiJfbo" `

exclude response size:

` --exclude-sizes=5kb `


#### Proxy usage
Be sure to set the port to whatever you set it to in chisel!
```bash - kali
proxychains dirsearch -w /usr/share/wordlists/dirb/common.txt -u http://$TARGET:80
```

Double check against dirb!
```bash - kali
proxychains dirb http://$TARGET /usr/share/wordlists/dirb/common.txt -w -X .asp,.aspx,.cgi,.htm,.html,.jsp,.php
```
