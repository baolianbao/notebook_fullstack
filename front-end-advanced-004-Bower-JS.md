title: Web开发：使用Bower.js进行包管理 
date: 2016-01-06 21:34:06
tags: bower
---

## 为什么使用Bower？

Web开发会依赖很多

## How

安装
```bash
npm install bower -g
```
<!--more-->

## 使用
###使用其安装最新包
```bash
bower install <package name>
```
 
### 使用其安装指定版本包
```bash
bower install <package name>#<version>
```

### 删除安装的包
```bash
bower uninstall <package name>

### 列举已经安装的包
```bash
bower list
```
 
### 列举已经安装的包所在路径
```bash
bower list --paths
```
 
### 团队协作

在团队协作时候，不希望把把依赖的包文件都提交上去（当然，为了你的项目即使在很久以后都可以运行，最好提交，或者在企业内部建立Git库），那么可以创建Bower配置文件
```bash
bower init
```

根据情况进行配置，会生成bower.json文件，那么团队在拿到该项目后可以直接安装所需要的包
```bash
bower install
```
 
如果在生成bower.json文件之后再安装新的包时候，也需要将新安装的包的依赖添加的bower.json文件中，
```bash
 bower install <package name veresion> -S
(S必须大写)
 ```
