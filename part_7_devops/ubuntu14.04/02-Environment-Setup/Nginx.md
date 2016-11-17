# 如何在Ubuntu 14.04 LTS上安装Ngnix

In order to display web pages to our site visitors, we are going to employ Nginx, a modern, efficient web server.

All of the software we will be getting for this procedure will come directly from Ubuntu's default package repositories. This means we can use the apt package management suite to complete the installation.

Since this is our first time using apt for this session, we should start off by updating our local package index. We can then install the server:

## 第一步：安装Nginx
```bash
sudo apt-get update
sudo apt-get install nginx
```

## 第二步：查看Web服务器
In Ubuntu 14.04, Nginx is configured to start running upon installation.
You can test if the server is up and running by accessing your server's domain name or public IP address in your web browser.
If you do not have a domain name pointed at your server and you do not know your server's public IP address, you can find it by typing one of the following into your terminal:

```bash
ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'
```

```bash
111.111.111.111
fe80::601:17ff:fe61:9801
```
Or you could try using:

```bash
curl http://icanhazip.com
111.111.111.111
```
Try one of the lines that you receive in your web browser. It should take you to Nginx's default landing page:

http://server_domain_name_or_IP
Nginx default page

If you see the above page, you have successfully installed Nginx.

## 第三步：管理Nginx进程
1. 停止Web Server
`sudo service nginx stop`

2. 启动Web Server
`sudo service nginx start`

3. 停止后再启动Web Server
`sudo service nginx restart`


4. 设置确保当服务器重启时Web Server会自动启动
`sudo update-rc.d nginx defaults`

This should already be enabled by default, so you may see a message like this:

System start/stop links for /etc/init.d/nginx already exist.

## 参考文件
* [How To Install Nginx on Ubuntu 14.04 LTS](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-14-04-lts)