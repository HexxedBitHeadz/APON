```bash - kali
git clone https://github.com/lanjelot/patator && cd patator
```

#### Blind SQL injection
[[1.7_Blind SQLi]]

#### Fuzz Get Request
```bash - kali
python3 patator.py http_fuzz method=GET url="http://$TARGET/ajax.php?fun=login&username=FILE0&password=test" 0=users.txt -x ignore:fgrep='invalid user'
```

#### Fuzz Post Request
```bash - kali
python3 patator.py http_fuzz url=http://$TARGET/phpmyadmin/index.php method=POST body='pma_username=root&pma_password=FILE0&server=1&lang=en' 0=passwords.txt follow=1 accept_cookie=1 -x ignore:fgrep='Cannot log in to the MySQL server'
```

#### Attack from Burp request
Place in your FILE placeholders where necessary.  Below, we see in the password field.

![[Pasted image 20220318104320.png]]

Right click > copy to file > "copy to file" as text file.




