With this query you will find the name of all the types being used:
```sql
{__schema{types{name,fields{name}}}}
```
We are interested in "listusers" and "getOTP".
```sql
listUsers
```
```sql
getOTP(username:"peter")
```
With this query you can extract all the types, it's fields, and it's arguments (and the type of the args). This will be very useful to know how to query the database.
```sql
?query={__schema{types{name,fields{name, args{name,description,type{name, kind, ofType{name, kind}}}}}}}
```
It's interesting to know if the **errors** are going to be **shown** as they will contribute with useful **information.**
```sql
?query={__schema}
```
```sql
?query={}
```
```sql
?query={thisdefinitelydoesnotexist}
```
