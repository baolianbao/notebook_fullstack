title: 拥有自己的Ubuntu 14.04服务器
date: 2016-03-12 17:31:13
tags: ubuntu
---


主要有两种方式来获取Ubuntu 14.04服务器：
1. 购买云服务器，选择Ubuntu 14.04操作系统
2. 本地搭建服务器




## 购买云服务器
这个我们有很多选择。
根据服务器的CPU、内存、带宽配置等等标准价格不等

## 本地搭建服务器
更多是用于本地开发测试，也有两种选择
1. 个人通过虚拟机安装，用于开发测试
2. 安装到物理主机，适合团队协作开发测试

然而这两种选择在安装和配置上几乎没有差异，所以就不拆开讨论，而是直接通过虚拟机安装展开，既然最终我们的项目是要部署到购买的云服务器上，我们就要尽量使本地的环境和云服务相似。
条件：
* CPU：	1核
* 内存：	2048M
* 硬盘：	20G
* 带宽：	1Mbps
* 默认用户： root（需要在登录后重新设置密码等）


### Step 1 下载安装VirtualBox
下载链接：[Oralce VM VirtualBox](https://www.virtualbox.org/wiki/Downloads)
根据自己主机的操作系统选不同的VirtualBox安装文件然后安装。

### Step 2 下载镜像文件

下载链接： Ubuntu Server 14.04 [i386](http://releases.ubuntu.com/14.04/ubuntu-14.04.4-server-i386.iso.torrent) / [amd64](http://releases.ubuntu.com/14.04/ubuntu-14.04.4-server-amd64.iso.torrent)镜像文件。
根据自己的情况决定使用32位/64位。


### Step 3 在VirtualBox中新增虚拟机并配置

### Step 4 开始安装

选用桥接模式可以确保虚拟机和主机处于同一个局域网。
之后我们可以通过

这里需要我们直接创建一个新的用户，和一些云服务器初始化使用的时候直接使用root登录不同，


我们也需要安装OpenSSH Server，确保我们可以在服务器安装好以后可以通过ssh客户端远程登录到服务器。


VirtualBox会自动弹出镜像文件，所以直接下一步。


至此，我们就拥有了一台Ubuntu 14.04的服务器了。 

我们可以将其作为一个基础环境做个备份，在之后的操作里先拿它做实验，如果失败了，可以直接删除，复制一份备份文件来使用， 这就有点像阿里云服务器中的Snapshot了，我们可以创建多个以供在不同的情况下使用。

Q : [如何调整Ubuntu Server的分辨率问题](http://blog.csdn.net/amymengfan/article/details/9854963)

[Linux 關機指令（shutdown、halt 與 poweroff）教學與範例](http://blogger.gtwang.org/2013/10/how-to-shutdown-linux.html)


* 下一篇： [Ubuntu 14.04 Server基本配置Additional Recommended Steps for New Ubuntu 14.04 Servers](https://www.digitalocean.com/community/tutorials/additional-recommended-steps-for-new-ubuntu-14-04-servers)






