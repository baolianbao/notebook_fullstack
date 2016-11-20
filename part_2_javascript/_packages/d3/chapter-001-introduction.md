# D3.js 介绍

## 简介
学习如何使用D3 JS库来创建漂亮的，即时的、可交互的，基于浏览器的数据可视化。

几乎所有的浏览器都可以渲染Scalable Vector Graphic(SVG) ，包括那些不能渲染Flash的移动设备。

用D3来做什么？

将数据集转换为适当的HTML元素，并能根据数据变化修改
能将数据值转换为对应的像素或者颜色

## D3
D3库允许我们操作Web页面的元素，例如创建、删除或者更久数据集的内容来编辑。
例如绘制散点图(scatter graph)，我们使用D3来 SVG circle元素，可以将数据集中的X值和Y值添加到其cx和cy属性中，并可以从默认单位到像素来缩放图形。？？

## 学习路径：
* 视频
* Getting Started With D3.js
* Learning D3.js Mapping

d3.geo
https://www.youtube.com/playlist?list=PLI_sHchSmdCDH0ooOKSWSA1uzr1vCqgHh

## 书籍参考

- Machine Learning for Hackers
- JavaScript: The Good Parts
- SVG Essentials

信息论？？？？？

总结下关于数据可视化的历史？

米娜德的流量图

D3的作者Mike Bostock
早期版本：Protovis

在中国有哪些即时数据？

## 其他
TopoJSON 优化 geographic数据
$npm install -g topojson

纽约大都会捷运局数据集
纽约是一个地域辽阔且人口密度较高的城市，随时人口移动，正因如此，它具有一个错综复杂的交通网络，由MTA管理。负责调度5个区1100万人的当地火车，地铁，公交，桥梁，隧道。

MTA向外开放了管理该网络产生的大量数据…… Page 3
我们将在该教程中使用该数据，教程中的每个案例或多或少的使用了又MTA提供的数据，可以通过：http://www.mta.info/developers/ 找到

整理数据
该教程相关的代码分为两个部分：
/code 目录包括了Python代码可以用来转MTA数据，可以转换多种格式，
/viz 目录包括HTML文件用于可视化
/viz/data包含了处理好的JSON数据，有些文件很大，所以在使用编辑器打开之前要注意。

Micha’s Golden Rule
Do not store data in the keys of a JSON blob.
不用JSON文件中不以数据作为键。
也就是，不要以如下的方式来格式化JSON：
{
     “bob”: 20,
     “alice” : 23,
     “drew”: 30
}
这个案例中我们将数据同时存储到键(name) 和值(age)中，当然，这是符合JSON的格式要求的，但破坏了Micha’s Goldeng Rule，我们应该使用如下的方式：
[
     {
          “name”: “bob”,
          “age”: 20
     },
     {
           “name”: “alice”,
           “age”: 23
     },
     {
          “name”: “drew”,
          “age”: 30
     }
]

上例中，我们仅仅将数据存储在值中，键只是表示了值的含义，如果你手里的数据不符合Micha’s Golden Role，考虑用d3.entries()试试转换。

提供数据
上面提到，d3.json()函数会向Web服务器发出HTTP GET请求，也就是说，我们需要运行一个Web服务器用来处理该请求并返回JSON数据，我们可以使用Python来提供一个简单的Web服务器。
