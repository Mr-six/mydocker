## docker 项目 文件目录
为保证线上线下统一环境和目录，故建立 mydocker 管理 docker 应用的配置项

线上默认不对外暴露端口，通过 容器间的 --link 来传输数据 访问通过 Nginx 反向代理实现

需要持久化的数据 使用 -v 设置数据卷

本地端 使用 -p 暴露本机端口（比如mysql rides 等）省去了安装配置的烦恼

log日志暂时没做处理，等有了方案在解决

目录位于 /usr/local/mydocker/ 下便于平台统一

暂时应用如下：
  * express
  * mysql 
  * redis
  * nginx
  * ngrok

## 服务器点 docker 服务

开启 express web 服务
docker run --name express -d mrsix/docker-express

开启 ngrok 内网穿透服务
docker run --name ngrok -p 4441:4441 -p 4442:4442 -p 4443:4443 -d  mrsix/my-ngrok

开启 Nginx 反向代理

docker run --name nginx -p 80:80 -p 443:443 -v /usr/local/mydocker/nginx/nginx.conf:/etc/nginx/nginx.conf:ro --link express:express --link ngrok:ngrok -d mrsix/my-nginx

