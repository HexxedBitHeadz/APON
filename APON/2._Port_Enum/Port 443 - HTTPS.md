#### Heartbleeed
```bash - kali
nmap -p 443 --script ssl-heartbleed $TARGET
```

```bash - kali
curl https://$TARGET:443/ -k
```

