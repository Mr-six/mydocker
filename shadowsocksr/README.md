## shadowsocksr命令
暂时shadowsocksr安装在当前主机下，以后解决端口暴露问题后，打算将其放入docker中。

用户操作
    python mujson_mgr.py

    如 `python mujson_mgr.py -a -utest -p6666 -ktest -t100`
参数说明：

    Actions:
      -a ADD               add/edit a user
      -d DELETE            delete a user
      -e EDIT              edit a user
      -c CLEAR             set u/d to zero
      -l LIST              display a user infomation or all users infomation

    Options:
      -u USER              the user name
      -p PORT              server port (only this option must be set if add a user)
      -k PASSWORD          password
      -m METHOD            encryption method, default: aes-128-ctr
      -O PROTOCOL          protocol plugin, default: auth_aes128_md5
      -o OBFS              obfs plugin, default: tls1.2_ticket_auth_compatible
      -G PROTOCOL_PARAM    protocol plugin param
      -g OBFS_PARAM        obfs plugin param
      -t TRANSFER          max transfer for G bytes, default: 8388608 (8 PB or 8192 TB)
      -f FORBID            set forbidden ports. Example (ban 1~79 and 81~100): -f "1-79,81-100"
      -i MUID              set sub id to display (only work with -l)

    General options:
      -h, --help           show this help message and exit


服务端运行与停止

后台运行（无log，ssh窗口关闭后也继续运行）

./run.sh

后台运行（输出log，ssh窗口关闭后也继续运行）

./logrun.sh

后台运行时查看运行情况

./tail.sh

停止运行

./stop.sh

注：通过脚本运行默认日志会保存在根目录的ssserver.log，可手动查看。

更新源代码

如果代码有更新可用本命令更新代码

进入shadowsocksr目录

cd shadowsocksr

执行

git pull

成功后重启ssr服务
