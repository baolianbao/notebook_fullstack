# 在Ubuntu 14.04 Server上搭建VPN服务器

## 购买VPS
选择搬瓦工，便宜！

## 重新安装操作系统


## 安装shadowsocks服务端
`apt-get update`
`apt-get install python-gevent python-pip`
`pip install shadowsocks`

## 配置shadowsocks
`vi /etc/shadowsocks.json`

1. 单人模式
```json
{
    "server":"<your_server_ip>",
    "server_port":443,
    "local_address":"127.0.0.1",
    "local_port":1080,
    "password":"yourpassword",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
}
```

2. 多人模式
```json
{
    "server":"<your_server_ip>",
    "local_address":"127.0.0.1",
    "local_port":1080,
    "port_password":{
         "8989":"password0",
         "9001":"password1",
         "9002":"password2",
         "9003":"password3",
         "9004":"password4"
    },
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
}
```
> 更多参考: 
> * [shadowsocks Quick Guide](https://shadowsocks.org/en/config/quick-guide.html)
> * [Configuration via Config File](https://github.com/shadowsocks/shadowsocks/wiki/Configuration-via-Config-File)

## 运行
我们可以用`ssserver -h`查看帮助。
1. 根据配置文件启动
`ssserver -c /etc/shadowsocks.json -d start`
2. 停止与重启
`ssserver -d stop`
`ssserver -d reload`

## 开机启动
`/usr/bin/python /usr/local/bin/ssserver -c /etc/shadowsocks.json -d start
`

## 高阶
### 优化
* [shadowsocks Advanced](https://shadowsocks.org/en/config/advanced.html)

### 管理多用户
* [Manage Multiple Users](https://github.com/shadowsocks/shadowsocks/wiki/Manage-Multiple-Users)