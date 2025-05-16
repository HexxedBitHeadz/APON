### **Checks**

- [ ] Try default credentials "root":""
- [ ] Brute force credentials
- [ ] Check database content for new passwords
- [ ] Check version for exploits

## Dangerous Settings
|**Settings**|**Description**|
|---|---|
|`user`|Sets which user the MySQL service will run as.|
|`password`|Sets the password for the MySQL user.|
|`admin_address`|The IP address on which to listen for TCP/IP connections on the administrative network interface.|
|`debug`|This variable indicates the current debugging settings|
|`sql_warnings`|This variable controls whether single-row INSERT statements produce an information string if warnings occur.|
|`secure_file_priv`|This variable is used to limit the effect of data import and export operations.
Some of the commands we should remember and write down for working with MySQL databases are described below in the table.

| **Command**                                          | **Description**                                                                                       |
| ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `mysql -u <user> -p<password> -h <IP address>`       | Connect to the MySQL server. There should **not** be a space between the '-p' flag, and the password. |
| `show databases;`                                    | Show all databases.                                                                                   |
| `use <database>;`                                    | Select one of the existing databases.                                                                 |
| `show tables;`                                       | Show all available tables in the selected database.                                                   |
| `show columns from <table>;`                         | Show all columns in the selected database.                                                            |
| `select * from <table>;`                             | Show everything in the desired table.                                                                 |
| `select * from <table> where <column> = "<string>";` | Search for needed `string` in the desired table.                                                      |
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

| username | password |
| --- | --- |
| admin | 59f9ba27528694d9b3493dfde7709e70 |



#### Change password
```
update cms_users set password = (select md5(CONCAT(IFNULL((SELECT sitepref_value FROM cms_siteprefs WHERE sitepref_name = 'sitemask'),''),'admin'))) where username = 'admin';
```

**cms_siteprefs would be found under show tables;**

`cms_siteprefs`

or

```
echo -n 'admin' | md5sum
```

==21232f297a57a5a743894a0e4a801fc3==

```
update cms_users SET password='21232f297a57a5a743894a0e4a801fc3' WHERE username='admin';
```


| username | password |
| --- | --- |
| admin | 21232f297a57a5a743894a0e4a801fc3 |

#### MYSQL UDF 4.x/5.0
[https://www.adampalmer.me/iodigitalsec/2013/08/13/mysql-root-to-system-root-with-udf-for-windows-and-linux/](https://www.adampalmer.me/iodigitalsec/2013/08/13/mysql-root-to-system-root-with-udf-for-windows-and-linux/)

```bash - kali
nmap --script=mysql-brute <TARGET>
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
