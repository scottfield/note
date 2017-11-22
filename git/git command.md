
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
##undo current commit
```
git reset --soft HEAD^
```
##undo uncommitted file
```
git checkout path/to/file
```