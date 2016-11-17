# 安装MySQL

在安装了web服务器之后，我们需要安装用于为我们的网站存储和管理数据的数据库管理系统MySQL。

```bash
sudo apt-get install mysql-server
```

在安装的过程中会要求我们提供超级管理员的密码，尽管MySQL数据库软件已经安装好了，但是我们的配置还没有完全完成。

首先，我们需要告诉MySQL生成其所需用来存储数据库和信息的的目录结构。可以简单的通过如下的命令来完成：
```bash
sudo mysql_install_db
```
接下来，你需要运行写简单的安全脚本用来提示你修改一些不安全的默认配置。输入如下的命令
```bash
sudo mysql_secure_installation
```
同样需要输入在安装的时候输入的MySQL超级管理员密码。 如果没有设置密码，输入`N`然后敲回车，回提示你移除一些测试用户和数据库，一直敲回车就可以了，它会帮我们移除不安全的默认配置的。

脚本运行结束后，MySQL就算是安装完成了。