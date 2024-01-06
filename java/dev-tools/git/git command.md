
##get help information
```
git <commandname> --help
```

##Setting your username in Git
- Setting your Git username for every repository on your computer
```bash
$ git config --global user.name "jackiew"
```
check the configuration
```bash
$ git config --global user.name
```

- Setting your Git username for a single repository

Change the current working directory to the local repository where you want to configure the name that is associated with your Git commits.
```bash
$ git config  user.name "jackiew"
```
check the configuration
```bash
$ git config  user.name
```
##create a new repository on the command line
```
echo "# book" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/scottfield/book.git
git push -u origin master
```
##push an existing repository from the command line
```
git remote add origin https://github.com/scottfield/book.git
git push -u origin master
```
##pull unrelated history from remote repo
```
git pull origin master --allow-unrelated-histories
```
##undo current commit
```
git reset --soft HEAD^
```
##give up uncommitted changes to file
```
git rm --cached -f -- src/main/gui/src/routes/IndexPage.js
git checkout HEAD -- src/main/gui/src/routes/IndexPage.js
  or
git checkout path/to/file
```
##give up all local changes and remove untracked  directories and files
```
git checkout . && git clean -xdf
```

##remember password
```
git config --global credential.helper wincred
```

##clone huge repository(shallow clone)
- First, turn off compression:

```
git config --global core.compression 0
```
- Next, let's do a partial clone to truncate the amount of info coming down:

```
git clone --depth 1 <repo_URI>
```
- When that works, go into the new directory and retrieve the rest of the clone:

```
git fetch --unshallow 
or, alternately,
git fetch --depth=2147483647
```
- Now, do a regular pull:
```
git pull --all
```

-use patch to share code change
```
step 1 create a patch file to store code changes
git diff > mypatch.txt
step 2 use apply command to import code changes from patch file
git apply mypatch.txt
```

### backfill history after shallow clone
```
backfill all history:
git pull --unshallow
backfill some history:
git fetch --depth=100

```
###how to clear commit history for a branch

```
Checkout

git checkout --orphan latest_branch

Add all the files

git add -A

Commit the changes

git commit -am "commit message"

Delete the branch

git branch -D master

Rename the current branch to master

git branch -m master

Finally, force update your repository

git push -f origin master
```
###how to squeeze commits
- commandline method:
```
git rebase -i <commit_hash>
//edit as playbook mark first commit as pick and mark the remaining as s,looks like the following,
pick 56bcce7 Closes #2774
s e43ceba Lint.py: Replace deprecated link

git rebase --continue

//edit the commit message, and save the changes

```
- use intellij squeeze commits git UI to quickly merge all commits.

###how to check files change history
```
 git log -- filepath

```
