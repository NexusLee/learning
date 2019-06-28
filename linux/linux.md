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
