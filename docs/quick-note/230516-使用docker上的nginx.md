# 使用 docker 上的 nginx


## 获取镜像
```shell
docker pull nginx
```


## 获取配置文件
```shell
docker run -d --naem nginx nginx
docker cp nginx:/etc/nginx/ ./
```

找到其中的 nginx.conf 这是主要的配置文件，默认内容如下：
```

user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
```

> 我为啥要在这里吧默认内容列出来呢，，，，因为他妈的有大坑



## 创建容器

```shell
image_tag='nginx' && \
content_name='nginx_web_learn' && \
docker_data_dire='/home/amadeus/data/docker' && \
docker run -d \
--network=host \
--privileged=true \
-v ${docker_data_dire}/${image_tag}/${content_name}/log:/var/log/nginx \
-v ${docker_data_dire}/${image_tag}/${content_name}/html:/usr/share/nginx/html \
-v ${docker_data_dire}/${image_tag}/${content_name}/conf/nginx.conf:/etc/nginx/nginx.conf \
--name ${content_name} ${image_tag}
```


## 配置代理
编辑 nginx.conf
```
user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    # log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                   '$status $body_bytes_sent "$http_referer" '
    #                   '"$http_user_agent" "$http_x_forwarded_for"';

    # access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       90;
        server_name  localhost;

        location / {
            root   /usr/share/nginx/html;
            index  index.html index.htm;
        }

        location ^~ /api/ {
            rewrite ^/api/(.*) /$1 break;
            proxy_pass http://localhost:8080;
        }
        
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }
    # include /etc/nginx/conf.d/*.conf;
}
```
我这里修改了 nginx 的监听端口为 90 还配置了将所有 /api/{} 的请求转发到 localhost:8080/{}s 。
你可能将做不一样的修改，但  是，不论你将要做什么样的修改你都要注意默认的 nginx.conf 配置文件的最后一行
`include /etc/nginx/conf.d/*.conf;` 它引入了 conf.d 目录下的所有配置文件，这其中可能就有一个名为 default.conf 的配置文件
他将覆盖掉你的一些重要配置。==在你不知情的情况下！！！==
