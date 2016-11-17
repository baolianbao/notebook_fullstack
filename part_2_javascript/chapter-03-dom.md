---
title: JavaScript and DOM
date: 2016-08-15 08:20:00
tags:
categories: fullstack
---

## 关于开发工具
查看另外一篇文档。

## 在console中试试JavaScript



## 节点
有12种节点类型，但我们往往只关心三种：元素节点、属性节点、文本节点，需要注意的是，元素节点并不包含文本节点，例如<p>text here!</p> 元素节点是p,文本节点是text here!

## 如何获取元素节点
根据ID获取元素节点，这个节点是个对象，那就意味着我们可以获取它的属性和方法。
更加Tag获取元素节点，会返回节点数组
## Next
http://www.caniuse.com
http://www.html5please.com
http://www.quirksmode.org/compatibility.html


概述：
the  document object model is tightly integrated into JavaScript. 
If you're looking to master how you can  control elements in your document through JavaScript.


目标：
* how the developer tools work by chrome and how to grasp  commands by the JavaScript counsel.
* select notes by ID,  class name and with the new query selector.
* modify regular,  restricted and HTML5 data attributes in dom element. 
* create, append, clone, replace and remove existing nodes.  
* build a project that
utilizes what you've learned by building  a moto popup.
We'll create an overlay with a centered  image, style it via JavaScript, and
handle events like clicks, scrolling and  resizing the document window.


## 开始
开始之前需要先讨论以下几个问题：
* 什么是DOM？
* 为什么DOM很重要
* 讨论和DOM相关的术语

### 什么是DOM？
Document Object Model的缩写，用于描述HTML文档结构和不同元素，例如页面中的标签、属性和内容之间的关系。
As you add, delete or modify existing  elements on your website, you're creating
structure that a browser interprets as  the DOM.
当你新增，删除或修改网页中的元素时候，你正创建结构

```html
<ol>
    <li>1</li>
    <li>2</li>
    <!-- 新增节点 -->
    <li>3</li>
</ol>
```

例如，你在页面中添加新的元素`<li>`，这样我们在页面的DOM中就添加了一个新的节点，该节点拥有不少关系，例如兄弟，父节点`<ol>`

DOM 同时也是API，它给一些语言，例如JavaScript和CSS一种途径来定义或修改已经存在的文档。例如CSS可以选中某个元素然后修改其颜色，

可以将DOM看成一个倒树状结构
### 为什么DOM很重要
### 讨论和DOM相关的术语

  The DOM is also the API that gives
languages like JavaScript and CSS a way  to define and modify the existing document.
So, I have an article tag here with an id  of main as well a headline right underneath.
If I go to the CSS with this document I  can access that element each 1 node and
ask the browser to change it's color.  The browser knows how to access this
element, because it looks at the HTML I  wrote, and creates a DOM tree.
Once that structure exists, it can can  map the CSS I wrote and target a specific
element in the page. 

 It's really best to think of the DOM as an upside down family tree.  I'm working with a really simple webpage
with a traditional HTML structure plus a  header, an article tag, and a footer.
At the top of the family tree is the  document itself.
And then what we called a root element,  which is normally the HTML tag.
Inside that element, we have children of  the html element, which is normally the
head and the body tags.  Inside those, we may have some additional elements.
For example, in the head section, we may  have a title element, a script tag, and
maybe a call to an external style sheet.  Inside the body tag we may have a header,
and that header can have a nav, and that  nav can have a list of links.
Each one of those links may have an  anchor tag inside them.
We could also have an article tag, with a  series of headlines and paragraphs.
Every element in the DOM, including the  text and attributes are considered nodes.
Nodes can be both parent, and have  children elements.
But they can also have other  relationships.
Elements in the same level is known as  siblings.
So these h1 and paragraph tags are  considered siblings.
So are these li tags.  Siblings are elements with the same parents.
The first and last children of an element  have special names called first child and
last child.  The rest of the children of the element
are known as child nodes.  Remember that browsers use your HTML code
to create this DOM structure.  And this is why it's really important to
write clean and valid HTML. 
So that your CSS and JavaScript code can access and modify existing elements  without any problem.


### 开发者工具一览DOM
主要是Elements和Console窗口，Command + Alt + J 
在非Console窗口，可以通过ESC键来启动命令行。

### 通过开发者工具测试JavaScript

```js
// 垂直显示
dir(document.body.childNodes)
// 获取元素
document.getElementById('main')
document.querySelector('#main')

// Console提供了获取元素的快捷方式
// 正如jQuery一样
$('#main')
$('footer')

// 会获取首个符合该条件的元素
$('header nav ol>li')
// 会获取所有符合该条件的元素列表
$$('header nav ol>li')

// console会将上一次存储获取的值存储在 $_变量中
$_

// 可以通过inspect来聚焦某个元素，它不仅会返回该元素，还会在Element窗口选中它
inspect( $('header nav ol>li') )

// 可以通过monitorEvents来监控事件
// 运行代码你并看不到任何结果，但是如果点击id为main的元素，在console 中就会输出关于点击的事件信息。
monitorEvents(document.getElementById('main'), 'click')

```
可以通过Ctrl + L 来清空console窗口。

## JavaScript与Console通信

```js
console.log();
console.dir();
console.info();
console.warn();
console.error();
```

### 关于group
```js
console.group("Page Links");
console.dir(document.querySelectorAll('a'));
console.groupEnd();

console.groupCollapsed("Paragraphs");
console.dir(document.querySelectorAll('p'));
console.groupEnd();
```

### 关于时间

```js
console.time("BigLoop");
for(var i=100000; i >=0 i --){

}
console.timeEnd("BigLoop");
// BigLoop: 0.82ms
```

### 关于断言 

```js 
console.assert(
    document.querySelectorAll('nav ol>li').length === 2,
    "Sorry, there's only two menu items"
);
```

-------------

## DOM选择
主要解决选择元素的一系列方法：

### getElementById 
可以使用`document.getElementById('<id>')`，它最常用，在Console中测试的时候，仅仅使用该代码时，只能获取到对应节点的HTML代码，如果我们使用`dir()`函数，就可以获取该节点的属性和方法：

```js
dir(document.getElementById('main'))
```
例如`firstChild`，`childNodes`

### 根据HTML标签选择元素
方法：`getElementsByTagName()`，即根据标签返回一组元素
返回：数组
可以配合`getElementById`使用：

```js
document.getElementById('mian').getElementsByTagName('li')
```
由于返回的数组，可以使用索引来访问

### 根据类选择元素
方法: `getElementsByClassName()`，即根据类返回一组元素，但它是新特性，可能一些老的浏览器不支持。例如早起的IE浏览器，这个时候jQuery这些插件就是好东西了。
当我们不确定某个方法浏览器是否支持的时候，可以通过：
* http://www.caniuse.com/
* http://www.quirksmode.org/dom/w3c_core.html 
来查询 。
当然也可以配合getElementById来选择。

### 用CSS选择器的方法来选择元素
新特性`querySelector`和`querySelectorAll`可以支持像用CSS类似的方法来选择元素，和jQuery非常相似。同样可以通过上面的链接来检查，但总体上来说，比`getElementsByClassName`好点

```js
// 选择第一个符合条件的
document.querySelector('article')
document.querySelector('article').childNodes


// 选择所有符合条件的
document.querySelectorAll('article')
document.querySelectorAll('article')[1].childNodes

document.querySelectorAll('input[type=radio]')
document.querySelector('#article li>img')

```
如果不关注IE8之前的浏览器，大可放心使用这两个方法，但如果需要担心，那可以使用Polyfills，它是指在老浏览器支持新的方法：
http://goo.gl/LPTDP
或者，直接考虑jQuery吧！

### 选择命名的表单元素
* 表单元素form可以有name属性 `document.getElementByName('name')`
* DOM提供了doucment.forms对象，返回页面所有的表单列表 `document.forms`
* 也可以直接根据表单名称获取表单对象 `document.myformname`

```js
document.forms 
document.forms[0]

// 表单名称是register
document.register
 
// 获取名为register的表单的myname字段
document.register.myname

// 设置它的值
document.register.myname.value = 'Neo'

// 需要注意的是，有可能一个表单里有相同的名字，例如radio，这时就会返回数组

// 设置某个radio按钮选中
document.getElementByName('subscribe')[1].checked = "checked"

// 对于下拉列表，可以通过name属性获取元素
document.myform.dropdownList.value = 'Fishing'
// 查看列表选中的索引
document.myform.dropdownList.selectedIndex
```

### 认识 nodeType, nodeName, nodeValue
每个DOM元素都有些重要的属性可以用来区分它们：
* node.nodeType : 节点类型的数值
* node.nodeNmae : 节点的名称，通常是标签名称
* node.attributes: 节点属性数组
* node.nodeValue: 节点内的元素

#### Node类型
http://www.w3schools.com/dom/dom_nodetype.asp
我们往往关注的是：
* 元素节点 1
* 属性节点 2
* 文本节点 3

这里有点困惑的是，文本节点，它只是表示了节点而已，而并非真正的文本，如果要修改它，必须通过nodeValue

核心就是：DOM里的一切都是节点！

### 节点树漫游
上面讲述了如何获取元素，而每个元素都是节点，那么如何根据某个节点找到其他节点？
* parentNode 上一层
* childNodes 子节点数组
* firstChild/lastChild 子节点数组中的第一个/最后一个节点
* previousSibbling/nextSibbling 
记住可以通过dir(node)来查看可用的属性和方法。

特殊情况：由于在DOM中所有东西都是节点，哪怕是文本。这就可能导致我们的`childNodes`所返回的数组并非是我们想要的，比如可能会包含一些空格键（文本节点），所以有些时候并不实用。

### 定位节点元素
上一节讲到关于 childNodes 使用的一系列问题，这里会提出一些改进，不过主要是一些新的浏览器特性：
* firstElementChild 第一个元素节点（也就是像文本节点、属性节点就不存在！）
* lastElementChild 
* children 仅仅返回元素节点列表
* previousElementSibbling/nextElementSibbling

但是……浏览器支持并不充分
http://www.quirksmode.org/dom/w3c_traversal.html
IE 9之前都不支持
FF3.0都不支持……
所以，如果不在乎，就用！
---------------------------

---------------------------
## 修改DOM属性和内容
### 修改HTML属性
最简单的就是通过 `.`来访问属性例如 `img.src`就可以返回图片源属性，而这些是可以read 和 write的，我们甚至还可以添加一个不存在的属性！需要注意的是，不能使用JavaScript的保留字(class)或关键字，所以需要特殊处理，不能就直接使用`myNode.class=` 而是使用 `myNode.className`
还有表单里；

```html
<label for="myname">Name</label>
```
这里的`for`在JS里是关键字，肯定也不能直接使用`myNode.for`来获取，而是`myNode.htmlFor`

设置值的时候，例如boolean值，

```html
<input type="radio" id="subscribe" name="subscribe" checked value="yes">
```
上面的`checked`便是boolean值，可以使用`true` 或 `false`来赋值，或者 `1` 或 `0`

总结来说：
1. 要避免使用JS的保留字
2. 光使用`.` 并不能删除属性
所以不太方便。

### 使用restricted 属性
上面提到了使用`.`会遇到的一系列问题，所以JS提供了一些函数用来处理这些问题，例如可以使用getAttribute方法来获取某个属性的值
* `node.getAttriubte(attributeName)` 获取属性值
* `node.setAttriubte(attributeName, value)` 设置属性值
* `node.hasAttribute(attributeName)` bool值用于检测是否有属性
* `node.removeAttribute(attributeName)` 用于删除属性
这就是增删改查！就这了！

### 检测数据属性
用户可以创建自己想要的任何属性，例如保护一些信息，对于这些自定义的属性，浏览器一般会忽略，但整个HTML并不是合法的，HTML5给我们提供了一种路径，所有自定义的属性，可以在前面加上`data-`，那么这就是一个合法的属性，然后可以通过`data.dataset`属性来获取

```html
<img src="all.jpg" alt="Photo of all" data-task="speaker">
```

```js
myNode.dataset.task 
// 返回speaker
```

这个功能对使用jQuery Mobile框架的小伙伴肯定很实用，因为jQuery Mobile大量使用了data属性来设置，但对于浏览器支持程度也需要考虑，也许可以考虑使用getAttribute 

### 通过classList来控制 类 
Class属性可以有多个类值，`.`和`getAttribute`用起来并不方便，但是HTML5给DOM中所有节新增了一个新的属性`classlist`，可让我们执行类似jQuery所具有对类修改的功能，例如新增，删除，启用、禁用类，不过IE支持不好（IE10才支持）
* node.classList.add(class) 新增一个类
* node.classList.remove(class) 移除一个类
* node.classList.toggle(class) 启用、禁用类，首次用启用（返回true），再用就禁用(返回false)
* node.classList.length获取当前节点有多少个类
* node.classList.contains() 当前元素是否包含类

同样，如果不打算使用jQuery而又想用这个对象，且需要考虑浏览器兼容问题，可以考虑polyfy

### 定位属性的属性(Targeting the attributes property)
首先，这个是只读的！
可以通过节点的`attributes`对象来获取当前节点的特定属性
* 通过索引访问
* 通过属性名访问
* 通过`.` 访问

```html
<img src="images/a.jpg" alt="Photo of ">
```
```js
// 获取所有属性，会返回属性对象
myNode.attributes
// NamedNodeMap {0: src, 1....}
// 获取第二个属性
myNode.attributes[0]

// 
myNode.attributes["src"]

//
myNode.attributes.src
```

### 使用HTML修改元素
我们还可以通过一些属性直接修改和节点相关的HTML内容：
* `node.innerHTML` 获取节点内的HTML
* `node.outerHTML` HTML5新特性，包括了节点元素的HTML
* `node.insertAdjacentHTML(insertionPoint, htmlText)` HTML5

暂时innerHTML就挺好的！

### 使用纯文本修改元素
上面我们使用诸如`innerHTML` 来以HTML的形式修改元素节点，还有可以通过纯文本的方式来修改，由于浏览器兼容性的问题，不过实用性不大。例如，你仅仅想获取节点的文本内容
* node.innterText 仅仅修改节点的文本
* node.textContent 在火狐中使用

所以需要条件判断：

```js
if(node.innerText){
    myText = node.innerText;
}else {
    myText = node.textContent;
}
```

这里的问题是，火狐不支持innerText,仅仅有textContent, 而textContent除了IE不支持外都支持，所以…………

-------------------


## 插入和删除节点
目前为止，我们一直都聚焦于如何选择和修改DOM元素，接下来就会讨论如何创建和删除。

### 新增或追加节点
* document.createElement(element)可以用来创建新的元素，然后但是它仅存于内存中，而非当前DOM的一部分。
* node.appendChild(element) 在一个特定的节点实例中新增一个节点，这样才会添加到当前的DOM中
当然我们也可以直接使用innerHTML来操作

```html
<ul>
    <li></li>
<ul>
```

```js
// 创建了一个新的节点元素，这个时候是不会显示到DOM中的
var myElement = document.createElement('img')
img.src = 'hh.jpe';
img.alt = 'another img";
myElement.setAttribute('data-test', 'speaker');

// 把它添加到指定的节点处
linode.appendChild(myElement);
```

经管`appendChild`挺好用的，但我们并非总是想将一个元素追加到某个元素中去，我们需要能将节点添加到任何我们想要的位置 
`insertBefore()` 就是个不错的方法

### 复制和删除节点
复制节点对于移动已存在的元素的位置特别重要：
* `cloneNode` 可以创建一个已存在的节点的副本，并且可以决定是否包含复制它的子对象
然后我们就可以把副本移动到任何我们想要的位置了！
* `removeChild(node)` 可以从来移除节点，注意的是，这个方法的调用实例必须是要删除节点的父节点

### 替换节点
`replaceChild()` 让我们用一个节点替换另外一个节点，同样也需要从某个节点的父对象开始调用！

## DOM实践

## 其他
JSON
AJAX
Validating and Processing Forms with JavaScript and PHP 
Buiding Facebook Applications with HTML and JavaScript  
相关资源：
http://www.caniuse.com 
http://www.html5please.com
http://www.quirksmode.org/dom/w3c_html.html