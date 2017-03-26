##docker 镜像构建 文件：

    FROM ubuntu:latest

    MAINTAINER jyy <582497915@qq.com>

    COPY . /usr/local/myngrok/

    EXPOSE 4441 4442 4443 4444 4445 4446 4447 4448 4449

    CMD ["/usr/local/myngrok/bin/ngrokd", "-domain", "ngrok.mrsix.top", "-httpAddr", ":4441", "-httpsAddr", ":4442", "-tunnelAddr", ":4443"]

开启 ngrok 内网穿透服务

    docker run -d --name ngrok \
    -p 4441:4441 \
    -p 4442:4442 \
    -p 4443:4443 \
    -p 4444:4444 \
    -p 4445:4445 \
    -p 4446:4446 \
    -p 4447:4447 \
    -p 4448:4448 \
    -p 4449:4449 \
    mrsix/my-ngrok



