## 为Wordpress创建MySQL数据库和用户

开始使用Wordpress之前，我们首先需要准备我们的数据库。

尽管我们已经安装了MySQL数据软件，但并未为WordPress创建数据库，同时也需要为WordPress创建一个账户以便其访问数据库。

通过如下命令登入MySQL管理：
```bash
mysql -u root -p
```

需要提供密码，现在我们需要为WordPress应用创业一个数据库，名为`wordpress`
```
CREATE DATABASE wordpress;
```

我们现在有数据库了，需要为其创建一个用户了。并在之后将该数据库的控制权交给新用户，那样我们的应用就可以与数据库进行交互了。

我们将使用`wordpressuser`作为用户名，并使用`password`作为密码
```bash
CREATE USER wordpressuser@localhost IDENTIFIED BY 'password';
```

现在我们有又了数据库和用户了，但它们之间没有任何联系。我们需要告诉MySQL，我们的新用户可以访问和控制数据库：
```bash
GRANT ALL PRIVILEGES ON wordpress.* TO wordpressuser@localhost;
```
现在就算是配置完成了， We need to flush the privileges to disk so that our current instance of MySQL knows about the privilege changes we have made:
```bash
FLUSH PRIVILEGES;
```
退出MySQL：
```bash
exit
```

## 下载WordPress到服务器
The latest stable version of the application is always given the same URL, which makes this part easy. We want to download the file to our user's home directory:
```bash
cd ~
wget http://wordpress.org/latest.tar.gz
```
Our application files have been downloaded as a compressed, archived directory structure stored in a file called latest.tar.gz. We can extract the contents by typing:
```bash
tar xzvf latest.tar.gz
```
This will create a directory called wordpress that contains the site files.

此时趁这个机会，下载一些WordPress实例需要用到的额外的组件：
```
sudo apt-get update
sudo apt-get install php5-gd libssh2-php
```
这两个包允许我们使用使用SSH来操作图片，安装更新插件和组件
These two packages allow you to work with images and install/update plugins and components using SSH respectively.

## 配置Wordpress

## 复制文件到Document Root
