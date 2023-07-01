# 高并发的底层逻辑
异步，非阻塞
在Nodejs中，数据库连接会自动生成为线程，并在js级别进行异步处理

# QPS
Query Per Second 每秒查询次数，即并发数

# 代理
反向代理
正向代理

# 动静分离
server {
  listen port;
  server_name ip;
  // 前端
  location /fe {
    root html;
    index index.html;
    try_files $uri /fe/index.html;
  }
  // 后端
  location /be {
    proxy_pass http://domain;
    //proxy_set_header Host $host:$server_port;
  }
}

# 负载均衡 集群cluster
upstream domain {
  server server_name1:port1 weight=3;
  server server_name2:port2 weight=2;
  server server_name3:port3 weight=2;
  server server_name4:port4 weight=3;
}

# SSL证书
获取证书和秘钥
  关闭核心防护和防火墙 systemctl stop firewalld     systemctl disable firewalld     setenforce 0
  安装openssl工具 yum install -y openssl
  创建存放证书的地址 mkdir -p /etc/nginx/ssl_key
  创建私钥 openssl genrsa -idea -out server.key 2048
  生成证书 openssl req -days 3650 -x509 -sha256 -nodes -newkey rsa:2048 -keyout server.key -out server.crt

配置SSL模块
  添加ssl模块 yum -y install gcc gcc-c++ pcre pcre-devel zlib zlib-devel openssl openssl-devel make
  开始编译 ./configure --prefix=/usr/local/nginx --user=nginx --group=nginx --with-http_ssl_module
  编译安装 make
  关闭服务 systemctl stop nginx
  覆盖旧的nginx服务 cp ./objs/nginx /usr/local/nginx/sbin/

  配置nginx文件
  server {
    listen 443 ssl;
    server_name ip;
    ssl_certificate /path/to/server.crt;
    ssl_certificate_key /path/to/server.key;
    location / {
      root /https-xx;
      index index.html;
    }
  }

# 扩缩容
Kubernetes

