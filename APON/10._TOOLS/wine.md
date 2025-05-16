#### Wine installation
```
sudo apt install wine
```
#### Wine32 package install
```
sudo dpkg --add-architecture i386 && sudo apt-get update && sudo apt-get install wine32
```
#### error wine mono not installed
1:
```
sudo apt-get install mono-complete
```
2:
```
sudo apt-get install winetricks
```
```
winetricks dotnet461
```
3:
Download [wine-mono.msi](https://dl.winehq.org/wine/wine-mono/) from the official WineHQ site (version 7.4.0 at the time of writing this).
```
wine msiexec /i wine-mono-7.4.0-x86.msi
```
#### error wine: could not load kernel32.dll, status c0000135
```
`rm -r ~/.wine`
```
Try running wine again
