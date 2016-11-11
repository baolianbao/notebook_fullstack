---
title: Node.js essentials
date: 2016-08-15 15:12:00
tags:
categories: fullstack
---

## 什么是NodeJS？

## 用Node.js做什么？
### 工具
* gulp
* sass？
* hexo
### Web服务器


## 模块
### 自己怎么管理模块，导出，导入
### npm怎么管理模块


1. 安装Node.js
2. 创建项目文件夹 todo，进入todo文件夹，使用node init
3. 安装express, npm i -S express
4. 全局安装webpack： sudo npm install -g webpack webpack-dev-server
    npm i -D webpack webpack-dev-server 使用开发版本
    sudo npm i -D babel-loader babel-preset-es2015

在package.json文件中删除"test":"echo\ Error..."
使用
"start" : "NODE_PATH=$NODE_PATH:./src node server",
"dev": "npm start & webpack-dev-server --progress --colors"

ctrl + C，断开，运行npm run dev
如果报错，则可能是ctrl + c 没有完全关闭，可以使用`killall -9 node`

接下来设置Angular和UI Router
`npm i -S angular angular-ui-router`
`npm i -D raw-loader`

创建config.js


## Node.js 应用是由哪几部分组成的：
* 引入 required 模块：我们可以使用 require 指令来载入 Node.js 模块。
* 创建服务器：服务器可以监听客户端的请求，类似于 Apache 、Nginx 等 HTTP 服务器。
* 接收请求与响应请求 服务器很容易创建，客户端可以使用浏览器或终端发送 HTTP 请求，服务器接收请求后返回响应数据。


这个时候，我们需要了解下Web工作的基本原理。

从发送请求到，响应。

require一个模块，是否会实例化并返回一个值？


## 关于NPM
常见的使用场景有以下几种：
* 允许用户从NPM服务器下载别人编写的`第三方包`到本地使用。
* 允许用户从NPM服务器下载并安装别人编写的`命令行程序`到本地使用。
* 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。


### 安装
`npm install <module name>`

安装的两种方式：本地安装与全局安装，

Windows下全局安装到哪里？
`C:\Users\ax10\AppData\Roaming\npm`

### 移除
`npm uninstall <module name>`

### 查找
`npm ls -g`

可以这样认为，所有的Node项目最终都是一个模块，每个模块可能包含一个或者多个第三方模块，那么每个模块都需要一个包含对模块解释的文件，也就是package.json文件，它必不可少。
可以使用`npm init`来进行初始化。

* name - 包名。
* version - 包的版本号。
* description - 包的描述。
* homepage - 包的官网 url 。
* author - 包的作者姓名。
* contributors - 包的其他贡献者姓名。
* dependencies - 依赖包列表。如果依赖包没有安装，npm 会自动将依赖包安装在 node_module 目录下。
* repository - 包代码存放的地方的类型，可以是 git 或 svn，git 可在 Github 上。
* main - main 字段是一个模块ID，它是一个指向你程序的主要项目。就是说，如果你包的名字叫 express，然后用户安装它，然后require("express")。
* keywords - 关键字


在npm里登录自己的ID
`npm adduser`

发布自己的模块
`npm publish`


## 版本号
使用NPM下载和发布代码时都会接触到版本号。NPM使用语义版本号来管理代码，这里简单介绍一下。
语义版本号分为X.Y.Z三位，分别代表主版本号、次版本号和补丁版本号。当代码变更时，版本号按以下原则更新。
如果只是修复bug，需要更新Z位。
如果是新增了功能，但是向下兼容，需要更新Y位。
如果有大变动，向下不兼容，需要更新X位。
版本号有了这个保证后，在申明第三方包依赖时，除了可依赖于一个固定版本号外，还可依赖于某个范围的版本号。例如"argv": "0.0.x"表示依赖于0.0.x系列的最新版argv。
NPM支持的所有版本号范围指定方式可以查看官方文档。


## NPM 常用命令
除了本章介绍的部分外，NPM还提供了很多功能，package.json里也有很多其它有用的字段。
除了可以在npmjs.org/doc/查看官方文档外，这里再介绍一些NPM常用命令。
NPM提供了很多命令，例如install和publish，使用npm help可查看所有命令。
NPM提供了很多命令，例如install和publish，使用npm help可查看所有命令。
使用npm help <command>可查看某条命令的详细帮助，例如npm help install。
在package.json所在目录下使用npm install . -g可先在本地安装当前命令行程序，可用于发布前的本地测试。
使用npm update <package>可以把当前目录下node_modules子目录里边的对应模块更新至最新版本。
使用npm update <package> -g可以把全局安装的对应命令行程序更新至最新版。
使用npm cache clear可以清空NPM本地缓存，用于对付使用相同版本号发布新版本代码的人。
使用npm unpublish <package>@<version>可以撤销发布自己发布过的某个版本代码。



## REPL
命令行里输入Node


## 关于回调函数

阻塞函数就是按序执行，同步编程
非阻塞就是不按序执行，异步编程，依赖于回调函数(callback)


http://www.nodebeginner.org/index-zh-cn.html