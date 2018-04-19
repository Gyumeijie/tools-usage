# edit the root commit in git

- ### method1
>
```bash
# checkout the root commit
git checkout <sha1-of-root>

# amend the commit
git commit --amend

# rebase all the other commits in master onto the amended root
git rebase --onto HEAD HEAD master  

git rebase --onto <newbase> <since>...<till>
```

- ### method2
```bash
git rebase -i --root
```
