## nginx 反向代理
[nginx 反向代理参考资料](http://www.jianshu.com/p/bed000e1830b)

## 我的docker配置
测试 本地 my-resume 文件

docker run --name my-nginx -p 80:80 -v /usr/local/mydocker/docker/nginx/nginx.conf:/etc/nginx/nginx.conf:ro -v /Users/miaojiang/web/my-resume/:/srv/www -d nginx

## 服务器 nginx 反向代理
docker run --name nginx -p 80:80 -v /usr/local/mydocker/nginx/nginx.conf:/etc/nginx/nginx.conf:ro --link express-test:express -d nginx

  1. 使用 --link 连接docker容器程序，配置 nginx.conf 设置反向代理
