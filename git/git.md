#### git新建远程分支
``` 
git checkout -b test
git push origin test{:name}
```

#### git删除远程分支
``` 
git push origin --delete {the_remote_branch}
```
#### git pull强制覆盖本地文件
```
git fetch --all
git reset --hard origin/master
or 
git reset --hard origin/<branch_name>
```
#### git 查看远程分支
```
git remote -v
```
#### git 查看本地日志
```
git log
```
#### git 生成私钥和公钥
```
ssh-keygen -t rsa -C "email@company.com" -f ~/.ssh/id_rsa
```
#### git 回滚错误的合并
```
git revert -m 1 faulty merge
git checkout master //合并dev操作
git revert rev3
git merge dev 
```
#### git 恢复未存入暂存区文件
```
git checkout -- filename
```

#### git rebase
```
git rebase master
git rebase master topic

          A---B---C topic
         /
    D---E---F---G master
    
    变成
                  A'--B'--C' topic
                 /
    D---E---F---G master
```

#### stash message
```
git stash push -m "message"
```
