#### git新建远程分支
```shell
git checkout -b test
git push origin test{:name}
```

#### git删除远程分支
``` shell
git push origin --delete {the_remote_branch}
```
#### git pull强制覆盖本地文件
```shell
git fetch --all
git reset --hard origin/master
or 
git reset --hard origin/<branch_name>
```
#### git 查看远程分支
```shell
git remote -v
```
#### git 查看本地日志
```shell
git log
```
#### git 生成私钥和公钥
```shell
ssh-keygen -t rsa -C "email@company.com" -f ~/.ssh/id_rsa
```
#### git 回滚错误的合并
```shell
git revert -m 1 faulty merge
git checkout master //合并dev操作
git revert rev3
git merge dev 
```
#### git 恢复未存入暂存区文件
```shell
git checkout -- filename
```

#### git rebase
```shell
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
```shell
git stash push -m "message"
```
