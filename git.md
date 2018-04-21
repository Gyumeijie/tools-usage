# edit the root commit in git

- ### method1
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

# create a new empty branch

1. ### create a branch as an orphan:
```bash
git checkout --orphan <branchname>
```
2. ### clear the working directory
```bash
git rm --cached -r .
```
> the option -r means allowing  recursive removal when a leading directory-name is given, another useful option is
--dry-run which means not actually removing the files, just show if they exist in the index.


# rename a local branch

- ### rename a branch while pointed to any branch, do:
```bash
git branch -m <oldname> <newname>
```
- ###  rename the current branch, you can do:
```bash
git branch -m <newname>
```
> A way to remember this, is -m is for "move" (or mv), which is how you rename files.

# multi users
given an scenario where we have local git configured with:
 ```bash
 git config --global user.email user2@example.com
 ```
and when we wanna push the master branch to the remote, we then use **user1 account**, so each of these commits will have a tip which takes the form of: 
``` 
user1 authored and user2 committed 
```
otherwise, if the author is just the user who commit, we would have a tip like this:
```
user1 authored and user1 committed 
```