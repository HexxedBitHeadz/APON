### PHP Info File
Let's determine the location of the web root directory,
```
kali@kali:~$ curl http://$TARGET:45332/phpinfo.php | grep 'DOCUMENT_ROOT' | html2text
...
DOCUMENT_ROOT
C:/xampp/htdocs
...
```
we found the document root directory of the website (from the `phpinfo()` output) to be `C:/xampp/htdocs/`. Leveraging another vulnerability, we should be able to write a PHP web shell to that directory.
https://book.hacktricks.xyz/pentesting-web/file-inclusion#via-phpinfo-file_uploads-on
[[Medjed]]