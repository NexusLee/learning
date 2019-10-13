## Linux

#### 1. 根据时间查看日志

```shell
grep "2014-01-01 21:" log.txt; tail -f log.txt

or

awk '/2014-01-01 21:/' log.txt; tail -f log.txt
```

#### 2. 切回上次目录
```shell
cd -
```

#### 3. centos7 开放端口
```shell
firewall-cmd --zone=public --add-port=80/tcp --permanent     //开放端口
firewall-cmd --reload                                        //重启防火墙
```

#### 4. centos7 关闭端口
```shell
firewall-cmd --zone=public --remove-port=80/tcp --permanent  //开放端口
firewall-cmd --reload                                        //重启防火墙
```
#### 5. 清空日志的几种方式
```shell
echo " " > test.log
> test.log
cat /dev/null > test.log
```

#### 6. 发送1次 icmp echo_request
```shell
ping -c 1
```

#### 7. 查看路由表
```shell
ip r
```

#### 8. 根据端口号查看PID
```shell
lsof -i:8080
```

#### 9. 根据PID查看进程信息
```shell
ll /proc/pid
```

#### 10. kcptun 重启
```shell
supervisorctl restart kcptun
```

#### 11. 查看memcache信息
```shell
telnet 127.0.0.1 11211
stats
ctrl+], 按q结束进程。
```

#### 12. 设置权限
```shell
chown -R user:group file
```

#### 13. 快速查找大日志文件内容(less、vim均可)
```shell
grep -n '日志' * （日志过大 grep: memory exhausted）

切割出日志 grep -n '2019-07-09 07:10:09' log.out > temp.out （日志过大 grep: memory exhausted）

head -n k file | tail -n m

$ sed -n '/2019-07-09 07:10:09/,/2019-07-09 07:10:10/p' server.out2019-07-09.log > temp.log （日志过大 sed: couldn't re-allocate memory）

$ time (head -50000000 file | tail -10) > /dev/null
real    0m0.694s
user    0m0.830s
sys     0m0.333s

$ time (sed -n '49999991,50000000p' file) > /dev/null
real    0m6.018s
user    0m5.863s
sys     0m0.160s

$ time (sed -n '50000000q;49999991,50000000p' file) > /dev/null
real    0m3.197s
user    0m3.153s
sys     0m0.043s

$ time (awk 'NR>=49999991 && NR<=50000000' file) > /dev/null
real    0m12.665s
user    0m12.543s
sys     0m0.123s

$ time (awk 'NR>=49999991 && NR<=50000000{print} NR==50000001{exit}' file)
real    0m9.104s
user    0m9.010s
sys     0m0.100s
```

#### 14. 查看文件大小(sparse file)

```shell
  $ ls -l file
  -rw-r--r--  1 myself wheel  536870912 Apr  8 11:44 file

  $ ls -lh file
  -rw-r--r--  1 myself wheel   512M Apr  8 11:44 file

  $ du -h file //实际大小
  24K    file

  $ du -B 1 file
  24576   file

  $ ls -s --block-size=1 file
  24576 file
```

#### 15. 检测https

```shell
curl -k -3 http://localhost:8443 | od -A n -t x1
```

#### 16. 查看tcp端口连接数

```shell
netstat -nat|grep -i "17001"|wc -l
```

#### 17. 用文件作为swap

```shell
 1. 创建文件块大小（1G）

    #  dd if=/dev/zero of=/tmp/swap bs=1M count=1024

 2. 格式化为swap

    #  mkswap /tmp/swap

 3. 启用swap

    # swapon /tmp/swap

 4. 添加到系统自动挂载（同上）

    # vim /etc/fstab
    
    /tmp/swap swap swap defaults 0 0

```
