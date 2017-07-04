## postgres 介绍
[postgres中文手册](http://www.postgres.cn/docs/9.3/)

##本地docker postgres 容器配置
***


## 本地生成容器命令 
  `docker run --name postgres-server \
   -p 127.0.0.1:5432:5432 \
   -v /usr/local/mydocker/postgres/database:/var/lib/postgresql/data/pgdata \
   -e POSTGRES_USER=root \
   -e POSTGRES_PASSWORD=root \
   -e PGDATA=/var/lib/postgresql/data/pgdata \
   -d  postgres ` 


  1. 容器名称为 postgres-server 
  2. 暴露本地ip+端口 便于连接 
  3. postgres 数据持久化位置：/usr/local/mydocker/postgres/database

  docker start postgres-server
  
----
## docker 容器连接命令
  `docker run -it --rm --link postgres-server:postgres postgres psql -h postgres -U root`

  1. --rm 可在容器退出后删除内容变化 因为此容器的存在只是为了 连接数据库
----
