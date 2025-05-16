Add "ad-" to the beginning of every line in a list of names
```
sed -i 's/^/rastalabs\\/g' names.txt
```
Convert `\n`'s to returns
```
echo "" | sed 's/\\n/\n/g'
```
