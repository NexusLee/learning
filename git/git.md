#### git删除远程分支 ####
``` 
git push origin --delete {the_remote_branch}
```
#### git pull强制覆盖本地文件 ####
```
git fetch --all
git reset --hard origin/master
git reset --hard origin/<branch_name>
```
