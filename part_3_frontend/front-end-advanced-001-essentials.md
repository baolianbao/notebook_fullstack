---
title: Web Workflow
date: 2016-08-30 20:28:28
tags:
---

## Install Requiments
* Git
* Node
    - `sudo npm i -g gulp`
    - `sudo npm i -g browserify`
* Ruby
    - `sudo gem install sass`
    - `sudo gem install compass`


## 创建package.json文件
创建项目workflows，并在terminal下切换到该目录，使用`npm init`来创建`package.json`文件
git : ?.git

## 添加资源文件
目录结构：
workflows
    |_ builds
        |_ development
            |_ images
            |_ css
            |_ js 
            |_ index.html
        |_ production
    |_ components
        |_ coffee
        |_ sass
        |_ scripts
    |_ package.json
