#### showmount
```bash - kali
showmount -e $TARGET
```
#### Null user enumeration
```bash - kali
rpcclient -U "" -N $TARGET
```
```bash - kali
rpcclient -p 135 -U "" $TARGET
```
```bash - kali
rpcclient -W '' -c querydispinfo -U''%'' '$TARGET'
```
#### rpcmap
```bash - kali
rpcmap.py 'ncacn_ip_tcp:$TARGET' | grep A2 'DCOM'
```
```bash - kali
rpcmap.py 'ncacn_ip_tcp:$TARGET' -brute-opnums -auth-level 1 -opnum-max 5
```
See [[APT.pdf]] for further steps.
#### rpcclient Enumeration
[[Spray]]
```bash - kali
rpcclient -U $USER $TARGET
```

```bash - kali
rpcclient -U "" $TARGET
```

```bash - kali
help
```

```bash - kali
srvinfo
```

```bash - kali
enumdomains
```

```bash - kali
enumdomusers
```

```bash - kali
querydominfo
```

```bash - kali
netshareenumall
```

#### Rpcclient - User & Group  Enumeration
```bash - kali
enumdomusers
```

```bash - kali
queryuser $rid_value
```

Example: 
```bash - kali
pcclient $> enumdomusers
user:[admin] rid:[0x9e8]

rpcclient $> queryuser 0x9e8

```

The ```queryuser ``` command can yield a group's RID information to get this info run:
```bash - kali
querygroup $rid_value
```

Brute Forcing User RIDs
```
for i in $(seq 500 1100);do rpcclient -N -U "" $TARGET -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "";done
```

##### Creating a list of valid usernames retrieved from RPC
```bash - kali
cat users.txt | awk -F\[ '{print $2}' | awk -F \] '{print $1}' > valid_users.txt
```
#### rpcclient.sh
```bash - kali
for u in $(cat users | awk -F@ '{print $1}' | awk -F: '{print $2}');
do
	rpcclient -U "$u%Welcome123!" -c "getusername;quit" $TARGET | grep Authority;
done
```
`Account Name: melanie, Authority Name: MEGABANK`
```bash - kali
impacket-rpcdump
```
