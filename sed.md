##### #1 dot match all

```
All you need to use is a -z option:
```

##### #2 remove the first line

```
sed -i '1!b;/^$/d' file
```
