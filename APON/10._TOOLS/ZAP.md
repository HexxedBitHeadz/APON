#### Installation
```bash - kali
sudo apt install zaproxy
```
[medium.com](https://medium.com/geekculture/%EF%B8%8Fstop-using-burp-suite-use-zap-fd68bf12d63e)
#### Rate Limiting
Tools > Options > Network > Rate Limit > Add
```
Description: Rate limit
Match String: example
Match Regex: X
Requets per Second: 3
Group by: Host
Enable: x
```
# 🕸️Stop Using Burp Suite, Use ZAP!⚡ - Geek Culture - Medium
---
Why use Burp Suite when OWASP ZAP _does it all*_ without the _paywall_. Everything you do in Burp Community can be done just as well in ZAP.
Nearly every [web application pentesting tutorial](https://www.google.com/search?q=web+app+pentesting+%22burp+suite%22) you’ll find online uses **Burp Suite Community** for demonstrations, but why is this? [Burp Suite is the most popular](https://trends.google.com/trends/explore?q=burp%20suite,OWASP%20ZAP), but every time I use it, I feel like I’m playing a free-to-play game where all the good stuff is behind a “membership”. There is a persistent feeling of _irritation_ in facing this paywall every time I use Burp.
Burp Suite has it’s vulnerability scanner and it’s fuzzing capabilities, among other things, behind a paywall of up to [**$400 USD per year**](https://portswigger.net/burp/pro)**.** This is beyond consideration for someone who is an aspiring security professional doing CTF’s and Boot2Root boxes.
Yet, it is **important to know how Burp Suite works** in case you end up in employment where the firm does have pro edition. *Also note Burp Suite does have features that OWASP ZAP doesn’t have like [Session Token Entropy Analysis, Comparison Feature, and a huge library of extensions.](https://allabouttesting.org/burp-suite-vs-owasp-zap-which-is-better/) So their are **somethings Burp has ZAP beat on**. However, for an independent web pentester, OWASP Zap is the overall better alternative to Burp Suite.
I’ll “translate” essential features you’re familiar with in Burp Suite to ZAP like:
Burp Suite -> ZAP
-   Proxy -> Requests/Response Editor
-   Intercept -> Break Points
-   Repeater -> Open/Resend Request Editor
-   Intruder -> Fuzz
-   Vulnerability Scanner -> “Attack”
## Proxy -> Requests/Response Editor
![](https://miro.medium.com/max/822/1*6obpkxmrJwM3dE7S_sZaxQ.png)
Clicking on the “Proxy” tab for Burp Suite brings you all the data of traffic being captured by Burp’s proxy, luckily you don’t have to set up the proxy on your own browser manually anymore(as you may see on a lot of guides and tutorials)thanks to the “Open Browser” feature.
![](https://miro.medium.com/max/913/1*_KD-Zn8xhMgRV-5xljww7A.png)
OWASP ZAP shares these nifty features too. Click on “Manual Explore” and “Launch Browser” to start capturing web traffic to the ZAP proxy without any configuration of your own browser.
![](https://miro.medium.com/max/836/1*F4jJ14StgRzWHC3CNgn-FQ.png)
The “HTTP history” of Burp Suite:
![](https://miro.medium.com/max/603/1*_xs27yYyMa3rVFi2-4y2tQ.png)
Shows up in the bottom left side of the ZAP interface in the “History” tab.
![](https://miro.medium.com/max/913/1*sVtEN1JzV7Oa0XH1QFvTCQ.png)
In Burp, you click on the HTTP history and request and response data shows up in the bottom:
![](https://miro.medium.com/max/913/1*bRAd4Cx_93RzM20ri7GPMQ.png)
In ZAP, it just shows up in the upper right!
![](https://miro.medium.com/max/913/1*TvTbQwKfFID52uGCeA2PGg.png)
## Intercept -> Break Points
In Burp, you can intercept HTTP requests before they are sent to a web server, allowing you to modify the request mid-transit. This is done by toggling “Intercept is off” to “Intercept is on”:
![](https://miro.medium.com/max/527/1*kgcTiGa3TdW94dxqVG970A.png)
Then sending a request with the browser:
![](https://miro.medium.com/max/762/1*nMsMnUQeadG3lQUxK8Sdwg.png)
Now in Burp you can modify the request in the “Intercept” tab:
![](https://miro.medium.com/max/655/1*y6fFc1EK_IuFoyb5WPgEVA.png)
After making modifications, you can “Forward” the request to the web server to complete it, or “Drop” the request and cancel the interception.
In ZAP, break points are the equivalent to intercepting in Burp. You turn on break points by clicking this little green button in the ZAP Browser
![](https://miro.medium.com/max/814/1*oReRKpprbB8UWl4vtwIugA.png)
Send a request, and a popup will give you information about the request you just intercepted, allowing you to edit the request and send it off.
![](https://miro.medium.com/max/892/1*KBibdUbRBI1F7Pd5YwHzcg.png)
## Repeater -> Open/Resend Request Editor
A very handy feature of Burp is to take any request and send it to “Repeater” to resend the request as many time as you want to the web server with modifications. This can be done by right clicking on any request panel and clicking “Send to Repeater”.
![](https://miro.medium.com/max/650/1*gySM5eQ486Bw0HqwCDuhdA.png)
Then in the “Repeater” tab, you can modify the request and send it off at will:
![](https://miro.medium.com/max/664/1*beWH0eEdTDUjFHCRiX6NrA.png)
In ZAP you can similarly right click any request but instead click on “Open/Resend with Request Editor…”:
![](https://miro.medium.com/max/891/1*3lA8gPqcdvMqt_ZtTfqJ_A.png)
This opens a window where you can edit request to modify and send repeatedly at will:
![](https://miro.medium.com/max/913/1*C_IJYcsq4OabxX4XXVX97w.png)
## Intruder -> Fuzz
In Burp Suite, spamming web requests to find interesting information about an application, AKA fuzzing, is part of the “Intruder” tab. For instance, if you’re trying to fuzz a login page, you’d right click the request and send it to Intruder:
![](https://miro.medium.com/max/913/1*OOHPalplzye2NJm9dp_Wtg.png)
You select where you want to fuzz in the request with the § characters. So to narrow down the fuzzing to the password and username fields, you configure Intruder like so and select Cluster Bomb to use multiple payload fields:
![](https://miro.medium.com/max/847/1*Qs0jEBzROwEkvDD-F5UTLw.png)
Click on the “Payloads Tab” and select file lists to fuzz on each payload:
![](https://miro.medium.com/max/550/1*m4i1HR6vKu6DuHbMtHYc3Q.png)
Once you click “Start Attack” you are met with the unfortunate relaxation you are behind a paywall and your fuzz requests are **heavily** throttled.
![](https://miro.medium.com/max/638/1*NsIOiMS6LKlSKFwuvPrJvA.png)
This throttling makes Burp Suite fuzzing **extremely slow and essentially unusable**, it’s only useful for demonstrating in tutorials like this one. Note if you still feel compelled to use Burp Suite Community after this post, [there is a add-on that is largely a bypass to this throttling and I encourage you to use it.](https://github.com/PortSwigger/turbo-intruder)
Enter ZAP, you can use their fuzzer without any throttling by right clicking any request and selecting “Fuzz…”:
![](https://miro.medium.com/max/913/1*i7yq3NQFt1zDtV4UQGnZyw.png)
Highlight parameters you wish to fuzz, click “Add…”:
![](https://miro.medium.com/max/913/1*LvYVaOrdV6cyKjOaWCjd5g.png)
Click add again to add a wordlist, you can select a file by clicking the “Type” drop down menu:
![](https://miro.medium.com/max/614/1*d1lJoW2KOcrbtE0_XRpmcA.png)
Repeat this with any other parameters you wish to fuzz and click “Start Fuzzer” to fire away, the results will show up under the “Fuzzer” tab:
![](https://miro.medium.com/max/913/1*caxMFNnEXa8A7Za-sSYINQ.png)
This fuzzer is useful for more things than just login pages, but can also be used to fuzz directories or input validation exploits and many other things
## Vulnerability Scanner -> “Attack”
I can’t really demonstrate the Burp Suite vulnerability scanner because in the community edition it is completely locked down, no throttling to even give you a hint of its capabilities. But you’d click “New Scan”:
![](https://miro.medium.com/max/913/1*_AvVzQGi6j9PjFN6lp6ENg.png)
In ZAP, the sites you are manually “spidering” will show up in the upper left hand side in a “Sites” window. Here you can also manipulate HTTP reqeusts, including selecting a website to run a vulnerability scan by right clicking the request -> “Attack” -> “Active Scan…”:
![](https://miro.medium.com/max/913/1*BlqstwC4Pm1N1ZO6M7izvA.png)
Then click “Start Scan”:
![](https://miro.medium.com/max/897/1*UAQZU6pWiC_SdxTJlhwvPw.png)
All the requests that result will show up in the “Active Scan” tab:
![](https://miro.medium.com/max/913/1*nUA2f5cfIVxKAIlGQnpQbQ.png)
Vulnerabilities found will popup under the “Alerts” tab:
![](https://miro.medium.com/max/785/1*f52ixU7dbzS3X-z0I8Wh-Q.png)
OWASP ZAP is a great web app testing suite and should definitely be used more commonly than Burp Suite Community. There just seems to be a lack of documentation and tutorials about ZAP compared to Burp. I hope to have helped bridge that gap with this post and have taught you how to transfer your web pentesting skills from Burp to ZAP.
