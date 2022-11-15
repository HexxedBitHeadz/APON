#### Network scanner
```command prompt - target
for /L %i in (1,1,255) do @ping -n 1 -w 200 xxx.xxx.xxx.%i > nul && e
cho xxx.xxx.xxx.%i is up.
```