### gzip压缩

``` nginx
  gzip on; #开启gzip压缩功能
  gzip_min_length 10k; #设置允许压缩的页面最小字节数; 这里表示如果文件小于10个字节，就不用压缩，因为没有意义，本来就很小.
  gzip_buffers 4 16k; #设置压缩缓冲区大小，此处设置为4个16K内存作为压缩结果流缓存
  gzip_http_version 1.1; #压缩版本
  gzip_comp_level 2; #设置压缩比率，最小为1，处理速度快，传输速度慢；9为最大压缩比，处理速度慢，传输速度快; 这里表示压缩级别，可以是0到9中的任一个，级别越高，压缩就越小，节省了带宽资源，但同时也消耗CPU资源，所以一般折中为6
  gzip types text/css text/xml application/javascript; #制定压缩的类型,线上配置时尽可能配置多的压缩类型!
  gzip_disable "MSIE [1-6]\."; #配置禁用gzip条件，支持正则。此处表示ie6及以下不启用gzip（因为ie低版本不支持）
  gzip vary on; #选择支持vary header；该选项可以让前端的缓存服务器缓存经过gzip压缩的页面; 这个可以不写，表示在传送数据时，给客户端说明我使用了gzip压缩
```

### expires设定页面缓存时间

配置expires起到控制页面缓存的作用，合理的配置expires可以减少很多服务器的请求要配置expires
``` nginx
  location ~ \.(gif|jpg|jpeg|png|bmp|ico)$ {
     root /var/www/img/;
     expires 30d; # 30m：30 分钟，2h：2 小时，30d：30 天
  }
```

### 事件处理模型优化use epoll

epoll用在linux上, kqueue用在bsd上, 不能物理上共存。如果你的服务器cpu较好，linux内核新，可考虑用epoll
``` nginx
  events {
    #单个进程允许的客户端最大连接数
    worker_connections  20480;
    #收到一个新连接通知后接受尽可能多的连接。
    multi_accept on; 
    #使用epoll模型
    use epoll;
  }
```

### 高效文件传输模式sendfile on

参数sendfile on 用于开启文件高效传输模式，同时将tcp_nopush on 和tcp_nodelay on 两个指令设置为on，可防止网络及磁盘I/O阻塞，提升Nginx工作效率
``` nginx
  #开启高效文件传输模式
  sendfile on;
  #减少网络报文段数量
  tcp_nopush on;
  #提高I/O性能
  tcp_nodelay on;
```

### 优化服务器域名的散列表大小

如果在 server_name 中配置了一个很长的域名，那么重载 Nginx 时会报错，因此需要使用 server_names_hash_max_size 来解决域名过长的问题
``` nginx
  #域名散列表大小 
  server_names_hash_bucket_size 64;
  server_names_hash_max_size 2048;
```

### 优化worker服务进程数

worker进程数最开始的设置可以等于CPU的核数，高流量高并发场合也可以考虑将进程数提高至CPU核数*2
``` linux
  #查看CPU总颗数：
  [root@nginx conf]# grep 'physical id' /proc/cpuinfo|sort|uniq|wc -l
  1
  #查看CPU总核数：
  [root@nginx conf]# grep processor /proc/cpuinfo |wc -l
  4
```
``` nginx
  #CPU的总核数4
  worker_processes  4;
```
