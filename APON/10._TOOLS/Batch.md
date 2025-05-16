#### Network scanner
```
for /L %i in (1,1,255) do @ping -n 1 -w 200 x.x.x.%i > nul && e
cho 10.5.5.%i is up.
```
