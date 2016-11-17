title: Web开发：Grunt 
date: 2016-01-06 21:34:06
tags: grunt
---

## Grunt是什么？

## 为什么需要Build System？
<!--more -->
### Build System 用来做什么？
* 重复性的任务
        - 合并Javascript，CSS之类的（）Concatenating JavaScript
        - Prefixing CSS

* Utilities
        - JSHint
        - Uglify(Compress/minify) JavaScript,CSS

* Local Server
* Live Reload

### 对用户有什么好处？
* Page Speed
        - Less file request for page load
        - Faster file requests

* Development Workflow
        - You can use cool technologies(e.g. SASS, LESS, etc)
        - You can break code into multiple files
        - Easier to avoid code conflicts
        - You can avoid annoying, repetitive tasks.

* 节省访问资源和时间
        - Vendor code
        - Application Code


### 现在有哪些工具？
* GRUNT
* GULP

## 如何使用Grunt？
### 安装
```bash
npm install -g grunt-cli
```
在项目中添加grunt
```bash
npm install grunt -S
```
此外还需要在项目中创建Gruntfile.js，Grunt是Task Runner，那么就让它运行一些Task。

### 运行常规的Task
#### 添加一个Task
文件：Gruntfile.js
```js
 module.exports = function(grunt){
  // create some tasks to run.
  grunt.registerTask("speak", function(){
    console.log("I'm Speaking");
  });
}
```
测试：
```bash
 grunt speak
```

#### 再添加一个Task
文件：Gruntfile.js
```js
 module.exports = function(grunt){
  // create some tasks to run.
  grunt.registerTask("speak", function(){
    console.log("I'm Speaking");
  });

  grunt.registerTask("yell", function(){
    console.log("I'm Yelling!");
  });
}
```
测试：
```bash
grunt speak

grunt yell
```

#### 同时运行两个Task
文件：Gruntfile.js
```js
module.exports = function(grunt){
  // create some tasks to run.
  grunt.registerTask("speak", function(){
    console.log("I'm Speaking");
  });

  grunt.registerTask("yell", function(){
    console.log("I'm Yelling!");
  });

  grunt.registerTask("both", ['speak', 'yell']);
}
```

测试：
```bash
grunt both
```

#### 运行默认的Task
文件：Gruntfile.js
```js
module.exports = function(grunt){
  // create some tasks to run.
  grunt.registerTask("speak", function(){
    console.log("I'm Speaking");
  });

  grunt.registerTask("yell", function(){
    console.log("I'm Yelling!");
  });

  grunt.registerTask("default", ['speak', 'yell']);
}
```
测试：
```bash
grunt
```

### 如何使用Plugins
[Plugins](http://www.hexcola.com/2016/01/06/WEB-JS-Grunt-JS/#Grunt_u91CC_u7684Plugins_u662F_u4EC0_u4E48_uFF1F)是什么？"
> Grunt里的[Plugins](http://gruntjs.com/plugins)是什么？

#### [grunt-contrib-concat](http://www.hexcola.com/2016/01/06/WEB-JS-Grunt-JS/#u4F7F_u7528_grunt-contrib-concat)
>使用 [grunt-contrib-concat](https://www.npmjs.com/package/grunt-contrib-concat)

##### 安装
```bash
npm install grunt-contrib-concat --save-dev
```

##### 使用
所有loadNpmTasks的任务都在
``` js
grunt.initConfig({
  // tasks
  });

grunt.initConfig({
  concat:{
    js: {
      src: ['js/1.js', 'js/2.js'],
      dest: 'build/js/scripts.js'
    },
    css:{
      src: ['css/main.css', 'css/theme.css'],
      dest: 'build/css/styles.css'
    },
  },
})

grunt.loadNpmTasks('grunt-contrib-concat')
```

##### 测试
```bash
grunt concat
```

#### [grunt-contrib-watch](http://www.hexcola.com/2016/01/06/WEB-JS-Grunt-JS/#u4F7F_u7528_grunt-contrib-watch)

>使用 [grunt-contrib-watch](https://www.npmjs.com/package/grunt-contrib-watch)

在当前的例子中，每次我们修改了JS或者CSS文件，不想都手动运行concat任务，我们可以使用watch来监控文件，一旦文件发生改动，就让它执行concat方法。
##### 安装

```bash
npm install grunt-contrib-watch --save-dev
```

##### 使用
```js
grunt.initConfig({
  concat:{
    js: {
      src: ['js/1.js', 'js/2.js'],
      dest: 'build/js/scripts.js'
    },
    css:{
      src: ['css/main.css', 'css/theme.css'],
      dest: 'build/css/styles.css'
    },
  },
  watch:{
    js: {
      files: ['js/**/*.js'],
      tasks: ['concat:js'],
    },
    css:{
      files: ['css/**/*.css'],
      tasks: ['contact:css'],
    },
  },
})

grunt.loadNpmTasks('grunt-contrib-concat');
grunt.loadNpmTasks('grunt-contrib-watch');
grunt.registerTask('default', ['concat', 'watch'])
```
##### 测试
```bash
 grunt watch
```

[GRUNT TUTORIAL - Grunt makes your web development better!](https://www.youtube.com/watch?v=TMKj0BxzVgw)