---
title: JavaScript 01 快速入门
date: 2016-08-15 07:20:00
tags: [javascript]
categories: fullstack
---

JavaScript核心与语法
放哪儿
有什么工具可以使用

然后使用：
1. Forms
2. Events
3. DOM
4. Debug
5. Libraries: jQuery
6. Other advanced topics: 
7. Best Practices

 ## What you should know
 * HTML and CSS
 

 ## Introduction to JavaScript
 for behavior of user interactive

 什么是Scripting Language
 配合JavaScript引擎使用，如果在浏览器端使用：
 * 无法访问本地文件
 * 无法直接访问数据库
 * 无法访问硬件（USB，等等）

JavaScript创建之初是在浏览器上使用的，但现在有了其他用途：
* Application： Acrobat / Photoshop / Unity 3D 
* Server-side：Node.js / Google Apps Script

### 作为客户端语言的问题：
* 当JS作为客户端语言时，是由服务器发送个客户端执行的，如果用户禁用了JS，那么结果和我们没有写JS没有区别，这个时候，我们需要保证我们的页面即使没有JS也要能正常运行。
* 不同的浏览器对JS的支持程度不一，以前需要检查不同浏览器并使用不同的方法，现在不需要太担心这个问题，这就需要了解下JS的简单历史：
1995            1996            1999
LiveScript      JavaScript      ECMAScript 3
                NetScape2

第五集


```js
alert('Hello world');
```

## JavaScript Tools
就用Visual Studio Code + Google Chrome 吧
查看各大浏览器市场份额
FF + Firebug
在console中：alert('hello world');

## JavaScript Structure
### JavaScript is Interpreted
JavaScript区分大小写！


## JavaScript放哪儿？
小段测试，放HTML文档里没事儿，项目大，放到另外的文件然后引用：

```HTML
<script src="myscript.js"> </script>
```
在HTML5里`script`标签的type属性没必要，因为它默认是"text/javascript"

尽量放到</body>之前以免影响HTML加载。

## 变量
就是容器，从内存中占用一点，给它命名用来存放内容。

`var variable`
变量名可以是字符，数字，下划线，$
var year;
var month;
var day;
=
var year, month, day;

或者：
var year = 2016;
var month = 9;
var day = 12;

=

var year=2016， month = 9, day = 12;
JavaScript是弱类型的，赋值后推测数据类型
var maVariable = true;

## 条件
if ( condition ) {
    // do somthing here
} else {
    // otherwise
}

术语：
* ( parentheses )
* [   brackets  ]
* {   braces    }

它们只是用来表示从哪儿开始和结束，而不具有实际意义

## 运算符合表达式
* 算术运算符 
  符合四则运算规则 + - * /  = += -= *= /=
* 比较运算符
  > < == === != !== >= <=
  这里有个陷阱：
  
  ``` javascript
  var a = 5;
  var b = 10;
  if ( a = b ){
      // always true!
  }
  ````
  上面的代码，没有使用 `==` 或者 `===`比较运算符，而是使用了 `=`赋值运算符，结果就是永远是true。

这个错误很难检测！！ 所以一定要小心。
`===`是严格检测（值和类型）是否相等
`==` 只会检测值，例如5和 '5' 结果是相等的。

* 逻辑运算
  AND: && 
  OR : ||
  NOT: !

* 取模运算
  %

* 递加递减运算
  ++ --
  a++;
  ++a;

``` js
var a = 5;
alert (++a); // 6
```
``` js
var a = 5;
alert(a++); // 5
```

* 三元运算符：
condition ? true : false


## console
console.log
console.debug
console.info
console.warn
console.error

## 循环
* while
* do ... while 
* for 
* break 结束整个循环
* continue 结束当前循环，继续下一个

## Function 函数
* function 
function name(){
    // do what  
}

好的方式是先定义函数然后再调用，虽然先调用也可以。
参数：
参数不匹配？！

变量域：local & global

## 数组
var multipleValues = [];
multipleValues[0] = 50;
multipleValues[1] = 60;
multipleValues[2] = "Mouse";

简写：
var multipleValues =[50, 60, "Mouse"];

高级：
var multipleValues = new Array(); //数组是对象
var multipleValues = Array(5);
JS里所有数组都是动态的，没有固定长度。
正是由于数组是对象，它便有了属性：
.length
同时它也有些方法：
.join();
.sort();
.append();
.reverse()
.splice();
.foreach(function(item){

});
...

几乎到哪儿都是JS数组：
var myArrayOfLinks = document.getElementsByTagName("a");

## 数值
什么类型的数值，整数？浮点数？JS中所有的数值都是64位浮点数。
Addition VS Concatenation

var foo = "55"; // could be "abc"
var myNumber = Number(foo); //如果是abc那么 myNumber就是NaN
if ( isNaN(myNumber)){
    console.log("It's not a number!");
}

使用Math对象
var x = 200.6
var y = Math.round(x); // 201

var a = 200, b = 10000, c = 4;
var biggest = Math.max(a,b,c);
...

## 日期
这也是内置对象
var today = new Date(); // current data and time

// year, month, day
var y2k = new(2000, 0, 1);// month is 0-index
它也有方法：
#### GET 
.getMonth();
.getFullYear();
.getYear(); //deprecated
.getDate(); // 1-31 day of month
.getDay(); // 0~6 day of week, 0 is sunday
.getHours(); // 0-23
.getTime(); // milliseconds since 1/1/1970

#### SET

#### 比较日期
var d1 = new Date(2000, 0, 1);
var d2 = new Date(2000, 0, 1);

if(d1 == d2)  // false这仅仅是比较这两个是否是一个对象？很显然不是
if (d1.getTime() == d2.getTime()) // true

## 对象 Object
数组，日期都是对象，一旦我们接触Web技术，我们就会遇到其他对象：document，window...

### 创建对象
var player = new Object(); // 这就是个容器
player.name = "Fred";
player.score = 100000;
player.rank = 1;

简写：
var player1 = {name: "Fred", score: 10000, rank:1 };
如果还想给对象添加方法呢？
function playerDetails(){// display
    console.log(this.name); // 这里的this是指当前函数链接的对象
}

player1.logDetails = playerDetails;
将对象方法和我们之前创建的函数建立联系。然后就可以通过对象来调用：
player1.logDetails();

暂时我们不需要OOP，也就是关于Prototyp那一套。

## DOM
我们的脚本需要和Web页面相关，那么DOM是什么？

Document    Object      Model(DOM)
web page    pieces      agreed-upon set of terms