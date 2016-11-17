title: 如何访问Ubuntu 14.04 Server
date: 2016-03-12 17:31:13
tags: ubuntu
---


创建了新的服务器之后，我们需要能够访问和操作。
本文章就主要用于解决如何访问以及和访问相关的问题。
> 注: 这里的访问特指具有服务器操作权限（重启、更新系统，修改配置等等）的访问，而非服务性质的访问（例如ftp服务器，web服务，文件共享服务等）。

## 访问服务器的方式

我们访问服务器主要有两种方式：
1. 直接访问
2. 通过ssh远程访问

直接访问又有两种情况：
1. “肉身”访问： 对机器直接操作，比如我们安装好的虚拟机，或者在本地搭建的服务，我们可以看得见摸得着的，我们可以直接打开该服务器并访问
2. 网页访问：一般我们购买的云服务器之后，服务商都会提供一个网页，用于管理登录终端，这样的效果也等同于我们直接访问了。

从目前来看，无论是直接访问还是远程访问，我们都需要服务器的地址（IP或者域名），用户名，密码才能登录。

那我们需要掌握的第一个技能就是用户管理。

## 用户管理
对于不同的服务器，默认的环境可能不一样，比如我购买了阿里云的服务器，我得到了一个root用户和初始密码，而没有其他的用户，但在本地安装服务器的时候，直接新建了一个用户，而没有见到root用户。
> root用户是Linux环境的超级用户，由于权限太大，并不建议使用root用户来使用操作系统，以免造成不可逆的操作，所以需要创建一个限定操作范围用于处理日常操作的新用户

所以我们先来将环境重置为系统只有root用户，然后继续操作。

### root用户管理
#### 启用root用户
通过我们安装系统时设置的密码登录到操作系统，然后使用如下的命令：
passwd是用于修改用户密码的工具

`sudo passwd root`

之后我们就可以直接使用root用户来登录了。

#### 通过root管理其他用户
1. 列出所有的用户

`lastlog`
或者查看 `/etc/passwd` 文件
> Tips: [How to display all user and groups by command](http://askubuntu.com/questions/515103/how-to-display-all-user-and-groups-by-command)

2. 删除用户
首先删除用户名：
`userdel <username>`
然后再删除用户的home目录：
`rm -r /home/<username>`

退出后再用hexcola就无法登录了。



3. 新增用户
`adduser <username>`
服务器在要求输入密码等操作后就可以创建一个普通的用户，但有些时候，我们需要执行一些管理员才能操作的任务，比如重启服务，安装、更新应用等。所以我们需要给普通用户设置超级用户的权限，那样普通用户可以通过在命令之前加上`sudo`来执行管理员权限的操作了。

要完成这个操作，我们需要将新增用户添加到`sudo`用户组，默认情况下，Ubuntu 14.04中属于`sudo`组里的所有用户都可以执行`sudo`命令。
`gpasswd -a <username> sudo`

> Tips: [`adduser`和`useradd`之间的区别？](http://askubuntu.com/questions/345974/what-is-the-difference-between-adduser-and-useradd)


4. 其他操作
修改用户名： `usermod -l <new_username> <old_username>`
修改用户密码： `passwd <username>`
> Tips: [A command to list all users? And how to add, delete, modify users?](http://askubuntu.com/questions/410244/a-command-to-list-all-users-and-how-to-add-delete-modify-users)


#### 禁用root用户
> 注： 在执行此操作之前，必须要保证系统有其他登录访问系统的用户，否则没法再访问系统了。
可以直接通过root用户来执行：
`passwd -l root`
或者其他有管理权限的用户执行：
`sudo passwd -l root`


用户管理到这里就算基本完了，下面该讨论下如何通过ssh来远程访问服务器了，最后要保证我们的服务器上root用户是被锁定的，同时还保留一个具有管理权限的用户。



## 使用SSH来登录到远程服务器
### 什么是SSH？
SSH，也称Secure Shell，是用于安全登录远程系统的协议，通常用于访问Linux或类Unix的服务器。[OpenSSH Server](https://help.ubuntu.com/lts/serverguide/openssh-server.html)
其工作原理就是：使用ssh客户端程序连接到远程服务器的ssh服务。

### 安装与管理ssh服务端
1. 检查是否安装
`ps -e |grep ssh`
如果没有安装可以通过：
`sudo apt-get install openssh-server`来进行安装

2. 查看ssh服务的状态
`sudo service ssh status`

3. 启动、停止与重启
`sudo service ssh` 可以查看可用的命令。
启动：
`sudo service ssh start`
停止：
`sudo service ssh stop`
重启：
`sudo service ssh restart`


### 使用
`ssh <remote host>`
这里的 remote host可以是IP或者域名，也就是对应暴露在互联网上的服务器，如果该服务器提供了ssh服务，就会需要你提供账号和密码用于登录，当然，我们也可以使用
`ssh <remote_username>@<remote host>`

退出登录使用`exit`命令。

### 进阶部分
#### ssh服务端配置
在我们拥有了新用户之后，通过对ssh服务端的配置来提高安全性。
配置文件位于`/etc/ssh/sshd_config`，在配置之前，为了安全起见，我们最好备份下该文件：
`sudo cp /etc/ssh/sshd_config{,.bak}`，
配置修改后需要重启ssh服务才会生效。

1. 是否允许root用户远程登录
    `PermitRootLogin yes`
    对于Linux或类Unix系统，大家知道系统肯定存在root用户为了安全性，一般需要从系统上锁定root用户外，还需要禁止root用户通过ssh登录来避免暴力破解登录。
    `PermitRootLogin no`

2. 修改ssh连接端口
    `Port 22`， 默认ssh连接端口是22，我们可以使用非常规的端口来提高安全性。


#### 使用ssh密钥对登录
我们固然可以直接通过用户名密码来登录，但使用SSH密钥对的方式来登录更好。

密钥授权登录的工作原理是通过一对密钥（公有密钥和私有密钥）来实现的：
1. 私有密钥位于本地，也就是客户端，必须保证其安全和私有。
2. 公有密钥位于服务端。
3. 当我们想通过ssh密钥来登录的时候，服务端会创建一条信息，并用公有密钥加密后发送给客户端，该信息只有具有私有秘钥的客户端才能读取
4. 有私有密钥客户端通读取信息后返回给服务端用于确认的信息，服务端就可以确定该连接客户端是合法客户端。

那么我们怎么创建ssh秘钥对呢？
通常在本地创建：
`ssh-keygen -t rsa`

对于Windows系统的用户，建议安装[Git](https://git-scm.com/downloads) 同时集成到Windows操作系统的命令提示符中，因为Git命令行软件集成了很多Linux系统的应用，比如说这里的`ssh-keygen`， 执行命令后，会在`C:\Users\ax10\.ssh` 目录下生成`id_rsa`和`id_rsa.pub`两个文件。

然后需要将id_rsa.pub 文件上传到服务端。
第一种方法：
`ssh-copy-id <username>@<remote host>`
这里的`<username>`是指远程主机的用户名 `<remote host>`是远程主机IP或者域名，连接到服务器验证密码通过之后就`id_rsa.pub`文件就上传了。

第二种方法：
打开本地的`id_ras.pub`文件并复制其中的内容，登录服务器后，进入当前用户目录，比如我是以hexcola登录的，我进入的目录就是/home/hexcola。执行以下的命令
```
$ mkdir .ssh
$ chmod 700 .ssh
$ vi .ssh/authorized_keys
$ 在这里粘贴你刚刚复制的内容，保存，退出
$ chmod 600 .ssh/authorized_keys
$ exit
```

然后在本地就可以测试以下：
`ssh hexcola@<remotehost>` 就会发现，不再需要密码了。


## 额外：关于对入口的思考

