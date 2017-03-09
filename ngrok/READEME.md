docker 镜像构建 文件：

FROM ubuntu:latest

MAINTAINER jyy <582497915@qq.com>

COPY . /usr/local/myngrok/

EXPOSE 4441 4442 4443

CMD ["/usr/local/myngrok/bin/ngrokd", "-domain", "ngrok.mrsix.top", "-httpAddr", ":4441", "-httpsAddr", ":4442", "-tunnelAddr", ":4443"]

开启 ngrok 内网穿透服务
`docker run --name ngrok -p 4441:4441 -p 4442:4442 -p 4443:4443 -d  mrsix/my-ngrok`


