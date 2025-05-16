https://github.com/DragoQCC/HardHatC2
#### Installing .net 7 SDK
```
winget install Microsoft.DotNet.SDK.7
```
#### Server
close and reopen cmd, point to  `HardHatC2-master\HardHatC2-master\TeamServer`
```
dotnet run
```
Pay attention to output for password `HardHat_Admin's password is +!DP-AE#InnpV@d#6E#g`
#### Client
open cmd, point to `C:\Users\Slave\Downloads\HardHatC2-master\HardHatC2-master`
```
dotnet run
```
Open web browser (best with firefox?), visit
```
https://localhost:7096/
```
HardHat_Admin : +!DP-AE#InnpV@d#6E#g
Follow steps here https://docs.hardhat-c2.net/documentation/operators-and-authentication to finish setup.
TeamLead
Alice
AliceIsCool2023
Operator
Bob
BobIsCooler2023
Guest
Charlie
CharlieIsTheBest2023
Log in as an operator
#### Managers
HTTP & HTTPS bind to a port on the team server, while TCP and SMB only inform generated implants on how to connect back.
| Entry | CLIENT/SERVER | IP/PORT |
| --- | --- | --- |
| Connection Address | CLIENT | 192.168.19.131 |
| Connection Port | CLIENT | 7096 |
| Bind Address | SERVER | 192.168.19.131 |
| Bind Port | SERVER | 5000 |
#### Engineer
| Entry | Option |
| --- | --- |
| Manager Name | Select from drop down |
| Connection Attempts | 3 |
| Sleep Timer | 2 |
| Working Hours | as needed |
| Compile Type | exe |
| Sleep Encryption Type | Custom_RC4 |
Encode Shellcode with SGN?  no?.......
File found in: `HardHatC2-master\HardHatC2-master`
