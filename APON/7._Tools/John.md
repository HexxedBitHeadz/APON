#### Unshadow
```bash - kali
sudo unshadow passwd-file.txt shadow-file.txt > unshadowed.txt
```
```bash - kali
sudo john --rules --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt
```
#### PDFCrack
```bash - kali
perl /usr/share/john/pdf2john.pl Infrastructure.pdf | tee pdf_hash
```
```bash - kali
john pdf_hash --wordlist=/usr/share/wordlists/rockyou.txt
```
#### Kirbi2john
```bash - kali
/usr/share/john/kirbi2john.py *.kirbi > kirbiHash
```
```bash - kali
john kirbiHash ––wordlist=wordlist.txt ––format=krb5tgs
```
#### rar2john
```bash - kali
rar2john flag.rar > hashes.txt
```
#### zip2john
```bash - kali
zip2john flag.zip > hashes.txt
```
#### Custom rule
```bash - kali
sudo mousepad /etc/john/john.conf
```
Example of appending 3 numeric values to existing wordlist.
```bash - kali
[List.Rules:append3nums]
$[0-9]$[0-9]$[0-9]
```
```bash - kali
john --wordlist=wordlist.txt --rules=append3nums hashes.txt
```
Example of appending 2 special characters to existing wordlist.
```bash - kali
[List.Rules:append2specials]
$[%^&*()_+\-={}|\[\]\\;':",./\<\>?`~]$[%^&*()_+\-={}|\[\]\\;':",./\<\>?`~]
```
```bash - kali
john --wordlist=wordlist.txt --rules=append2specials hashes.txt
```