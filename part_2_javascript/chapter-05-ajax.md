---
title: JavaScript And AJAX
date: 2016-08-15 09:20:00
tags:
categories: fullstack
---


The World's Most Misunderstood Programming language.

注意Start的第二节课代码与第三节课

developer.mozilla.org/en-US/docs/DOM/XMLHttpRequest

尽管旧的IE浏览器的份额越来越小，但知道实现AJAX请求的兼容还是很重要的，事实上XHR请求的概念一开始是由微软创建的，并在IE5中实现了，完成异步请求的需求，微软使用了ActiveXObject的方式，但ActiveX在其他浏览器，例如Safari，Chrome，Firefox中并没有， 它们通过另外一种方式实现了该API，也就是XMLHttpRequest， ActiveX看起来是个不错的实现，慢慢的XMLHttpRequest开始成了标准。

所以和其他不少Web技术一样，我们需要处理不同的浏览器（尤其是老的）的兼容问题，需要检查这些浏览器是否有XMLHttpRequest对象，如果没有，我们就使用ActiveXObject，代码如下

``` javascript
var request;
if(window.XMLHttpRequest){
    request = new XMLHttpRequest();
} else{
    request = new ActiveXObject('Microsoft.XMLHTTP');
}
```

## 配合getElementById来修改DOM
当我们使用AJAX，很大程度上是因为我们希望在页面加载完成后，对页面进行修改，这个时候，怎么获取页面元素，和怎么修改就很重要了：
var yourObj = getElementById('id');
yourObj.innerHTML = '从服务器获取的数据后……';


## 使用AJAX转换XML 

request.responseXML
对于XML我们也可以使用getElementsByTagName()，例如：
request.responseXML.getElementsByTagName('tag-name')[1].childNodes[0].nodeValue;
当然也可以使用firstNode。 不然，我们就获取了整个Node，比如`<name>Neo</name>`，而使用firstNode就会返回其中的Text，这还会有双引号，我们可以使用nodeValue来去除。查看代码！

当然其实不管是不是XML，也可以是JSON或其他文件，关键就是如何转换为JavaScript Object，并可以操作（增删改查）。

## 使用AJAX转换JSON
json.Parse(request.responseText)

## 使用事件驱动AJAX
我们可以通过一些事件触发来决定我们是否要通过AJAX获取数据：用户点击，页面加载等等，其实没有什么区别，只是将我们要执行的AJAX操作绑定到事件上罢了


## 使用jQuery执行AJAX操作
$('.update').load('data.txt')
$.getJSON('data.json', function(data){
    // data 是经过转换的

    $.each(data, function(key, value){

    })
})


## 开始
### 什么是AJAX？

asynchronouse JavaScript and XML 

### 什么是XHR？
* 不是XML
* AJAX请求可以是任何格式
    - 文本文件
    - HTML
    - JSON 对象
    


### 如何使用AJAX来创建动态网站？

## 修改DOM

## jQuery AJAX

