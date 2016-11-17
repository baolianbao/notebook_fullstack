# 如何在Ubuntu 14.04上部署Node.js应用

## 简介

## 要求
This guide uses two Ubuntu 14.04 servers with private networking (in the same datacenter). We will refer to them by the following names:

* app: The server where we will install Node.js runtime, your Node.js application, and PM2
* web: The server where we will install the Nginx web server, which will act as a reverse proxy to your application. Users will access this server's public IP address to get to your Node.js application.

It is possible to use a single server for this tutorial, but you will have to make a few changes along the way. Simply use the localhost IP address, i.e. 127.0.0.1, wherever the app server's private IP address is used.

当然，只需要稍微做些改动，将`app`服务器的私有IP改为`127.0.0.1` 即可直接在同一台服务器上完成。

Here is a diagram of what your setup will be after following this tutorial:

![](node_diagram.png)
Reverse Proxy to Node.js Application

在开始之前，你需要一个有`sudo`权限的非`root`用户来配置服务器

## 安装Node
参考 02-Environment-Setup / Nodejs

## 创建或获取Node应用
可以直接

```bash
cd ~
mkdir www
cd www
git clone https://github.com/hexcola/stephub.git
```

运行应用
```
node app.js
```

## 安装PM2

```bash
sudo npm i pm2 -g 
```
### 通过 PM2 来管理应用
1. 启动应用
`$ pm2 start app.js`

This also adds your application to PM2's process list, which is outputted every time you start an application:

Output:
┌──────────┬────┬──────┬──────┬────────┬───────────┬────────┬────────────┬──────────┐
│ App name │ id │ mode │ PID  │ status │ restarted │ uptime │     memory │ watching │
├──────────┼────┼──────┼──────┼────────┼───────────┼────────┼────────────┼──────────┤
│ hello    │ 0  │ fork │ 5871 │ online │         0 │ 0s     │ 9.012 MB   │ disabled │
└──────────┴────┴──────┴──────┴────────┴───────────┴────────┴────────────┴──────────┘
As you can see, PM2 automatically assigns an App name (based on the filename, without the .js extension) and a PM2 id. PM2 also maintains other information, such as the PID of the process, its current status, and memory usage.

Applications that are running under PM2 will be restarted automatically if the application crashes or is killed, but an additional step needs to be taken to get the application to launch on system startup (boot or reboot). Luckily, PM2 provides an easy way to do this, the startup subcommand.

The startup subcommand generates and configures a startup script to launch PM2 and its managed processes on server boots. You must also specify the platform you are running on, which is ubuntu, in our case:

`pm2 startup ubuntu`

The last line of the resulting output will include a command (that must be run with superuser privileges) that you must run:

Output:
[PM2] You have to run this command as root
[PM2] Execute the following command :
[PM2] sudo su -c "env PATH=$PATH:/opt/node/bin pm2 startup ubuntu -u sammy --hp /home/sammy"
Run the command that was generated (similar to the highlighted output above) to set PM2 up to start on boot (use the command from your own output):

 `sudo su -c "env PATH=$PATH:/opt/node/bin pm2 startup ubuntu -u sammy --hp /home/sammy"`

2. PM2的其他功能

PM2 provides many subcommands that allow you to manage or look up information about your applications. Note that running pm2 without any arguments will display a help page, including example usage, that covers PM2 usage in more detail than this section of the tutorial.

Stop an application with this command (specify the PM2 App name or id):

`pm2 stop example`
Restart an application with this command (specify the PM2 App name or id):

`pm2 restart example`
The list of applications currently managed by PM2 can also be looked up with the list subcommand:

`pm2 list`
More information about a specific application can be found by using the info subcommand (specify the PM2 App name or id)::

`pm2 info example`
The PM2 process monitor can be pulled up with the monit subcommand. This displays the application status, CPU, and memory usage:

`pm2 monit`
Now that your Node.js application is running, and managed by PM2, let's set up the reverse proxy.

## 设置反向代理
先安装Nginx，参考 02-Environment-Setup / Nginx
同时参考 03-Configuration / Nginx-Server-Blocks

这样通过如下的配置我们就可以在同一台服务器上运行多个Node应用了。

## 确认app位置
根据上一步，现在我们的应用位于 `~/www/<app-name>`

## 为应用创建Server Block文件
默认Nginx包含一个Server Block文件`default`，我们可以用来作为模板，复制修改一下。

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/stephub.cn
```

删除`stephub.cn`中的所有内容，然后粘贴如下的配置内容，需要注意的是将`server_name`的值改为你自己的域名(如果没有就用IP)，且`app`服务器的私有IP地址`APP_PRIVATE_IP_ADDRESS`和端口根据你的实际情况进行调整。

```json
server {
    listen 80;

    server_name example.com;

    location / {
        proxy_pass http://APP_PRIVATE_IP_ADDRESS:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

该配置让web server来响应根目录请求，假设我们的服务器可以通过`stephub.cn`来访问，通过浏览器`http://stephub.cn`就会发送请求到Node应用的私有IP及对应端口，然后Node应用处理请求。

此外，在相同的`server block`下我们还可以添加额外的`location block`以便用于访问该`web`服务器下的其他应用，例如我们在`app`服务器的`8081`端口运行了另外一个Node应用，然后我们就可以通过如下的路径来访问了：
`http://example.com/app2`

```json
location /app2 {
        proxy_pass http://APP_PRIVATE_IP_ADDRESS:8081;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
```

配置完成之后，保存退出，然后通过
`sudo service nginx configtest` 来测试我们的配置文件是否有问题。

 现在就可以重启我们的服务器了
`sudo service nginx restart`