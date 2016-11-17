# PHP 

## 安装PHP 环境
现在我们已经安装了Nginx来展示网页，MySQL来存储和管理我们的数据，但我们仍旧需要可以连接它们两端并生成动态内容的部分。在这里我们使用PHP。

由于Nginx不像其他的一些Web服务器，默认情况下不包含PHP，我们需要安装`php-fpm`,也就是`fastCGI process manager`的缩写，我们也需要告诉Nginx，将PHP请求给该程序处理。

除了这个模块外，我们还需要另外的模块可以让PHP和我们的数据库进行沟通，它会安装到PHP的内核文件中。

```bash
sudo apt-get install php5-fpm php5-mysql
```

### 配置PHP 处理器
安装完成后，我们需要做些配置是系统更加安全。
通过超级管理权限打开`php-fpm`的配置文件：
```bash
sudo vi /etc/php5/fpm/php.ini
```

我们需要找的是，被注释的，用于设置参数的`cgi.fix_pathinfo`且默认值为1的那一项。

这是一个非常不安全的设置，因为它告诉PHPThis is an extremely insecure setting because it tells PHP to attempt to execute the closest file it can find if a PHP file does not match exactly.这几乎就是允许用户通过一些方式制造PHP请求来执行他们所不被允许的脚本。

我们需要取消注释，并将值设置为 0
```bash
cgi.fix_pathinfo=0
```
保存和关闭该文件，然后重启PHP处理器。
```bash
sudo service php5-fpm restart
```
这样我们的修改就起作用了。

## 配置Nginx来使用我们的PHP处理器
现在，我们把需要的组件都安装完成了，剩下需要做的就是告诉Nginx使用PHP处理器来处理动态内容。

我们通过修改Server block level（he Apache服务器的虚拟主机类似）值来实现，通过如下的命令打开Nginx的server block 配置文件：
```bash
sudo vi /etc/nginx/sites-available/default
```
当前情况下，除去那些被注释掉的内容，默认的server block文件内容如下：
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

我们需要做如下的配置：
1. 我们需要添加一个index.php选项，以便请求根目录的时候允许php文件
2. 需要修改`server_name`只想我们服务器的域名或公网IP
3. 取消注释一些用于定义错误处理的线程。
4. 对于PHP处理部分，我们需要取消注释，我们也需要添加 
5. First, we need to add an index.php option as the first value of our index directive to allow PHP index files to be served when a directory is requested.
We also need to modify the server_name directive to point to our server's domain name or public IP address.
The actual configuration file includes some commented out lines that define error processing routines. We will uncomment those to include that functionality.
For the actual PHP processing, we will need to uncomment a portion of another section. We will also need to add a try_files directive to make sure Nginx doesn't pass bad requests to our PHP processor.

下图中红色的部分就是需要修改的部分：
```json
server {
    listen 80 default_server;
    listen [::]:80 default_server ipv6only=on;

    root /usr/share/nginx/html;
    index index.php index.html index.htm;

    server_name server_domain_name_or_IP;

    location / {
        try_files $uri $uri/ =404;
    }

    error_page 404 /404.html;
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

在做了上面的改动后，你可以保存并关闭该文件，重启Nginx使其生效。
```bash
sudo service nginx restart
```

## 创建PHP文件来测试下配置
我们的LEMP栈应该已经完全配置好了，我们任然需要测试下，确保Nginx可以正确将.php文件交给PHP处理器来处理。
我们可以在上面配置的目录里创建info.php文件
```bash
sudo vi /usr/share/nginx/html/info.php
```
可以输入如下的内容：
```php
<?php
    phpinfo();
?>
```

当你完成后，保存关闭该文件，然后访问就可以了，你应该可以看到下图。这表示P使用Nginx PHP处理就成功了。

之后，我们也许该移除掉这个文件，以免给未授权的用户知道我们的配置信息，避免一些意图。如果需要你可以之后再创建。


如果访问失败，可以查看错误日志： 
[Where can I find the error logs of nginx, using fastcgi and django](http://stackoverflow.com/questions/1706111/where-can-i-find-the-error-logs-of-nginx-using-fastcgi-and-django)
 /var/log/nginx/nginx_error.log

## 参考
* [How To Install Linux, nginx, MySQL, PHP (LEMP) stack on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-14-04)

* [How to check my PHP and MySQL version on Ubuntu VPS?](http://serverfault.com/questions/296156/how-to-check-my-php-and-mysql-version-on-ubuntu-vps)

[How To Install and Secure phpMyAdmin with Nginx on an Ubuntu 14.04 Server](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-with-nginx-on-an-ubuntu-14-04-server)


[虚拟主机管理系统](http://baike.baidu.com/view/822862.htm)
