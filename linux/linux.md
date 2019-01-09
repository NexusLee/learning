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
