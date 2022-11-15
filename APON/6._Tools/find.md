#### History hunting
```bash - target
find / -iname .bash_history 2>/dev/null
```

#### Hunting for config files.
```bash - target
find / -iname *config* 2> /dev/null
```

```bash - target
find / -iname *conf* 2> /dev/null
```

```bash - target
find / -iname *.cnf 2> /dev/null
```

Hunting for config files that contain 'password'
```bash - target
find / -iname '*config*' -exec grep -rli 'password' {} \; 2> /dev/null
```

Hunting for config php files that contain 'password'
```bash - target
find / -iname '*config*.php' -exec grep -rli 'password' {} \; 2> /dev/null
```

```bash - target
find / -iname '*config*.php' -exec grep -rli 'DBPASS' {} \; 2> /dev/null
```

Find files by group (network group in example):
```bash - target
find / -xdev -group network 2>/dev/null
```

#### whereis

```bash - target
whereis phpmyadmin
```


#### Find local.txt file
```bash - target
find / -iname local.txt 2> /dev/null
```
