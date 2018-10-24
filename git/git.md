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
