---
title: JavaScript 和 JSON
date: 2016-08-15 10:20:00
tags: [javascript, json]
categories: fullstack
---

### What is JSON
JavaScript对象与JSON很容易混淆，就讨论下什么是JSON，以及其在处理数据上的优势。
JSON是JavaScript Object Notation的缩写，它是格式化的文本，易于传递，例如在服务器和客户端之间 。
由JavaScript派生出来的，且和JavaScript对象很像，但不完全相同 。尽管和JavaScript有很大的相似性，但却是独立于编程语言，像C，Ruby， Perl，Python，PHP等等都有和JSON交互的方式。 和XML alternative

#### 优势
易读（键值对） —— 对人
```
var data = 
{
    "name"      : "Neo Yang",
    "position"  : "China",
    "hobby"     : [
        "Read",
        "Sleep",
        "Eat"
    ]
}
```
易于转换和读取    —— 对计算机
```
var info = JSON.parse(data);
info.name
info.position
```

比XML体积更小
API支持程度更高，编程语言支持多。

* Format for sharing data
* Derived from JavaScript
* Language Independent

### Understanding objects and JSON
尽管它是由JSON格式是由JavaScript派生的，也很像JavaScript对象，但它们之间有区别的：
在写JavaScript应用的时候，我们需要处理JavaScript对象和JSON，

JSON：
JSON 的键必须使用引号
JSON的键可以是任何合法的字符串，也就是使用空格，特殊字符等，但一般不建议使用
JSON的值类型必须是以下六种数据类型之一：string，number，object，array， boolean， null


JavaScript对象可以是任何JavaScript结构，比如函数，
例如，这里我们创建了一个JavaScript对象：
var info = { full_name: "Neo Yang" };
看起来和JSON挺像，但是有区别，比如full_name没有引号，在JSON中我们可以使用full name 也就是中间有空格，但是JavaScript不行

var info = {
    full_name : "Neo",
    getName: function(){
        alert(this.full_name);
    }
};

它的键没有必要使用引号
它的值类型可以是任何数据类型，甚至是函数。
和JavaScript对象不同的是，JSON对象必须作为字符串放到引号中，且必须被转换为JavaScript
有好几种方法可以完成：
eval('(' + data + ')' );
或者
JSON.parse()

这两种方法各有优劣：
第一种方法有安全缺陷，比如将一段脚本放到JSON字符串中
第二种方法，对于一些老的浏览器不兼容

还有一个方法称为：JSON.stringify，用来将JSON对象转换为字符串，和JSON.parse一样，也有兼容性的问题，这种情况下jQuery库就起很大作用了。


### Create simple data
键值对，以逗号分隔

#### 获取数据
通过转换为对象后，
* 通过.访问: info.full_name
* 可以使用["key"]来获取：console.log(info["full_name"]);
这就是建议使用_ 来连接空格
也可以包含数组 []， 通过索引来获取。
也可以包含对象 {} 不过它不能保证读取的顺序，如果一定需要按照某种顺序的，用数组吧！


### Using JavaScript and JSON tools
创建JSON不复杂，但也很容易出错，借助一些工具来辅助检查：
JSLint
JSONLint
JSONOnlineEditor
也许需要离线的：
JSONCocoaEditor
JSONPad
浏览器插件：
火狐
Chrome JSONView


## Working with JavaScript Objects
### Debugging JavaScript objects with your browser
有时候需要方便的在浏览器中调试JSON或JavaScript Object，这个时候我们就需要Developer Editor
在Chrome中打开如下的HTML文件：

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>JavaScript And JSON</title>
</head>
<body>
	<script>
		var info = {
		"full_name" : "Ray Villalobos",
		"title" : "Staff Author",
		"links" : [
				{ "blog"     : "http://iviewsource.com" },
				{ "facebook" : "http://facebook.com/iviewsource" },
				{ "youtube"  : "http://www.youtube.com/planetoftheweb" },
				{ "podcast"  : "http://feeds.feedburner.com/authoredcontent" },
				{ "twitter"  : "http://twitter.com/planetoftheweb" }
			]
		};
	</script>
</body>
</html>
```

打开Developer Editor，打开Console选项卡：
1. 获取
直接输入 info 就可以获取info对象，或者使用dir(info)来换个方式显示。

2. 获取对象属性
可以使用 info.full_name 或 info["full_name"]

3. 获取对象列表内容
info.links[0].facebook

4. 修改对象值：
info.full_name = "Neo"

5. 删除对象值：
delete(info.full_name)

6. 新增对象值：
info.address = "US"

### Modifying Array objects in JavaScript
那么如何删除和新增对象中列表（或数组）中的值呢？
可以是试试delete(info.links[1]); 再次输出info对象后，我们发现数组长度依旧是5，但元素不见了，这不符合我们的要求，我们应该使用数组的splice函数
info.links.splice(1,1);
它有两个参数，第一个参数是开始索引，第二个参数是包括索引后的几个元素。
如果我们要想数组中新增元素，我们需要使用push方法：
info.links.push({"course": "whatever"});


### Looping through JavaScript objects

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
	<title>JavaScript And JSON</title>
</head>
<body>

<script>

var info = {
"full_name" : "Ray Villalobos",
"title" : "Staff Author",
"links" : {
    "blog"     : "http://iviewsource.com",
    "facebook" : "http://facebook.com/iviewsource",
	"youtube"  : "http://www.youtube.com/planetoftheweb",
	"podcast"  : "http://feeds.feedburner.com/authoredcontent",
	"twitter"  : "http://twitter.com/planetoftheweb" 
	}
};

</script>
</body>
</html>
```

我们修改一下HTML
```html
<h2> Links </h2>
<ul id="links">
</ul>
```

```JavaScript
var output = "";

for (key in info.links) {
    if(info.links.hasOwnProperty(key)){
        output += `<li><a href="${info.links[key]}">${key}</a></li>`
    }
}

var update = document.getElementById('links');
update.innerHTML = output;

```
这里读取的是无序的。


### Accessing objects in arrays

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>JavaScript And JSON</title>
</head>
<body>
	<script>
		var info = {
		"full_name" : "Ray Villalobos",
		"title" : "Staff Author",
		"links" : [
				{ "blog"     : "http://iviewsource.com" },
				{ "facebook" : "http://facebook.com/iviewsource" },
				{ "youtube"  : "http://www.youtube.com/planetoftheweb" },
				{ "podcast"  : "http://feeds.feedburner.com/authoredcontent" },
				{ "twitter"  : "http://twitter.com/planetoftheweb" }
			]
		};
	</script>
</body>
</html>
```

```JavaScript
var output = '';
for (var i = 0; i < info.links.length; i ++){
    for(key in info.links[i]){
        if(info.links[i].hasOwnProperty(key)){
        output += `<li><a href="${info.links[i][key]}">${key}</a></li>`
        }
    }
}
```



## JavaScript, JSON and AJAX
### Parsing JSON data with AJAX
JSON和AJAX配合起来使用非常强大， AJAX是Asynchronous JavaScript and XML，这里需要了解关于Ajax的知识，可以查看：
基本的思路就是通过AJAX向服务器请求JSON数据，然后在本地转换并获取想要的信息。


### Communicating across sites with JSONP
JSONP，P是Padding的缩写
如果直接通过AJAX代码获取位于其他服务器的JSON数据，可能会遇到无法获取的情况，因为访问的内容超过了当前域，这个时候，我们就可以使用JSONP
位于其他服务器的JSON文件data.JSON
dataHander({

});
然后在我们的服务器中使用AJAX获取。
### Using jQuery to parse JSON feeds
使用jQuery来实现异步获取JSON并转换会更加方便：
```JavaScript
$(document).ready(function(){
    $.getJSON('data.json', function(){
        // do whatever you want.
    })
})
```

## JavaScript and JSON in Action
### Setting up our HTML file
### JavaScript templating with mustache
### Rotating with jQuery Cycle
### Styling our application

到这里其实已经没有什么深究的了，看课程的源代码就可以了。

## Next?
JavaScript and AJAX
jQuery Mobile Web Aplications
Building Facebook Applications
Blog: iviewsource.com

Recommand Books:
JavaScript: The Good Parts
Secrets of the JavaScript Ninja
Effective JavaScript(David Herman)