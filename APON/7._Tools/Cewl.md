#### dirList password creator
Find words on pages at least 5 characters long.
```bash - kali
for url in $(cat dirList | grep -v ".png\|\.jpg\|\.js\|\.css\|\.gif\|\.svg\|\.ico" | cut -d "h" -f2-100 | sed "s/^/h/g"); do echo $url && cewl -m 5 -d 5 $url >> temp_cewl.txt;done
```
Sort / unique results, create list all lowercase as well (Remember `Nexus` vs `nexus`).  Be sure to try both when attacking.
```bash - kali
cat temp_cewl.txt | sort -u > cewlOrig.txt | tr '[:upper:]' '[:lower:]' > cewlLower.txt && rm temp_cewl.txt
```
#### Cewl password list
```bash - kali
cewl http://$TARGET -m 5 -w cewl-passwords.txt
```
Add 2 numeric characters to end of cewl-passwords.txt
```bash - kali
sudo mousepad /etc/john/john.conf
```
Find `[List.Rules:Wordlist]` section.
```bash - kali
# Add two numbers to the end of each password
$[0-9]$[0-9]
```
#### Mutate the cewl-password.txt file
```bash - kali
john --wordlist=cewl-password.txt --rules --stdout > mutated.txt
```
---
ULTIMATE WAY OF CREATING A WORDLIST
 1.DIRECTORY BRUTEFORCING
```bash - kali
feroxbuster -eknr --wordlist dir -u http://$TARGET/ -o ferox.txt
```
 2. PREPARE FIRST PART OF THE cewl.txt
```bash - kali
cat ferox.txt | grep 200 | grep -v "png\|\.js" | cut -d "h" -f2-100 | sed "s/^/h/g" >> urls.txt
```
```bash - kali
for url in $(cat urls.txt); do echo $url && cewl -m 6 -d 5 $url >> temp_cewl.txt;done
```
```bash - kali
cat temp_cewl.txt | sort -u >> cewl.txt && rm temp_cewl.txt
```
3. GO TO BURP AND SELECT ALL 200 NON STATIC SITES
![](https://miro.medium.com/max/700/1*ASIxVCxstUzAM6ogpK4Z1Q.png)
4. SEND THEM TO CO2-CEWLER, EXTRACT WORDS, SAVE OUTPUT cewl2.txt
PPM => EXTENSIONS => SEND TO CEWLER
![](https://miro.medium.com/max/700/1*3slzzVaZHKWDXrlcU3oLvA.png)
5. MERGE cewl2.txt with cewl.txt
```bash - kali
go install -v github.com/tomnomnom/anew@latest
```
```bash - kali
cat cewl2.txt | anew cewl.txt & rm cewl2.txt**
```