## 基于docker的ipsec-vpn 服务

[docker 镜像](https://github.com/hwdsl2/docker-ipsec-vpn-server)

使用方法 ：
1. 账号配置文件 vpn.env 如下
```
    VPN_IPSEC_PSK=<IPsec pre-shared key>
    VPN_USER=<VPN Username>
    VPN_PASSWORD=<VPN Password>`
```
2. 主机上加载 IPsec NETKEY 内核模块
    `sudo modprobe af_key`
3. 创建docker容器
```
    docker run \
    --name ipsec-server \
    --env-file ./vpn.env \
    --restart=always \
    -p 500:500/udp \
    -p 4500:4500/udp \
    -v /lib/modules:/lib/modules:ro \
    -d --privileged \
    hwdsl2/ipsec-vpn-server`
```
4. 查看链接情况：
    `docker exec -it ipsec-server ipsec whack --trafficstatus`
    
