# 第一章： 安装

## 使用虚拟环境
https://www.develves.net/blogs/asd/2016-04-28-using-virtual-environments-nodejs/
https://pypi.python.org/pypi/nodeenv/


## 初始化项目
我们通常使用Express来开发网站应用，在初始化项目我们需要使用:
```bash
npm init
```

## 通过npm安装node.js模块
要安装express，使用如下命令

```bash
npm i express --save
```
> 这里的`i`表示 `install`，你完全可以写全了。

该命令会安装Express及其依赖并保存到`package.json`，可以通过node命令提示符然后导入express来检测是否安装成功。
```bash
$ node
>>> require('express')
>>>
```
如果看到输出了关于express的模块信息而不是 `Error: Cannot find module 'express'`，恭喜，我们可以进入下一个环节了，开始创建我们的第一个Web应用。


## Essentials
npm i express -g

express --version

locally
npm install express --save


app.js

```
var express = require('express');
var app = express();

app.get('/', function(req, res) {
    res.send('Hello Express');
});

var server = app.listen(3000, function(){
    console.log('Listening on port 3000');
});

```

## Create Routes
get
无参数
app.get('/aboutme', function(req, res) {
    res.send('@hexcola');
})

有参数
app.get('/who/:name?', function(req, res){
    var name = req.params.name;
    res.send(name + ' was here');
});

app.get('/who/:name?/:title?', function(req, res){
    var name = req.params.name;
    var title = req.params.title;
    res.send(name + ' was here');
});

完全匹配
app.get('*', function(req, res){
    res.send('bad route');
})


## Using Template
what you want ? Jade or EJS?
npm install ejs --save

```
app.set('view engine', 'ejs');
```

we will create a folder named views, and we crate a file name default.ejs

```
app.get('/', function(req, res){
    // it will search views folder, and find the default.ejs file  
    res.render('default');
});
```

btw, if you don't want templates stay in the views folder, you can set anything you want , just doing by this:

```
app.set('views', __dirname + '/whateveryouwant');
```
then, your template file should be in the whateveryouwant folder.

### Render template with data
res.render('default', {title: 'Home'});

in the default.ejs file
<%= title %>

some other same shit:
for loop, conditions

在概念上，我们可以认为template就是View，而数据就是Model，这样处理起来，是不是就很好理解？

### template partials
在views文件夹内我们创建一个partials的文件夹，然后在里面创建一个page的文件夹，然后在里面创建head.ejs, footer.ejs

那么在其他需要引用的页面：
<% include partials/page/head.ejs %>
基本概念就是打散页面，让其原子化

### Using locals
locals变量可以在不同路由，不同视图页面都能共享变量
app.locals.title  = 'whatever you want?'
获取方式和渲染模板时候传递参数的方式是一样的：
<%= title %>



## Modularizing our Routes
随着项目体积增大，或者出于组织方式，我们有时候需要将路由放到不同的文件中，例如常规的项目和验证路由，我们就可以分开。

创建routes文件夹
var routes = require('./routes);

那么原来在app.js 下的路由：
```
app.get('/', function(req, res) {
    res.render('template');
});

app.get('/about', function(req, res){
    res.render('template');
});
```
就可以换成在routes文件夹下创建index.js文件中：
```
exports.index = function(req, res){
    res.render('template');
}

exports.about= function(req, res){
    res.render('template');
}
```

同时，在app.js中，我们需要修改代码为：
app.get('/', routes.index);
app.get('/about', routes.about);


## Structuring Our Content
### 使用express generator
`sudo npm i -g express-generator`

进入我们的项目，
`express - e project`
e 表示我们将使用ejs视图引擎

使用generator很简单，但有了前面的基础，一起看起来顺理成章了。


在views文件夹内我们创建一个partials的文件夹，然后在里面创建一个content的文件夹
views
    |__ content
        |__ socialmedia.ejs
        |__ somethingelse.ejs
        |__ 
        |__ ...
    |__ templates
        |__ header.ejs
        |__ footer.ejs
        |__ head.ejs
        |__ jsdefault.ejs
        |__ ...
    |__ err.ejs
    |__ index.ejs

JSON Online Editor

## Importing data
对于Node.js来说，可以直接像模块一样直接导入文件。
var data = require('./data.josn')
这将导入数据作为一个对象，存储在data中，当然我们也可以这样：
app.local.data = require('./data.json');
这样我们所有的页面都可以访问。


访问数据的方式：
1. 通过app.locals
2. 通过路由传递


Font Awesome

What's Next

Recommond books
Node for Front-End Developers
Learning Node
Node.js in Action


## 使用yo express

```bash
yo express
? Would you like to create a new directory for your project? No 
? Select a version to install:
    Basic
>   MVC

? Select a view engine to use:(Use arrow keys)
    Jade
    Swig
    EJS
    Handlebars
    Marko
>   Nunjucks

? Select a css preprocessor to use (Sass Requires Ruby): (Use arrow keys)
    None
    Node-Sass
    Sass
>   less
    Stylus

? Select a database to use: (Use arrow keys)
    None
>   MongoDB
    PostgreSQL
    RethinkDB
    SQLite

? Select a build tool to use: (Use arrow keys)
    Grunt
>   Gulp

````

这里我们选择了MongoDB作为数据库， 默认会连接到`mongodb://localhost/stephub-development`，所以，我们只要在本地启动Mongo服务器就可以了。

* 选择模式MVC
* HTML Template：Nunjucks
* CSS Compiler：LESS
* 任务自动化：Gulp

以上设置完成后会自动安装node modules
在命令行中运行`gulp`然后打开 localhost:3000/ 就可以看到：

