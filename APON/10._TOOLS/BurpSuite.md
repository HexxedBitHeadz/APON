#### TCM Bug Bounty
Navigate to to azena.com with Burp proxy
Target tab > Site map > Scope settings > Check the Advanced Sope checkbox > Add
Protocal: Any
Host or IP range: `azena.com`
Port: *BLANK*
File: *BLANK*
This will auto include any sub-domains to azena.com
From here, we can simply navigate the website to populate Burp's Site map and potentially find more sub domains
OR
Crawling:
Right click entry in site map > Passively scan this host
Bad to enable right away, but it is possible to only intercept in-scope requests and responses:
Proxy Settings > Request intercept rules > check the box > Enable: `And URL Is in target scope` option
Proxy Settings > Response intercept rules > check the box > Enable: `And URL Is in target scope` option
To perform Directory Busting, send a request to intruder
`Get /$careers$ HTTP/2` > Sniper attack > Payload settings > add payload list
Review any .js findings for extra details / creds / api keys / etc
#### Android
Start with Burp Suite and emulated device open
Burp Suite > Proxy > Options > Proxy Listeners > Add > Binding > Bind to port: 8082 > All interfaces
Emulated device > `...` / `more button` > Settings > Uncheck `Use Android Studio HTTP proxy settings` > Click `Manual proxy configuration` > 127.0.0.1 > 8082 > Apply
Open browser on device > google.com > view certificate > Verify we see PortSwigger
We need to trust and import certificate
In Burp Suite > Proxy > Proxy Listeners > `Import / export CA certificate` > Export > Certificate in DER format > Next > Select file > XXX.CER > Save > Next
Find XXX.CER in file explorer, drag and drop into emulated Android device
Emulated Android device > Settings > Security > Credential storage > Install from SD card > Select XXX.CER file > Provide cert name > VPN and apps > OK > pin
Or push to physical device:
```
adb push C:\Users\$USER\Desktop\Burp.CER /sdcard/
```
In settings, search for certificate, find install CA certificate, locate and install the Burp.CER file
To test, enable intercept in Burp, open browser on device, visit google to view traffic in Burp intercept
#### iOS Safari
In Burp:
Proxy > Options > Proxy Listeners > Add > Binding > Port: 8082 > All Interfaces > Ok > Yes
In iPhone:
Settings > WiFi > Click WiFi network name > Configure Proxy > Manual > Enter MacBook IP address > Enter Port 8082 > Save
How to find MacBook IP:
```
ifconfig
```
Turn on Intercept in Burp, and load up Safari on the phone, visit http://burp:8082 > Click CA Certificate > Allow
Go back to Settings > General > Profile > PortSwigger CA > Install
Go back to Settings > About > Certificate Trust Settings > Enable PortSwigger CA
Now intercept will work within Burp
May / may not work with iOS apps
## Extenstions
https://www.reddit.com/r/hacking/comments/18eo1ur/whats_your_top_burp_suite_extensions_or_tips/
https://github.com/snoopysecurity/awesome-burp-extensions
https://www.betterhacker.com/2021/01/the-burp-extension-no-one-told-you-about.html
#### jython
[[6._Burp Extension]]
#### FREE
1. Agartha
	1. https://github.com/volkandindar/agartha
		1. Payload Generator
		2. Authorization Matrix
2. Param Miner
	1. https://github.com/PortSwigger/param-miner
		1. identifies hidden, unlinked parameters. It's particularly useful for finding web cache poisoning vulnerabilities.
3. Json Web Token
	1. https://github.com/portswigger/json-web-tokens
		1.
4. Autorize
	1. https://github.com/portswigger/autorize
5. Turbo Intruder
	1. https://github.com/portswigger/turbo-intruder
6. Content Type Convetor
	1. https://github.com/portswigger/content-type-converter
7. HTTP Request Smuggler
	1. https://github.com/portswigger/http-request-smuggler
8. Hackvector
	1. https://github.com/portswigger/hackvertor
9. Logger++
	1. https://github.com/portswigger/logger-plus-plus
### Paid
1. Burp Bounty Pro
	1. https://burpbounty.net/downloads/burpbountyprostripe/
2. Active Scan++
	1. https://github.com/portswigger/active-scan-plus-plus
3. Retire.js
	1. https://github.com/portswigger/retire-js
4. JS Miner
	1. https://github.com/portswigger/js-miner
5. J2EEScan
	1. https://github.com/portswigger/j2ee-scan
6. Collaborator Everywhere
	1. https://github.com/portswigger/collaborator-everywhere
7. 403 Bypasser
	1. https://github.com/portswigger/403-bypasser
8. JS Link Finder
	1. https://github.com/portswigger/js-link-finder
9. Software Vulnerability Scan
	1. https://github.com/portswigger/software-vulnerability-scanner
10. XSS Validator
	1. https://github.com/portswigger/xss-validator
