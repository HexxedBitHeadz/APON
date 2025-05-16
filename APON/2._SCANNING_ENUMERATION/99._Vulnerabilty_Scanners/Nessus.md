https://www.tenable.com/downloads/nessus
#### Installing Nessus
```bash - kali
sudo apt install ./Nessus-X.X.X.deb
```
#### Starting Nessus after install
```bash - kali
sudo systemctl enable --now nessusd
```
or
```bash - kali
sudo systemctl start nessusd
```
```bash - kali
sudo systemctl status nessusd
```
```bash - kali
https://localhost:8834/#
```