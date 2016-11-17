title: Handlerbars.js学习
date: 2015-12-15 20:54:44
tags: handlerbars
---


![handlebars.js](https://raw.githubusercontent.com/hexcola/blog/master/source/_images/web/handlebarsjs/01/01.jpg)

<!--more-->
# 什么是Handlebars.js？
**[Handlebars.js]** (http://handlebarsjs.com/)是款比较流行的模版引擎，功能强大，简单易用，社区支持很好。使用Handlerbars，可以从JavaScript代码中将单独生成的HTML分离。

# 将Handlerbars.js添加到项目中去
## CDN
```js
// From CDN
<script src="https://cdnjs.cloudflare.com/ajax/libs/handlebars.js/4.0.5/handlebars.js"></script>
```

## 下载文件
到 [http://handlebarsjs.com/]( http://handlebarsjs.com/) 下载最新的文件，引用到自己的项目中去。
问题：[Handlebars.js 和 Handlebars.runtime.js的区别](http://stackoverflow.com/questions/19147161/what-is-the-difference-between-handlebar-js-and-handlebar-runtime-js)
```js
// From local
<script src="js/handlebars-v4.0.5.js"></script>
```

# 模版
js文件引入后，就可以创建模版了，推荐的用法是，将模版内容添加到`<script>`标签中，需要注意的是标签中需要加入一个属性`type`其值为`text/x-handlebars-template`，该属性非常重要，不加的话浏览器会默认该标签内的内容是JavaScript，但事实上并不是。
```js
<script id="YourID" type="text/x-handlebars-template">
  <!--模版内容-->
</script>
```
模版的语法非常简单，其中可以将HTML，普通文本与Handlebars表达式混合，表达式通过`\{\{  \}\}` 或者 `\{\{\{ \}\}\}`包裹起来，表达式可以告诉Handlebars导入变量值或者执行Helper函数。

模版在用之前需要将其编译成JavaScript脚本，通过GitHub上示例代码 [example01_templates](https://github.com/hexcola/HandlebarsForBeginner/tree/master/example01_templates) 就可以明白。
> 注意：在代码中我使用了jquery, 需要指明的Handlerbars.js并不依赖于jquery，纯JavaScript就可以实现我们想要的功能，使用jquery是为了方便。[Does Handlebars require jQuery](http://stackoverflow.com/questions/30950150/does-handlebars-require-jquery)

# 表达式
上面说过表达式通过`\{\{  \}\}` 或者 `\{\{\{ \}\}\}`包裹起来，其实它们之间有区别的，
* `\{\{ \}\}` 为了安全考虑，所有输出的内容不包括HTML本身
* `\{\{\{ \}\}\}` 可以输出原生的HTML代码

所以用法得看具体的需求了。

与此同时，handlebars的表达式也支持内嵌值的获取，这个特性可以让我们获取JavaScript对象的值。
具体的示例可以查看GitHub上示例代码 [example02_expressions](https://github.com/hexcola/HandlebarsForBeginner/tree/master/example02_expressions)

# Context
the object where properties you include in curly braces are looked up. Every template you write has a context. On the top level, this is the JavaScript object that you pass to the compiled template. But helpers like #each or #with modify it, so that you can access the properties of the iterated object directly. The next example will make things clearer.

另外，将编译好的Html代码添加到页面中也可以直接追加到`body`中去：
```
$(document.body).append(theCompiledHtml);
```
> Tip：在模版中的注释方式是使用`<!---->`

具体的示例可以查看GitHub上示例代码 [example03_context](https://github.com/hexcola/HandlebarsForBeginner/tree/master/example03_context)

# Helper
Handlebars不允许直接在模版中写JavaScript代码，对应的，它提供了Helper，也就是一些可以在模版中调用的JavaScript函数，可以帮助我们在建立复杂的模版时，复用代码。
调用Helper，只需要`\{\{HelperName\}\}`就可以了，当然可以可以通过 `\{\{HelperName Params\}\}`来调用Helper并传递参数。
除了一些[内建Helper](http://handlebarsjs.com/builtin_helpers.html)外，我们可以自己创建Helper，需要使用[`Handlebars.registerHelper(name, helper) `](http://handlebarsjs.com/reference.html#base-registerHelper) 函数

具体的示例可以查看GitHub上示例代码 [example04_helpers](https://github.com/hexcola/HandlebarsForBeginner/tree/master/example04_helpers)

# Helper块
[Helper块](http://handlebarsjs.com/block_helpers.html)和普通的Helper类似，只不过他们有对应的开始结束标签（比如 `\#if` ，`\#each` 这些内置Helper）， 这些Helper可以修改其包裹的HTML及其内容。虽然创建的时候不太容易，是功能非常强大，我们可以使用它们来复用一些功能或者创建大块的HTML代码（比如通讯录人员列表）。

创建Helper块，依旧需要使用[`Handlebars.registerHelper(name, helper) `](http://handlebarsjs.com/reference.html#base-registerHelper) 函数。与之前不同的是，我们需要使用该函数的callback函数的参数 `options`，它对外暴露了一些需要用到的属性值。

具体的示例可以查看GitHub上示例代码 [example05_block_helpers](https://github.com/hexcola/HandlebarsForBeginner/tree/master/example05_block_helpers)

# 参考
* [Learn Handlebars in 10 Minutes or Less](http://tutorialzine.com/2015/01/learn-handlebars-in-10-minutes/)
* [andlebars.js Tutorial: Learn Everything About Handlebars.js JavaScript Templating](http://javascriptissexy.com/handlebars-js-tutorial-learn-everything-about-handlebars-js-javascript-templating/)
* [Handlebars Helpers ](https://github.com/assemble/handlebars-helpers)
* [SWAG](https://github.com/elving/swag)
* [Handlebar Reference](http://handlebarsjs.com/reference.html)
* [Handlebars.js初级教程：学习Javascript模板Handlebars.js（二）](http://www.html-js.com/article/The-Javascript-template-of-Handlebarsjs-junior-tutorial-learning-Javascript-template-Handlebarsjs-two)

-------------
> 欢迎关注公众号：hexcola
>
>![qrcode](https://raw.githubusercontent.com/hexcola/blog/master/source/_images/profile/qrcode.jpg)
