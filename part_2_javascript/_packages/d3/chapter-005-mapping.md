---
title: D3.js 04 Mapping
date: 2016-08-22 14:29:14
tags: [d3.js, data visualization]
categories: data visualization
---

创建地图
任务：

- 创建基本地图
- 调整分界
- 创建地区分布
- 给可视化添加点击事件
- 使用update和transition来提高可视化
- 添加兴趣点
- adding visualizations as a point of interest

创建基本地图

首先，创建容器，宽高取决于你在哪儿看，手机？平板还是PC
var height = 600;
var width = 900;

接下来需要声明可以将地理坐标系（cartographic space）（经纬度）转换为笛卡尔坐标系（ 也就是将经度和纬度映射到坐标系）的projection 对象。
可以假想projection就是将三维球形展平，这有很多种方式(链接：https://github.com/mbostock/d3/wiki/Geo-Projections)，常用的是geoMercator(墨卡托投影)
var projection = d3.geoMercator();
var mexico = void 0;

接下来需要将Projection赋给geoPath函数，该函数的作用是将JSON格式的地理数据映射为SVG路径，geo.path函数需要的数据格式称为GeoJSON

var path = d3.geo.path().projection(projection);
var sag = d3.select(“#map”)
     .append(“svg”)
     .attr(“width”, width)
     .attr(“height”, height);

现在我们需要地理数据了。
d3.json(‘geo-data.json’, function(data){
     console.log(‘mexico’, data);
});

数据导入完成后，我们只想绘制我们感兴趣的数据，此外，我们还希望能自动将地图缩放到我们定义的宽高。

我们需要寻找有geometries的父对象，我们可以绘制：
var states = topojson.feature(data, data.objects,MEX_adm1);

注意，在我们使用console.log查看了数据源之后，我们发现MEX_adm1含有geometries数据，现在我们家将所有行政区域的数据传递给topojson.feature函数来挑出并创建GeoJSON对象。现在states变量包含了features属性，features数组是一个32GeoJSON元素的列表，每个都表示了墨西哥每个州的地理界限。

我们设置初始的缩放为1，偏移量是0,0

projection.scale(1).translate([0,0]);

path.bounds函数非常有用，它可以根据提供的一组地理数据据返回一个最小和最大坐标的数组：

var b = path.bounds(states);

详细描述：
bonding box表示二维数组[[left, bottom], [right, top]],

- left：最小经度
- bottom：最小纬度
- right：最大经度
- top：最大纬度

"The bounding box is represented by a two-dimensional array: [[left, bottom], [right, top]], where left is the minimum longitude, bottom is the minimum latitude, right is maximum longitude, and top is the maximum latitude."

如果我们想将这个版图都包含在我们的SVG容器内，这两个值就非常重要

地图实际坐标的实际宽度值 /  SVG 图形宽度值

var s = .95 / Math.max((b[1][0] - b[0][0]) / width, (b[1][1] - b[0][1]) / height);

按照需要缩放最大的来，0.95 对Scale值进行了调节，因为我们需要给地图和SVG容器边框留点空间。

var t = [(width - s * (b[1][0] + b[0][0])) / 2, (height - s * (b[1][1] + b[0][1])) / 2];

为了让地图位于屏幕中间。

最后对projection进行设置：
projection.scale(s).translate(t);

现在需要创建一个map变量用于将所有元素统一添加到组<g>标签中，同时也便于我们设置属性：
var map = sag.append(‘g’).attr(‘class’, ‘boundary’);

最后进入D3的经典模式：enter，update，exit。

mexico = map.selectAll(‘path’).data(states.features);

// Enter
mexico.enter()
     .append(‘path’)
     .attr(‘d’, path);

不知道是数据的原因还是什么，绘制中国地图错误。

调整边界，主要就是path.bounds函数，我们需要返回特定区域的值就可以了，例如：
var b = past.bounds(states.features[5]);

创建区域划分

需要地图数据 geojson
如何获取：QGIS 用于将图形转换为geojson，或者直接从网上下载

d3.json(“china.geojson”, function(data){
     var group = canvas.selectAll(“g”)
          .data(data.features)
          .enter()
          .append(“g”)

     // 需要补同的Projection？！

     var projection = d3.geo.mercator().scale(7300).translate([0, 1900]);
     var path = d3.geo.path().projection(projection);

     var areas = group.append(“path”)
          .attr(“d”, path)
          .attr(“class”, “area”)
          .attr(“fill”, “steel blue”);

     group.append(“text”)
          .attr(“x”, function(d) { return path.centroid(d)[0]; })
          .attr(“y”, function(d) { return path.centroid(d)[1]; })
          .attr(“text-anchor”, “middle”)
          .text(function(d) {return d.properties.LNNAMN; })
          .
})
