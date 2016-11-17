---
title: D3.js for data visualization
date: 2016-08-11 18:06:27
tags: [d3.js, data visualization]
categories: data visualization
---

<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <script src=“d3.min.js"></script>
        <script>
            function draw(data) {
                "use strict";
                // badass visualization code goes here }
        </script>
    </head>

    <body>
        <script>
            d3.json("data/some_data.json", draw);
        </script>
    </body>
</html>
其中的要点包括：

- 导入d3库
- 创建draw(data)函数，这是我们的主要工作，它有一个参数，该函数会在客户端下载数据完成后调用。
- 使用”use strict”，使用严格标准的JS，会让代码易读
- d3.json()函数会创建一个HTTP GET请求，例如要下载json文件，一旦下载完成后就会调用第二个参数，也就是draw函数，会传递唯一的参数，也就是将json数据转换为一个对象或者数组。注意：尽管D3也可以读取XML，CSV，但该教程主要集中于JSON。

关于Selection的运用

练习一：创建列表图形——简单的地铁列车状态板
数据：service_status.json
解决：
function draw(data){
            'use strict';
            d3.select("body")
            .append("ul")
            .selectAll("li")
            .data(data)
            .enter()
            .append("li")
                .text(function (d) {
                return d.name + ": " + d.status;
                });
        }

D3实现的方式有点奇怪：

- 这种编程方式称为“方法链”或“层叠”
- 我们通过selectAll来选择页面的所有列表元素，尽管我们知道根本就没有，这为新列表元素进入可视化准备了方法。事实上，其创建了一个空选择(empty selection)，是未赋值的数组，but that has been blessed with a data method, allowing it to accept data.
- data方法将数据集中的每个元素与空选择进行关联，这就生成一个和我们的数据集一一对应一个数组的选择
- 所有已经含有数据但没有页面对应标签的元素，称为enter selection.

尽管当我们使用selectAll的时候还没有创建任何列表元素，我们姑且称其为空选择（但是它定义了之后到底使用什么HTML元素来对应数据元素），但之后的data方法会将其参数数据集中的每一个数据元素和刚刚的selectAll中的元素一一对一，那必然就会有以下三种情况：

- selectAll为空，但数据集合不为空
- selectAll返回的HTML元素总量与数据集总量想等
- selectAll返回的HTML元素总量比数据集总量多。

对于这三种情况分别有对应的方法：
就是enter, update, exit
.data()方法用来初始化选择，就好像设置了一个舞台，而.enter()方法只会选择那些有数据却还没有创建HTML元素的元素

所以这里的模式就很清晰：

- 找到要填充的元素是什么：比如我们这里的selectAll(‘li’)
- 为其找到相关的数据，就是.data(data)
- 将一个个数据元素和一个个HTML元素配比操作。

可以设置下样式：
function draw(data){
            'use strict';
            d3.select("body")
            .append("ul")
            .selectAll("li")
            .data(data)
            .enter()
            .append("li")
                .text(function (d) {
                return d.name + ": " + d.status;
                })
                .style('color', function(d){
                    if(d.status == "GOOD SERVICE"){
                        return "green";
                    }else{
                        return "red";
                    }
                });

        }

或者：

d3.selectAll("li") .style("font-weight", function (d) {
if (d.status == "GOOD SERVICE"){ return "normal";
} else {
return "bold";
} })

练习二：创建条形图——收费口日平均流量
数据：plaza_traffic.json
解决：
function draw(data){
            'use strict';
            d3.select("body")
            .append("div")
            .attr("class","chart")
            .selectAll(".bar")
            .data(data.cash)
            .enter()
                .append("div")
                .attr("class","bar")
                .style("width", function(d){
                    return d.count/100 + "px"
                })
                .style("outline", "1px solid black")
                .text(function(d){
                    return Math.round(d.count)
                });
        }

这样不太美观，我们需要修改外观，这里我们设置的class属性就有作用了：

Selection是D3的一个核心概念，基于CSS选择器，其可以让我们根据数据集对网页元素，选择修改，追加或删除。

选择网页的Page元素，添加容器元素，为数据集中的每一个元素添加元素。这是构建即使复杂的可视化的通用模式。
function draw(data) {
                "use strict";
                // badass visualization code goes here
                d3.select("body")
                    .append("ul")
                    .selectAll("li")
                    .data(data)
                    .enter()
                        .append("li")
                        .text(function (d) {
                            return d.name + ": " + d.status;
                        });
            }

添加样式
<style type="text/css">
        div.chart
        {
            font-family:sans-serif;
            font-size:0.7em;
        }

        div.bar
        {
            background-color:DarkRed;
            color:white;
            height:3em;
            line-height:3em;
            padding-right:1em;
            margin-bottom:2px;
            text-align:right;
        }

需要注意的是，这里的数据看起来是比较“黏人”的，单独的函数中的数据总是指向绑定到enter函数的数据。

收费站流量日平均图

- 获取数据：这个不需要我们解决
- 如何绘制：

使用DIV标签创建水平条形图
我们会使用和之前的模式。

Scales, Axes and Lines
我们需要处理的一个问题是怎样将我们的数据值转换为适当的像素或者color

对于统计可视化则是个很复杂的问题，我们需要确定使用Numerical Scales, Ordinal Scales, Log Scales, Time Scales或者其他。

练习三：公交瘫痪，事故，受伤事故散点图
数据：bus_perf.json

首先需要设置viewport的维度，
var margin = 50,
 width = 700,
 height = 300,
这样设置SVG的Viewport在我们设置scales的时候会比较麻烦。

当我们绘制散点图的时候，我们需要知道其距离左上角的偏移量，这就需要缩放数据使得我们用像素作为单位来进行可视化时保证有意义。在D3中也就意味着我们需要创建一个函数使得能将数据域（输入）映射到像素范围（输出），这也就是scale对象的任务。

var x_extent = d3.extent(data, function(d){return d.collision_with_injury});

D3中的extent方法可以方便的返回数据域中的最小值和最大值。然后我们就可以创建scale了：
var x_scale = d3.scaleLinear()
.range([margin, width-margin])
.domain(x_extent);

同样：
var y_extent = d3.extent(data, function(d){return d.dist_between_fail});
var y_scale = d3.scaleLinear()
.range([height-marigin, margin])
.domain(y_extent);

我们还需要坐标轴
var x_axis = d3.axisBottom(x_scale);
这和之前版本d3.svg.axis().scale(x_scale)不一样的！
绘制：
            d3.select("svg")
            .append("g")
            .attr("class", "x axis")
            .attr("transform", "translate(0," + (height-margin) + ")")
            .call(x_axis);

我们还需要添加坐标轴名称：
不知道为什么……坐标轴不显示……

练习四：旋轴闸门流量
其实这里指的是地铁出入流量
数据：turnstile_traffic.json
基本样式：
{"times_square": [
     {"count": 36.333333333333336, "time": 1328356800000},
     ...
     ]}

第一个问题：
我们这里有两个地点，怎么为两个地点的count数据创建scale？
var count_extent = d3.extent(data.times_square.concat(data.grand_central), function(d){return d.count});
                var count_scale = d3.scaleLinear()
                                          .domain(count_extent)
                                          .range([height, margin]);
这是js的数组的属性，可以用来将两个数组拼接为一个。

如何映射时间戳
我们这里的time值是毫秒，直接用的话可读性不好，还好D3.js单独提供了时间轴，它是一个专业用于处理时间的线性Scale。
var time_extent = d3.extent(data.times_square.concat(data.grand_central), function(d){return d.time} );
                var time_scale = d3.scaleTime()
                                        .domain(time_extent)
                                        .range([margin, width]);

这样基本的绘制点的问题就解决了，现在添加坐标轴！
var time_axis = d3.axisBottom(time_scale);
这和之前版本d3.svg.axis().scale(x_scale)不一样的！
绘制：
// Set x axis
                var time_axis = d3.axisBottom(time_scale);
                d3.select("svg")
                .append("g")
                .attr("class", "x axis")
                .attr("transform", "translate(0," + height + ")")
                .call(time_axis);

让我们把这些点串起来——创建路径。

路径是有一条或多条连续的线组成，使用SVG来绘制非常难用，但D3为我们提供了路径生成器。
首先我们通过如下的代码创建一个line函数，其装载了数据集并可以作为SVG路径元素输出，注意，在x()和y()方法使用了我们之前创建的scale。
var line = d3.line()
                .x(function(d){return time_scale(d.time)})
                .y(function(d){return count_scale(d.count)});

然后我们通过调用它将其赋给d属性特定路径。
d3.select("svg")
    .append("path")
    .attr("d", line(data.times_square))
    .attr("class", "times_square");

d3.select("svg")
    .append("path")
    .attr("d", line(data.grand_central))
    .attr("class", "grand_central");

交互与过渡
到目前为止，我们已经可以创建了：列表、条形图、散点图、线状图。
现在我们可以做些交互以及一些动画来实现丰富的可视化效果。

数据：subway_wait_mean.json 与 subway_wait.json

我们将创建一个时间序列图，用户可以选择他们想看的时间序列

Layout
之前我们一直在关注D3通过数据集连接网页元素，现在我们需要了解点D3的布局工具。

地铁连接