---
title: JavaScript And Event
date: 2016-08-15 11:20:00
tags:
categories: fullstack
---
## 概述
* How the modern JavaScript Event Mode Works 
* Practical experience dealing with different types of events
show you how the modern Javascript Event Model works
and give you a lot of practical experience dealing with different types of events.

how events work and how to register them in order to make them available to your applications.

discuss the different ways that events can propagate and be
registered in the cache ring, as well as in the bubbling phase.
Plus,

how to stop an event from propagating and how to cancel an event or an element's default behavior.

explore how to deal with events through a series of exercises that show you how to deal with clicks, Mouse-overs, right-clicks, following the mouse, plus loading images.



## 关于事件
### 理解事件注册
JavaScript默认是按序执行脚本的，但我们让代码仅仅在某些事件发生的时候才调用，这是因为当网页DOM中的一些元素发生一些事儿浏览器可以触发某些事件。JS事件可以在任何时候发生，例如，当浏览器加载页面时，用户移动鼠标时，视频加载完成，表单提交时，这些都是事件，所以当你需要在某些事件发生时执行一些任务时，你需要捕获该事件，而这是通过事件注册来完成。这就等于告诉浏览器，当某件事发生时，要做什么事儿。

我们有不少方法可以实现，有些对旧的浏览器兼容比较好：
* 使用标签属性，例如`<a href="#" onclick="alert('hh')">` ，这虽然有效，但是总比较糟糕的做法，代码复用性差，且不易更新，将JS和HTML标签分开会比较好。
* 使用`.`，也就是，首先需要找到你需要的元素，然后指定你想跟踪的事件

```html
<a href="#" id="mylink">

<script>
    document.getElementById('mylink').onclick=function(){
        alert('hh');
    }
</script>

```

* 使用`addEventListener`，它可以用于页面中的任何元素，接受三个参数：
    1. 事件类型
    2. 调用方法
    3. true/false 也就是propagation类型

```html
<a href="#" id="mylink">

<script>
    document.getElementById('mylink').addEventListener('click',function(){
        alert('hh');
    }, false);
</script>

```
那么`addEventListener`有什么特别的地方呢？
它可以让我同时检测多个事件，也就是所知的事件propagation，
还有个不常见的优点是，可以被非DOM触发，这意味着，通过该方法，我们可以创建自己的事件

当然，它有个缺点是IE8及之前的浏览器并不支持

### 在老浏览器中使用事件
IE8不支持`addEventListener`方法，但是它有类似的`attachEvent`不过也有些不同：
* 事件类型是`onclick`
* 没有第三个参数
```html
<a href="#" id="mylink">

<script>
    document.getElementById('mylink').attachEvent('onclick',function(){
        alert('hh');
    });
</script>
```
尽管现在对要兼容浏览器要求不那么高，但是至少得知道，所以想写段代码同时支持IE8，可以这么写：
```html
<a href="#" id="mylink">

<script>
    if(windows.addEventListener){
            document.getElementById('mylink').addEventListener('click',function(){
            alert('hh');
        }, false);
    } else if(windows.attachEvent){
        document.getElementById('mylink').attachEvent('onclick',function(){
        alert('hh');
    });
    }
</script>
```

当然也可以考虑使用jQuery，其他更老的浏览器，可以看看这篇文章：http://www.dustindiaz.com/rock-solid-addevent

### 分析事件属性
当注册并捕获了一个事件后，我们会从浏览器那儿获取一个对象，对于不同的浏览器返回的对象可能略有不同，这就意味着我们有可能不能使用所有的功能，此外，对象还取决于事件的类型。

但是很多事件几乎都有些类似的信息
我们可以从事件对象和浏览器环境中获取很多信息，下面我们就看看从事件对象中我们可以获取哪些信息？

```html
<a href="#" id="mylink">

<script>
    document.getElementById('mylink').attachEvent('onclick',function(e){
        // 获取事件
        console.log(e);
    });
</script>
```
#### Event Info
* type              事件类型，比如这里是`click`事件 
* timestamp         事件发生的时间
* defaultPrevented  事件发生时是否需要阻止浏览器默认的行为，例如点击一个链接，但你只想对页面做一点修改而不是页面跳转，这个时候就该使用`true`，就会阻止跳转行为的发生。

#### Targeting Info
* currentTarget     事件绑定的元素
* target            is the element that the event is originated from 这和事件绑定的元素有点区别
* srcElement        触发事件的元素
* fromElement
* toElement         这和fromElement联系在一起使用，往往用于处理鼠标事件，比如从一个地方移动到另外一个地方。

对于Targeting Info，IE和其他浏览器的是有差别的，会在之后讨论，可以看看如下的网页：
http://www.javascriptkit.com/jsref/event.shtml

#### Coordinate Info
* screen X,Y 
* layer X, Y 
* client X, Y 
* offset X, Y 
* page X, Y 

使用这些属性时，需要注意，它们并不是很精确，而且不是所有浏览器都具有这些属性，要检测兼容性，还是需要考虑看看 quricksmode.org
 
#### Key/Mouse Info 
和键盘鼠标相关的事件：
* altKey
* button
* shiftKey
* ctrlKey
* charCode/keyCode
参考：http://www.unixpapa.com/js/key.html 


### 理解事件传播(Propagation)
理解事件传播非常总要！
Event Propagation lets you have a single element caputre all the events of its children element

而它也是为什么我要使用`addEventListener`的原因，尽管它并不和IE8之前的浏览器所兼容。

示例：之前，我们通过给一个元素设置ID，然后为该元素注册事件，现在假设我们想给一个列表中的所有元素都添加事件，除了一个一个写外，我们还能怎么做呢？

```html
<ul id="grid">
    <li><img src="imgs/a.gif" alt="yellow"></li>
    <li><img src="imgs/b.gif" alt="orange"></li>
    <li><img src="imgs/c.gif" alt="purple"></li>
    <li><img src="imgs/d.gif" alt="green"></li>
    <li><img src="imgs/e.gif" alt="ygreen"></li>
    <li><img src="imgs/f.gif" alt="gray"></li>    
</ul>

<script>
    document.getElementById('grid').addEventListener('click', function(e){
        // 在console里查看 toElement,会发现值为 img 
        console.log(e);

        // 直接获取，我们到底点击了那个元素
        console.log(e.toElement.alt);
    },false);
</script>
```
这样，我们就可以获取列表里的所有子元素的事件了。

但这里有些不好的地方，就是不同的浏览器支持不同的传播模式(Propagation Model):
* 捕获模式(Capture) 一直会沿着DOM向下捕获，例如从`ul`到`li`到`img` 来注册事件
* 冒泡模式(Bubble) 例如会从`img`到`li`再到`ul`

之前我们的`addEventListener`有三个参数，第三个参数就是决定我们用哪个传播模式，
false将使用bubble模式，true使用capture模式，IE浏览器只支持bubble模式，有些浏览器只支持capture模式，而Chrome都支持，想获得更多细节，查看：
http://www.quricksmode.org/js/events_order.html



### 停止事件传播(Propagation)
事件传播可以让我们通过为父对象添加事件监听，从而为所有的子元素注册事件，但有时候，你可能想阻止这样的行为，我们可以使用`stopPropagation`方法来实现。
如果想在IE中使用，需要将`cancelbubble = true` 来实现
```html
<ul id="grid">
    <li><img src="imgs/a.gif" alt="yellow"></li>
    <li><img src="imgs/b.gif" alt="orange"></li>
    <li><img src="imgs/c.gif" alt="purple"></li>
    <li><img src="imgs/d.gif" alt="green" id="green"></li>
    <li><img src="imgs/e.gif" alt="ygreen"></li>
    <li><img src="imgs/f.gif" alt="gray"></li>    
</ul>

<script>
    document.getElementById('grid').addEventListener('click', function(e){
        console.log('Clicked inside the UL');
    },true);

     document.getElementById('green').addEventListener('click', function(e){
        // 直接获取，我们到底点击了那个元素
        console.log(e.toElement.alt);
    },true);
</script>
```
如上的代码，id为`green`的图片会有两个事件监听，如果我们点击它，运行结果：

```bash
Clicked inside the UL
green
```

要阻止传播，我们先将传播模式改为bubble，这样的话，和更多浏览器兼容，然后将id为`green`的元素，停止传播：

```js
document.getElementById('green').addEventListener('click', function(e){
    console.log(e.toElement.alt);
    e.stopPropagation();
}, false);
```

这下，我们再运行，`green`元素，就只有一个事件监听了。

### 取消默认行为
有很多事件在事件发生时，都有些默认行为，例如，当我们点击一个链接，默认的行为就是浏览器会根据这个链接跳转到新的页面，或者当用户尝试提交一个表单时，默认行为是携带数据并传递给表单处理器，你也许会阻止，这样就可以对表单进行验证了，为了控制默认行为的发生，我们可以使用`preventDefault()`方法。

```html
<ul id="grid">
<li><a href="a.html"><img src="a.jpg" alt="the img"></a></li>
</ul>
<script>

document.getElementById('grid').attachEventListener('click', function(e){
    e.preventDefault();
    console.log('click inside the UL'); 

},false);

</script>
```

## 常见事件

### 通过事件移除DOM元素

### 清理事件问题
### 通过事件创建DOM元素
### 移除一个事件
### 阻止默认事件

## 时间事件
### 为大图片加载创建等待旋转图片
### 多媒体事件
### 监控多媒体播放结束事件
### 多媒体暂停
### 开始新的歌曲

## 实践