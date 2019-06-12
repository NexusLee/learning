
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
