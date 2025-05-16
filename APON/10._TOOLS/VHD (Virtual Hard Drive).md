```bash - kali
sudo apt install libguestfs-tools
```
```bash - kali
mkdir mnt2
```
```bash - kali
guestmount --add ./mnt/WindowsImageBackup/L4mpje-PC/Backup\ 2019-02-22\ 124351/9b9cfbc4-369e-11e9-a17c-806e6f6e6963.vhd --inspector --ro ./mnt2/
```
Try dumping hashes with [[6._Dumping Hashes with Secretsdump.py#Locally with secretsdump py]]
