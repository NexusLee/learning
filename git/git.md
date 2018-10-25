1. #### git删除远程分支 ####
``` 
git push origin --delete {the_remote_branch}
```
2. #### git pull强制覆盖本地文件 ####
```
git fetch --all
git reset --hard origin/master
or 
git reset --hard origin/<branch_name>
```
3. #### git 查看远程分支
```
git remote -v
```
4. #### git 查看本地日志
```
git log
```
5. #### git 生成私钥和公钥
```
ssh-keygen -t rsa -C "email@company.com" -f ~/.ssh/id_rsa
```
6. #### git 回滚错误的合并
```
git revert -m 1 faulty merge
git checkout master //合并dev操作
git revert rev3
git merge dev 
```
