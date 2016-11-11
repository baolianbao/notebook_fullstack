## 为啥需要workflow management?

## 为什么使用Workflow 工具？
 * 加快开发速度
 * 自动化任务
 * Handle processed languages
 * 提升网站访问速度

## 工具类型 
### 内置工具
* 编辑器（语法高亮，语法检查，格式化，主题等等）
### 开源工具

node.js
npm
glup
browserify
ruby
gem
sass
compass

## 创建package.json文件
进入项目文件夹，`npm init`
关于什么是Semantic Version ？

## 安装gulp
全局安装
项目也需要安装
`npm i --save-dev gulp`
创建`gulpfile.js`，用来告诉gulp干啥

```js
var gulp = require('gulp')
    gutil = require('gulp-util');

gulp.task('log', function(){
    gutil.log('workflows are awesome');
});
```

仅仅安装gulp还不够，我们还需要一些其他的包来完成一系列的任务：
例如：
* `gulp-util`

然后在命令行里运行：`gulp log`就可以看到结果啦！

例如专门处理coffeeScript的gulp插件：
* `gulp-coffee`

```js
var gulp = require('gulp')
    gutil = require('gulp-util'),
    coffee = require('gulp-coffee');

gulp.task('coffee', function(){
    gulp.src('components/coffee/tagline.coffee')
        .pipe(coffee({ bare: true })
            .on('error', gutil.log))
        .pipe(gulp.dest('components/scripts'))
}); 
```
这里主要强调gulp的管道方式，比如src作为输入源，用pipe输送给另外的程序处理，知道最后输出。

当然，这里有几个问题：
1. bare是什么鬼？
http://coffeescript.org
2. 优化路径：

```js
var coffeeSource = ['components/coffee/tagline.coffee'];

...
gulp.src(coffeeSource)
    .pipe...
```

### 合并JavaScript
流程是一样的：
首先找完成该任务的依赖包，这里是`gulp-concat`
 

## 通过Browserify导入库（jQuery）
`npm i --save-dev gulp-browserify`

然后还需要安装需要的库：

```bash
npm i --save-dev jquery
npm i --save-dev mustache
```
http://browserify.org/