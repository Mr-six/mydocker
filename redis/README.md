## redis 介绍
[redis简单介绍](http://www.redis.net.cn/tutorial/3503.html)

##本地docker redis 容器配置
***
  * cnf 文件为redis 配置文件

## 本地生成容器命令 
  `docker run --name redis-server -p 127.0.0.1:6379:6379 -v /usr/local/mydocker/redis/redis.conf:/usr/local/etc/redis/redis.conf -d  redis redis-server /usr/local/etc/redis/redis.conf ` 

  1. 容器名称为 redis-server 
  2. 暴露本地ip+端口 便于连接 
  3. 使用本地的配置文件 redis.conf
  4. redis 目前暂只用来内存储存，暂不考虑数据持久化，添加数据卷等

  docker start redis-server
  
----
## docker 容器连接命令
  `docker run -it --link redis-server:redis --rm redis  redis-cli -h redis -p 6379`

  1. --rm 可在容器退出后删除内容变化 因为此容器的存在只是为了 连接数据库
----

## 服务器生成容器命令
  `docker run --name redis-server -v /usr/local/mydocker/redis/redis.conf:/usr/local/etc/redis/redis.conf -d  redis redis-server /usr/local/etc/redis/redis.conf ` 

  1. 取消了暴露端口的命令，程序采用 --link 获取通信
