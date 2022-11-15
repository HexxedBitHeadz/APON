####  Manual
```bash - kali
sudo nmap -p- -Pn -vvv $TARGET -Pn
```

```bash - kali
sudo nmap -sVC -p- -Pn -vvv $TARGET  -Pn
```

```bash - kali
sudo nmap -vvv --reason -Pn -T4 -sV -sC --version-all -A --osscan-guess -p- -oN full_tcp_nmap.txt $TARGET -Pn
```

#### Script scans
---
nmap Vuln Scanner
```bash - kali
sudo nmap --script=vuln -Pn $TARGET -Pn
```
---
```bash - kali
sudo nmap --script=ftp* -p 21 $TARGET -Pn
```

```bash - kali
sudo nmap --script=ssh* -p 22 $TARGET -Pn
```

```bash - kali
sudo nmap --script=telnet* -p 23 $TARGET -Pn
```

```bash - kali
sudo nmap --script=smtp* -p 25 $TARGET -Pn
```

```bash - kali
sudo nmap --script=http* -p 80 $TARGET -Pn
```

```bash - kali
sudo nmap --script=pop3* -p 110 $TARGET -Pn
```

```bash - kali
sudo nmap --script=rpc* -p 111 $TARGET -Pn
```

```bash - kali
sudo nmap --script=rpc* -p 135 $TARGET -Pn
```

```bash - kali
sudo nmap --script=imap* -p 143 $TARGET -Pn
```

```bash - kali
sudo nmap --script=smb-vuln* -p 445 $TARGET -Pn
```

```bash - kali
sudo nmap --script=ms-sql* -p 1433 $TARGET -Pn
```

```bash - kali
sudo nmap --script=oracle* -p 1521 $TARGET -Pn
```

```bash - kali
sudo nmap --script=nfs* -p 2049 $TARGET -Pn
```

```bash - kali
sudo nmap --script=docker* -p 2375 $TARGET -Pn
```

```bash - kali
sudo nmap --script=mysql* -p 3306 $TARGET -Pn
```

```bash - kali
sudo nmap --script=rdp* -p 3389 $TARGET -Pn
```

```bash - kali
sudo nmap --script=vnc* -p 5900 $TARGET -Pn
```


- [ ] Review OpenPorts for any UDP ports.
####  UDP scan
```bash - kali
nmap -A -sV -sC -sU $TARGET --script=*enum --top-ports 20  -Pn
```

#### nmap script
```bash - kali
mousepad nmap.sh
```

```bash - kali
#!/bin/bash

TARGET=$1
USER=$USER

SCRIPT_DIR=$( cd -- "$( dirname -- "${BASH_SOURCE[0]}" )" &> /dev/null && pwd )

echo $SCRIPT_DIR


spin()
{
  spinner="/|\\-/|\\-"
  while :
  do
    for i in `seq 0 7`
    do
      echo -n "${spinner:$i:1}"
      echo -en "\010"
      sleep 1
    done
  done
}

echo "---------------------------------------------------"
echo "Fly like a T4!  |  TARGET =" $TARGET
echo "---------------------------------------------------"
echo "Let's start with a sneak peek..."
echo "---------------------------------------------------"

# Start the Spinner:
spin &
# Make a note of its Process ID (PID):
SPIN_PID=$!
# Kill the spinner on any signal, including our own exit.
trap "kill -9 $SPIN_PID" `seq 0 15`

######################################


sudo nmap -T4 $TARGET -Pn -vvv | grep "open" | column -t | grep -v "Discovered"

echo "---------------------------------------------------"
echo "Now we look into all TCP ports..."
echo "---------------------------------------------------"

sudo nmap -T4 $TARGET -Pn -p- | grep "open" | column -t | cut -d '/' -f 1 | grep -v "Discovered" > OpenPorts


echo "Found the following ports!"
echo "---------------------------------------------------"
cat OpenPorts

echo "---------------------------------------------------"
echo "Scanning for services on found ports..."
#sudo nmap -sVC $TARGET -Pn -p $(tr '\n' , < OpenPorts) > nmapSVC

sudo nmap -A $TARGET -Pn -p $(tr '\n' , < OpenPorts) > nmapSVC


########################

if grep -q "135" OpenPorts; then
	bash $SCRIPT_DIR/PortScanners/RPC/RPC.sh $TARGET & 
fi

if grep -q "139" OpenPorts; then
	bash $SCRIPT_DIR/PortScanners/SMB/SMB_139.sh $TARGET & 
fi

if grep -q "445" OpenPorts; then
	bash $SCRIPT_DIR/PortScanners/SMB/SMB_445.sh $TARGET & 
fi

########################


# Awk command to spit out just the Service names. 
cat nmapSVC | awk '/open/{print $3}' | grep -v results > Services

echo "---------------------------------------------------"
echo "Here's what we found!"
echo "---------------------------------------------------"

cat nmapSVC

echo "---------------------------------------------------"
echo "Checking some UDP ports..."
echo "---------------------------------------------------"
echo "---------------------------------------------------" >> nmapSVC
echo "UDP PORTS >>>" >> nmapSVC
echo "---------------------------------------------------" >> nmapSVC
nmap -A -sV -sC -sU $TARGET --script=*enum --top-ports 20 >> nmapSVC

#sudo nmap -T4 --top-ports 20 $TARGET -Pn -sUV | grep "open" | column -t | cut -d '/' -f 1 | grep -v "Discovered" >> OpenPorts
echo "---------------------------------------------------"
echo "Finished!"
######################################

# If the script is going to exit here, there is nothing to do.
# The trap above will kill the spinner when this script exits.
# Otherwise, if the script is going to do more stuff, you can
# kill the spinner now:
kill -9 $SPIN_PID

```

```bash - kali
chmod +x nmap.sh && sudo ./nmap.sh $TARGET
```

#### AllIn1
```bash - kali
sudo nmap -T4 $TARGET -Pn -p- | grep "open" | awk '{print $1}' | column -t | cut -d '/' -f 1 > PortTest && sudo nmap -sVC $TARGET -Pn -p $(tr '\n' , < PortTest) > nmapSVC
```