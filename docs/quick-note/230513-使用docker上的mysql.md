# 使用 docker 上的 mysql 
@Time("2023-05-13")

## 创建 mysql 容器
```
mysql_name='mysql_web_learn' && \
docker run -d \                       
-p 3306:3306 \
--privileged=true \ 
-v /home/amadeus/data/docker/mysql/$(mysql_name)/log:/var/log/mysql \
-v /home/amadeus/data/docker/mysql/$(mysql_name)/data:/var/lib/mysql \
-v /home/amadeus/data/docker/mysql/$(mysql_name)/conf.d:/etc/mysql/conf.d \
-e MYSQL_ROOT_PASSWORD=abc1235 \ 
--name $(mysql_name) mysql:8.0.33-debian \
--character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```

## 配置字符集
```shell
vim /home/amadeus/data/docker/mysql/$(mysql_name)/conf.d/my.cnf
```
添加如下内容
```
[client]
default-character-set = utf8mb4

[mysql]
default-character-set = utf8mb4

[mysqld]
character-set-server=utf8mb4
character-set-client-handshake = FALSE
collation-server = utf8mb4_unicode_ci
init_connect='SET NAMES utf8mb4'
```


```mysql
show variables like 'character%'
```

## 解决连接缓慢问题
用 idea 连接时发现对于数据库的各种操作都非常慢，要十秒左右
```
# 编辑 my.cnf
[mysqld]
skip-name-resolve
```

> 参考链接
> https://blog.csdn.net/weixin_43464964/article/details/122837704


