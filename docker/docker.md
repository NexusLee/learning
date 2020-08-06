
## Docker

### 1. pull

```
docker pull hello-world
```

### 2. run
```
docker run hello-world
```

### 3. exec
    
"exec" 命令只能执行一个已运行的容器, 所以它需要通过容器ID去运行而非镜像.
    
```
docker run -itd alpine
docker exec containerid /bin/bash
```

### 4. start/stop/restart
```
docker start/stop/restart containerid/containername
```

### 5. network create 
```
docker network create --driver bridge my_net
```

### 6. attach 正确退出方式 
```
ctrl+p ctrl+q
```

### 7. 容器间使用相同网络
```
container1: --name=japronto
container2: --network=container:japronto
```

### 8. namespace 

```
Mount, UTS, IPC, PID, Network 和 User
```

### 9. docker 网络 

```
none, host 和 bridge
```

### 10. user-defined 网络

```
bridge, overlay 和 macvlan
```

### 11. 容器间通信

```
IP 通信, Docker DNS Server 和 joined 容器

```

### 12. 查看网络

```
docker network inspect
```

### 13. docker存储

   - storage driver 管理的镜像层和容器层

   - Data Volume
   
    1. bind mount
    
    -v <host path>:<container path>: auth
    
    2. docker managed volume

### 14. 删除 none 镜像

```
$ docker stop $(docker ps -a | grep "Exited" | awk '{print $1 }') //停止容器
$ docker rm $(docker ps -a | grep "Exited" | awk '{print $1 }')  //删除容器 
$ docker rmi $(docker images | grep "none" | awk '{print $3}')  //删除镜像 
```

### 15. 保存镜像

```
-a :提交的镜像作者；
-c :使用Dockerfile指令来创建镜像；
-m :提交时的说明文字；
-p :在commit时，将容器暂停。
将容器a404c6c174a2 保存为新的镜像,并添加提交人信息和说明信息

docker commit -a "runoob.com" -m "my apache" a404c6c174a2 mymysql:v1
```
