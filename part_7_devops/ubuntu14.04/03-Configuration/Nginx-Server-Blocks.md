# 如何在Ubuntu 14.04上设置Nginx Server Blocks

## 简介
使用Nginx Web Server时， `server blocks`（类似于Apache中的 virtual hosts）可以用于封装配置详细内容以及在一台物理服务器上运行多个web服务器。
When using the Nginx web server, server blocks (similar to the virtual hosts in Apache) can be used to encapsulate configuration details and host more than one domain off of a single server.

## 条件
确保已经安装了Nginx
作为案例，我们会在Nginx服务器里设置两个域
我们会使用example.com和test.com
要保证域名要解析到指定的IP


## 第一步：指定一个根目录
我假设将目录设置在~/www下，也就是/home/hexcola/www
然后在这个目录下创建不同的项目
`sudo mkdir -p /home/hexcola/www/example.com/html`
`sudo mkdir -p /home/hexcola/www/test.com/html`

将这两个文件夹的所有权转给我们的常用用户，比如我们这里的用户是hexcola，我们可以通过$USER环境变量来获取，这个步骤可以让当前用户创建文件，而普通的访问用户不可以修改内容
``` bash
sudo chown -R $USER:$USER /var/www/example.com/html
sudo chown -R $USER:$USER /var/www/test.com/html
```

## 第二步：创建示例页面
在/example.com/html和test.com/html目录下创建 index.html文件

## 第三步：为我们的两个网站创建Server Block文件
现在我们有两个文件要对外展示，我们需要Server block文件来告诉Nginx怎么做

默认情况下，Nginx包含一个Server Block文件 `default`可以作为一个模板文件，我们直接复制，然后做些修改。
复制：
`sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/example.com`

编辑该文件：

```json
server {
    listen 80 default_server;
    listen [::]:80 default_server ipv6only=on;

    root /usr/share/nginx/html;
    index index.html index.htm;

    server_name localhost;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

1. 关于listen
我们仅仅需要一个`default_server`，它往往用于Only one of our server blocks can have the default_server specification. This specifies which block should server a request if the server_name requested does not match any of the available server blocks.

2. 修改文件目录
`root /home/hexcola/www/html`

3. 修改 server_name
`server_name example.com www.example.com`

看起来如下：

```json
server {
    listen 80 default_server;
    listen [::]:80 default_server ipv6only=on;

    root /var/www/example.com/html;
    index index.html index.htm;

    server_name example.com www.example.com;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

对于第二个Server Block文件，主要在于需要移除`default_server`
所以关于listen部分就如：
```
listen 80;
listen [::]:80;
```

其他照旧

## 第四步：启用Server Block文件，重启Nginx
1. 要启用Server Block文件，我们可以通过创建Symbolic Link文件到Nginx在启动的时候回读取的`sites-enabled`目录，
```
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/test.com /etc/nginx/sites-enabled/
```
要移除，我们可以直接删除sites-enabled文件夹内的文件
`sudo rm /etc/nginx/sites-enabled/default`


2. 同时，取消`/etc/nginx/nginx.conf`文件中的`server_name_hash_bucket_size 64`的注释

3. 现在就可以重启我们的服务器了
`sudo service nginx restart`

同时我们可以通过
`sudo service nginx configtest` 来测试我们的配置文件是否有问题。

## 参考文件
* [How To Set Up Nginx Server Blocks (Virtual Hosts) on Ubuntu 14.04 LTS](https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-14-04-lts)
* [Set up Automatic Virtual Hosts with Nginx and Apache](http://www.sitepoint.com/set-automatic-virtual-hosts-nginx-apache/)