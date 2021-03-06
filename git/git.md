#### git新建远程分支
```shell
git checkout -b test
git push origin test{:name}
```
#### git检出远程分支
```shell
git pull origin test{:name}
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

#### 同步fork的项目
```shell
git remote -v 
git remote add upstream git@github.com:xxx/xxx.git
git fetch upstream
git merge upstream/master
```

#### git 关联远程分支
```shell
git branch --set-upstream-to=origin/<branch> release
```

#### git 删除大文件

```shell
git verify-pack -v .git/objects/pack/pack-*.idx | sort -k 3 -g | tail -5

git rev-list --objects --all | grep 35047899fd3b0dd637b0da2086e7a70fe27b1ccb

git log --pretty=oneline --branches --  huge.exe

git filter-branch --index-filter 'git rm --cached --ignore-unmatch huge.exe'

rm -rf .git/refs/original/
 
git reflog expire --expire=now --all
 
git fsck --full --unreachable
 
git repack -A -d
 
git gc --aggressive --prune=now
 
git push --force
```
