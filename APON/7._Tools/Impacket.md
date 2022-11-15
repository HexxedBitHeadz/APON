#### Impacket for Windows
```
https://github.com/ropnop/impacket_static_binaries/releases/tag/0.9.21-dev-binaries
```

#### Latest Version
```bash - kali
sudo pip3 uninstall impacket
```

```bash - kali
sudo git clone https://github.com/cube0x0/impacket
```

```bash - kali
cd impacket
```

```bash - kali
sudo python3 ./setup.py install
```

#### Older version
```bash - kali
sudo git clone https://github.com/SecureAuthCorp/impacket
```

#### psexec.py
```bash - kali
python3 psexec.py $USER:$PASSWORD@$TARGET
```

#### Get-GPPPassword
```bash - kali
impacket-Get-GPPPassword $DOMAIN/$USER:$PASSWORD@$TARGET
```