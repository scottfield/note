###查询repository的创建时间
```
https://api.github.com/repos/{owner}/{repository}
e.g.
https://api.github.com/repos/spring-cloud/spring-cloud-security
```

###configure ssh
```
#check whether exist ssh key
 ls -al ~/.ssh
#generate ssh key
 ssh-keygen -t rsa -b 4096 -C "scottfield@qq.com"
 #start ssh-agent
 eval $(ssh-agent -s)
 #add ssh key to ssh agent
 ssh-add ~/.ssh/id_rsa
 #copy ssh public ssh key into clipboard
 clip < ~/.ssh/id_rsa.pub
 #configure ssh in github settings
```
###switch repo from https to ssh
```
#change current working dir into your local repo
cd D:/workspace/note
#check current repo setting
git remote -v
#update current repo to use ssh
git remote set-url origin git@github.com:scottfield/note.git
#post check ssh setting wehther take effect
git remote -v
```
