##本地docker mysql 容器配置
***
  * cnf 文件为MySQL 配置文件
  * database 为数据卷 挂载文件 便于数据持久化

## 本地生成容器命令 
  `docker run --name mysql-server -p 127.0.0.1:3306:3306 -v /usr/local/mydocker/mysql/cof:/etc/mysql/conf.d -v /usr/local/mydocker/mysql/database:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -d mysql` 

  1. 容器名称为 mysql-server 
  2. 暴露本地ip+端口 便于连接 
  3. 挂载连个数据卷 
  4. 设置密码为 root
  5. 本地开启 `docker start mysql-server`
  6. 使用下方进行容器连接或者 使用客户端连接
  
  
----
## docker 容器连接命令
  `docker run -it --link mysql-server:mysql --rm mysql sh -c 'exec mysql -h "$MYSQL_PORT_3306_TCP_ADDR" -P"$MYSQL_PORT_3306_TCP_PORT" -uroot -p"$MYSQL_ENV_MYSQL_ROOT_PASSWORD"' `

  1. --rm 可在容器退出后删除内容变化 因为此容器的存在只是为了 连接数据库

## 服务器生成容器命令 
  `docker run --name mysql-server -v /usr/local/mydocker/mysql/cof:/etc/mysql/conf.d -v /usr/local/mydocker/mysql/database:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -d mysql` 
