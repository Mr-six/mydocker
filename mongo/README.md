## mongo 介绍
[mongo简单介绍](http://www.mongo.net.cn/tutorial/3503.html)

##本地docker mongo 容器配置
***
  * cnf 文件为mongo 配置文件

## 本地生成容器命令 
  `docker run --name mongo-server -p 127.0.0.1:27017:27017 -v /usr/local/mydocker/mongo/database:/data/db -d  mongo ` 

  1. 容器名称为 mongo-server 
  2. 暴露本地ip+端口 便于连接 
  3. mongo 数据持久化位置：/usr/local/mydocker/mongo/database

  docker start mongo-server
  
----
## docker 容器连接命令
  `docker run -it --link mongo-server:mongo --rm mongo sh -c 'exec mongo "$MONGO_PORT_27017_TCP_ADDR:$MONGO_PORT_27017_TCP_PORT/test"'`

  1. --rm 可在容器退出后删除内容变化 因为此容器的存在只是为了 连接数据库
----

## 服务器生成容器命令
  `docker run --name mongo-server -v /usr/local/mydocker/mongo/database:/data/db -d  mongo ` 

  1. 取消了暴露端口的命令，程序采用 --link 获取通信
