title: Vagrant For Beginner
date: 2016-03-28 13:38:13
tags:
---
Download Vagrant: https://www.vagrantup.com/downloads.html

使用 Vagrant 打造跨平台开发环境 https://segmentfault.com/a/1190000000264347


vagrant 需要至少两个文件：
1. box
2. vagrantfile


让Vagrant在Windwos下支持使用NFS/SMB共享文件夹从而解决目录共享IO缓慢的问题
http://www.iamle.com/archives/2011.html


## 怎么制作box
>vagrant package --output vvv.box


## Workspace
vagrant destroy             // tear down
vagrant up --no-parallel    //rebuild the system
vagrant ssh