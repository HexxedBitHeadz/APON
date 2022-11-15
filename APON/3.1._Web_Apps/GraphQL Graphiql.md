
![[Pasted image 20221108114319.png]]

With this query you will find the name of all the types being used:

```sql
{__schema{types{name,fields{name}}}}
```

![[Pasted image 20221108114352.png]]

We are interested in "listusers" and "getOTP".

```sql
listUsers
```

![[Pasted image 20221108114422.png]]

```sql
getOTP(username:"peter")
```

![[Pasted image 20221108114441.png]]
