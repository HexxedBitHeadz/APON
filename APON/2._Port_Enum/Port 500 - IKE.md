https://book.hacktricks.xyz/pentesting/ipsec-ike-vpn-pentesting

```bash - kali
ike-scan -M $TARGET
```

![[Pasted image 20220125181008.png | 1200]]

![[Pasted image 20220125182150.png | 1200]]

```bash - kali
echo -n 9C8B1A372B1878851BE2C097031B6E43 | wc -c
```

![[Pasted image 20220125182347.png | 1200]]

```bash - kali
sudo apt install strongswan -y
```

```bash - kali
echo '$TARGET : PSK "Dudecake1!"' >> /etc/ipsec.secrets
```

![[Pasted image 20220125182910.png | 1200]]

```bash - kali
sudo mousepad /etc/ipsec.conf
```

```bash - kali
conn Conceal
	type=transport
	keyexchange=ikev1
	right=$TARGET
	authby=psk
	rightprotoport=tcp
	leftprotoport=tcp
	esp=3des-sha1
	ike=3des-sha1-modp1024
	auto=start
```

```bash - kali
sudo ipsec stop
```

```bash - kali
sudo ipsec start --nofork
```

```bash - kali
nmap -p- -sT $TARGET
```

---

```bash - kali
for ENC in 1 2 3 4 5 6 7/128 7/192 7/256 8; do for HASH in 1 2 3 4 5 6; do for AUTH in 1 2 3 4 5 6 7 8 64221 64222 64223 64224 65001 65002 65003 65004 65005 65006 65007 65008 65009 65010; do for GROUP in 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18; do echo "--trans=$ENC,$HASH,$AUTH,$GROUP" >> ike-dict.txt ;done ;done ;done ;done
```

And then brute-force each one using ike-scan (this can take several minutes):

```bash - kali
while read line; do (echo "Valid trans found: $line" && sudo ike-scan -M $line $TARGET) | grep -B14 "1 returned handshake" | grep "Valid trans found" ; done < ike-dict.txt
```

If the brute-force didn't work, maybe the server is responding without handshakes even to valid transforms. Then, you could try the same brute-force but using aggressive mode:

```bash - kali
while read line; do (echo "Valid trans found: $line" && ike-scan -M --aggressive -P handshake.txt $line $TARGET) | grep -B7 "SA=" | grep "Valid trans found" ; done < ike-dict.txt
```

Hopefully a valid transformation is echoed back. You can try the same attack using https://github.com/isaudits/scripts/blob/master/iker.py

ou could also try to brute force transformations with https://github.com/SpiderLabs/ikeforce

```bash - kali
./ikeforce.py $TARGET # No parameters are required for scan -h for additional help
```
