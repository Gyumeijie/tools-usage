### #1 Edit the root commit in git

- #### Method1
```bash
# checkout the root commit
git checkout <sha1-of-root>

# amend the commit
git commit --amend

# rebase all the other commits in master onto the amended root
git rebase --onto HEAD HEAD master  

git rebase --onto <newbase> <since>...<till>
```
- #### Method2
```bash
git rebase -i --root
```

### #2 Create a new empty branch

1. #### Create a branch as an orphan:
```bash
git checkout --orphan <branchname>
```
2. #### Clear the working directory
```bash
git rm --cached -r .
```
> the option -r means allowing  recursive removal when a leading directory-name is given, another useful option is
--dry-run which means not actually removing the files, just show if they exist in the index.
3. #### Clean the untracked files or directories
```bash
git clean -ffdx [--dry-run]
```

### #3 Rename a local branch

- #### Rename a branch while pointed to any branch, do:
```bash
git branch -m <oldname> <newname>
```
- #### Rename the current branch, you can do:
```bash
git branch -m <newname>
```
- #### Rename the current branch to an existing branch, you can do:
```bash
git branch -M <newname>
```
given two branches named ***master*** and ***tmp***, and we are now in ***tmp*** branch, if we 
execute the command ```git branch -M master```, then the ***tmp*** becomes ***master***, and the old
***master*** branch is deleted.

> A way to remember this, is -m is for "move" (or mv), which is how you rename files.

### #4 Multiple users
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

### #5 Permission to User1/repo.git denied to User2
1. Run `ssh -vT git@github.com` to check which private key is being used
2. If it is the User2's, try add the following configuration to `~/.ssh/config`
```
Host github.com
  IdentityFile /path/to/your_ssh_id_rsa
```

### #6 Cherry-pick a range of commits
given a commits sequence of A, B, C, D and E, if we execute the following command, then the commit B and C 
will be applied to the current branch, and the commit A is exclusive.
```bash
  git cherry-pick A..C 
```
if we wanna have commit A be inclusive, we can write this:
```bash
  git cherry-pick A^..C 
```
### #7 Keep, but not track, a file
A common developer problem: the version that the developer works with locally may be customized in ways that are not 
intended to be visible upstream.
```bash
git update-index --assume-unchanged thefile
```
When you want to make a published change to the file, you can proceed via:
```bash
git update-index --no-assume-unchanged thefile
git add -p thefile
```

### #8 Relative Commmit Names
Git also provides mechanisms for identifying a commit relative to another reference, commonly the tip of a branch.

- The caret (^)
Within a single generation, the caret is used to select a different parent.
> For a commit can have multiple parent commits.
- The tilde (~)
The tilde is used to go back before an ancestral parent and select a preceding generation.


### #9 Diff the same file between two different commits
```bash
git diff [--options] <commit> <commit> [--] [<path>...]
```
> Note that the \<path\> is not exact the path of the file on your local system. 

### #10 Push all branch to remote
```
$ git push --all origin
```

### #11 any level of Wildcard to match any level of subdirectories:
With version 1.8.2 of git, you can also use the `**` wildcard to match any level of subdirectories:
```bash
**/__pycache__
```

### #12 checkout file from specific stash
```bash
git checkout stash@{0} -- `find . -name filename`

git stash show -p stash@{0} --name-only
```

### #13 rollback for not staged
```bash
git diff --name-only | xargs git checkout --
```

### #14 new-old 

```bash
DIR_PATH=$(pwd)"/new-old"
tmp_name=".difffiles"

if [ $# -ne 0 ];then
    DIR_PATH = $1;
fi
mkdir $DIR_PATH
mkdir -p $DIR_PATH"/new"
mkdir -p $DIR_PATH"/old"

git diff --cached --name-only > $tmp_name

git stash
cp --parents $(<$tmp_name) $DIR_PATH"/old"

git stash pop
cp --parents $(<$tmp_name) $DIR_PATH"/new"

rm -f $tmp_name
```

### #15 switch between branch

```bash
# current in master, and switch to branch_one
git checkout branch_one
# switch back to master
git checkout -
```

### #16 get head of specific branch

```bash
git rev-parse branch-name
```

### #17 get modified files in a commit

```bash
git diff-tree --no-commit-id --name-only -r xxx
```


### #18 add local repo as remote

```bash
 git remote add trunk /usr1/y00520193/project/trunk/xxx/.git
 
 git fetch trunk sync
 git checkout sync
```

### #19 checkout out remote branch
> 1. git branch -a (all); 2. git branch(local)
```bash
# remote branch
git branch -r

m/OpenHarmony-2.2-Beta2 -> origin/OpenHarmony-2.2-Beta2
origin/OpenHarmony-2.2-Beta2
origin/OpenHarmony-2.3-Beta
origin/OpenHarmony-v2.2-Beta
origin/backup/master
origin/master
origin/master_dy

git checkout origin/master
```

### #20 fetch a remote PR 
```bash
git fetch origin pull/$ID/head:$BRANCHNAME
```

where `$ID` is the pull request id and `$BRANCHNAME` is the name of the new branch that you want to create.
For instance, let's imagine you want to checkout pull request #2 from the origin main branch:
```bash
git fetch origin pull/2/head:MASTER

git fetch git@gitee.com:openharmony/utils_native.git pull/38/head:pr_38
```
