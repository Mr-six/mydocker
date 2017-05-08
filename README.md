## docker 项目 文件目录
为保证线上线下统一环境和目录，故建立 mydocker 管理 docker 应用的配置项

线上默认不对外暴露端口，通过 容器间的 --link 来传输数据 访问通过 Nginx 反向代理实现

需要持久化的数据 使用 -v 设置数据卷

本地端 使用 -p 暴露本机端口（比如mysql rides 等）省去了安装配置的烦恼

log日志暂时没做处理，等有了方案在解决

目录位于 /usr/local/mydocker/ 下便于平台统一
```
git clone https://github.com/Mr-six/mydocker.git
```

暂时应用如下：
  * express
  * mysql 
  * redis
  * nginx
  * ngrok
  * shadowsocksr（暂未做成docker容器）

## 服务器单个启动 docker 服务

开启 express web 服务
docker run --name express -d mrsix/docker-express

开启 ngrok 内网穿透服务
docker run --name ngrok -p 4441:4441 -p 4442:4442 -p 4443:4443 -d  mrsix/my-ngrok

开启 Nginx 反向代理

docker run --name nginx -p 80:80 -p 443:443 -v /usr/local/mydocker/nginx/nginx.conf:/etc/nginx/nginx.conf:ro --link express:express --link ngrok:ngrok -d mrsix/my-nginx

## 使用docker-compose 启动应用
* 编写 docker-compose.yml 文件
* 填写相关配置项
* 在目录运行 `docker-compose up` 来检测服务是否正常启动，如一切正常 Ctrl+C 结束
* 使用 `docker-compose start` 启动项目，其会在后台运行，使用 `docker-compose logs`可查看相关日志
[命令参考](https://yeasy.gitbooks.io/docker_practice/content/compose/commands.html)

