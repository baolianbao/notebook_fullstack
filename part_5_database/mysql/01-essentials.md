---
title: MySQL Essentials
date: 2016-08-15 18:37:51
tags:
categories: fullstack
---

一、安装
http://dev.mysql.com/downloads/mysql/
安装结束会提示一个默认密码。

二、修改默认密码

cd /usr/local/mysql/bin
$ mysqladmin -u root -p'oldpassword' password newpass
参考链接：http://www.cyberciti.biz/faq/mysql-change-root-password/

三、创建新的用户与密码

四、如何卸载MySQL：

To uninstall MySQL and completely remove it (including all databases) from your Mac do the following:

- Open a terminal window
- Use mysqldump to backup your databases to text files!
- Stop the database server
- sudo rm /usr/local/mysql
- sudo rm -rf /usr/local/mysql*
- sudo rm -rf /Library/StartupItems/MySQLCOM
- sudo rm -rf /Library/PreferencePanes/My*
- edit /etc/hostconfig and remove the line MYSQLCOM=-YES-
- rm -rf ~/Library/PreferencePanes/My*
- sudo rm -rf /Library/Receipts/mysql*
- sudo rm -rf /Library/Receipts/MySQL*
- sudo rm -rf /private/var/db/receipts/*mysql*