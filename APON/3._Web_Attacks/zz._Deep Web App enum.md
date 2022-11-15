#### HTML
Tags:
https://www.w3schools.com/TAgs/default.asp

#### Web console commands
URL Encoding:
`encodeURIComponent("%");`
![[Pasted image 20220905123652.png]]

Current date in milliseconds since 1/1/1970
`Date.now()`
Coupon example:
`Date.now().toString(16)`

#### Parameter Enumeration
Think about what the parameter is representing.  
- A file?
	- `?page=` : [[3._LFI RFI]]
	- `?redirect?to=` : [[3._LFI RFI]]

- Something involving a DB?
	- `?id=` : SQLi / XSS
	- [[1_SQL Injection]]
	- [[7._XSS]]

==PAY ATTENTION TO DROP DOWN MENUS!==

![[Pasted image 20220902132417.png]]
![[Pasted image 20220902132438.png]]

- Settings / Search engine?
	- `?default=English` : [[7._XSS]]
	- `?q=Banana` :               [[7._XSS]]

- Comment field / Email field?
	- `Topic` or `Comment` : [[7._XSS]]
	
---
#### JavaScript (Angular)
Firefox  > Dev Tools > Sources > main.js
Enable pretty print
Search for known existing page (photo-wall)
Look for path: configurations:
![[Pasted image 20220905121939.png]]

Maybe use `wget` on this main.js file, then grep out results:
```bash - kali
grep "path:" main.js | tr -s " " | cut -d " " -f 3
```

#### Admin access without Auth header
`http://....../rest/user/whoami`
![[Pasted image 20220905130028.png]]

Remove Authorization header in repeater, send:

![[Pasted image 20220905130127.png]]
