#### awking specific column
```
| awk -F ':' '{print $2}'
```
#### Adding domain name in front of username list
```
cat ~/top-usernames-shortlist.txt | awk '{print "$DOMAIN_NAME\\" $1}' > ~/top-usernames-shortlist-CUSTOM.txt
```
