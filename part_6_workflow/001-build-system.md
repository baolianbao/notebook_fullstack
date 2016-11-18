# 创建Build System
## Build System是什么？
A build system is simply a collection of tasks(commonly called "task runners") that automate repetitive work.

那么这些任务是什么呢？
* 编译sass
* 转换JS，拼接，压缩
* 启动Web服务器
* 自动刷新浏览器
* 自动发布到服务器

build System需要与其他工具协作，例如包管理器(package manager)

简单看看现在的工作流所需要的组件

我们可能常见的三大组件：
* Package manager 
* Preprocessors
* Task Runner & Build Tools

## Package manager
例如：Bower， npm
主要的职能安装，卸载，升级项目所需要的依赖包或库，项目里有可能需要两个包管理器：
Bower：用于管理前端依赖，例如：jQuery， Backbone， Angular
NPM：用于管理后端开发环境依赖，例如：Gulp， Browser-Sync，Plumber等等

## Preprocessors
什么是Preprocessors呢？
Processors are critical to an efficient modern workflow by adding additional features and an optimized syntax that compiles into its native language.

* CSS: Sass, Less, Stylus
* JavaScript: CoffeeScript, Typescript, Babel
* HTML: HAML, Jade, Markdown, Slim

## Task Runners & Build Tools
例如：Gulp，Grunt
经典的Gulp脚本结构，往往分为四个部分

### 第一步：Required Modules
声明所需要的依赖模块

```js
var gulp = require('gulp');
var uglify = require('gulp-uglify');
```

### 第二步：定义各种任务
这就是实际所需要的完成的任务了：
* 压缩静态图片
* 复制文件
* 发布

```js
// 创建一个名为scripts的任务
gulp.task('scripts',function(){
    // code
});
```

然后要执行该任务的时候就是：`gulp scripts`

### 第三步骤：可选，监控 Watch

```js
gulp.task('watch', function(){
    gulp.watch('app/js/**/*.js', ['scripts']);
})
```
监视任务，上面的代码就是检测js文件夹内的所有.js文件，如果有变化就执行`scripts`任务 

### 第四步：默认任务
可以将其视作用其他任务的入口，例如代码：

```js
gulp.task('default', ['scripts', 'watch']);
```

那么我们执行`gulp`命令时就会同时运行`scripts`和`watch`任务。

## 创建项目环境
### 基本文件结构
```bash
mkdir app
cd app
mkdir image js css scss
touch index.html js/main.js scss/style.scss
```

如何在命令行里使用VSC打开当前文件夹。

### 设置git
```bash
touch readme.md .gitignore
```
在gitignore里往往不需要上传的内容：查看gist

```bash
git init
git add .
git status
git commit -m "first commit"
git log --oneline
```

### 使用bower
首先全局安装
`npm i bower -g`

然后进入app文件夹，首先初始化bower配置文件：
`bower init`
一路回车，然后在app目录下就出现了bower.json文件了，然后可以使用bower 来安装一些依赖：
`bower install jquery angualr backbone --save`
安装结束后会发现在app目录下多了bower_components目录，且里面有我们安装的依赖包以及这些包所依赖的文件，同时在`bower.json`配置文件会增加了依赖项，那么我们即使删除了`bower_components`，也可以通过`bower install`来重新安装所有依赖的包。

* 查看安装了哪些包：
`bower list`
* 卸载包
`bower uninstall jquery --save`
这样就会从`bower.json`和`bower_components`中移除和`jquery`相关的内容。

* 如何在HTML中引用这些包
`bower list --paths`
会列出所有安装的包以及对应的路径，那样我们就可以直接在script中引用，例如：

```html
    <script src="bower_components/jquery/dist/jquery.js"></script>
```


## Compass设置 可选项
### gulp-sass
为啥老提到susy, breakpoint，这是个什么鬼？
mac默认安装了ruby
`sudo gem install compass`

compass -v 
gem list 

然后还要安装susy, breakpoint 

```bash
sudo gem install susy
sudo gem install breakpoint 
```
在项目的根目录下创建`config.rb`配置文件，他奶奶的依赖ruby



## 安装Gulp

```
npm install -g gulp
```

然后使用npm在项目根目录下创建配置文件（不是app目录下哦！）：
```
npm init 
```

然后安装gulp
```
npm i gulp --save-dev
```

创建gulpfile.js


好了，到这里创建项目结构任务就算是完成了，太特么无聊了！


## Gulp文件
