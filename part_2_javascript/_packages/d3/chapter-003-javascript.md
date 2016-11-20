# D3.js与JavaScript

核心

- 创建基本的SVG元素
- Enter
- Update
- Exit
- AJAX

创建基本的SVG元素

## 创建容器

```js
var svg = d3.select("body")
     .append("svg")
     .attr("width", 200)
     .attr("height", 200)
```

## 向容器中添加元素

```js 
var rect = svg.append("rect")
     .attr("x", 10)
     .attr("y", 10)
     .attr("width", 50)
     .attr("height", 100);
```

选中网页的body元素，追加一个容器元素，然后为数据集中的每一个元素追加一个可视化的元素，也是我们创建更加复杂的可视化的模式。

## Enter
Enter函数是D3可视化中非常基础的一部分

```js 
svg.selectAll('rect').data([1,2]).enter()
```
data函数将数据（[1,2]）绑定到我们的选区（所有的`rect`）,而`enter()`函数会循环数据中的每个值执行`enter()`之后的所有函数，例如：

```js
.append('rect')
.attr('x', function(d) { return d * 20; })
.attr('y', function(d) { return d * 50; })
```

在循环的数据时，创建`rect SVG`元素，并设置其x，y值

## Update

## Exit

## AJAX
简单介绍：允许用户在网页后台获取数据。
将数据和代码分离的优点：

- 代码少，可维护性高
- 更新数据，不动代码
- 可以使用第三方提供的数据源

```js
d3.json( data_source, function(error, json){
     if (error) return console.log(error);
     var data = json;
})
```

`d3.json`或者`d3.csv`函数必须有两个参数，第一个参数是请求的文件名称，第二个参数是一个函数，表示当文件请求完成之后读取文件内容作为第二个方法的参数。
需要注意的是，我们从数据文件里读出来的内容格式往往是`string`，所以需要类型转换，假设`data.csv`文件内容为：

```csv
x,y
100,100
130,120
80,180
180,80
180,40
```

现在我们需要每一行的x与y的和，固然可以在函数里完成，但csv函数提供了可选参数：https://github.com/d3/d3-request/blob/master/README.md#csv
也就是row, An optional row conversion function may be specified to map and filter row objects to a more-specific representation;
其目标就是将每一行内容转换为符合我们需要的格式，所以我们的代码可以这样写：

```js
d3.csv("data.csv", type, function (myArrayOfObjects){
        myArrayOfObjects.forEach(function (d){
          console.log(d.x + d.y);
        });
      });

function type(d){
  d.x = parseFloat(d.x);
  d.y = parseFloat(d.y);
  return d;
}
```




其他经常会使用到的JavaScript方法

将string转换为数值的快捷方式
myStringVal = "5"
myNumVal = +myStringVal
其效果等同于 myNumVal = parseFloat(myStringVal)

JS中对象的属性的获取方式
var myObj = { x: 5, y: 6}
val_x = myObj.x
val_y = myObj['y']

快速循环列表中的每一个元素，并将元素作为参数
var myArrayOfObjects = [
     { x: 100, y: 100 },
     { x: 130, y: 120 },
     { x: 80,   y: 180 },
     { x: 180, y: 80  },
     { x: 180, y: 40  }
]

myArrayOfObjects.forEach(function (d) {
     console.log(d.x + ", " + d.y)
});
之所以这个重要的原因是，myArrayOfObjects往往是d3发送HTTP GET请求所获取的数据。示例如下：
d3.csv("data.csv", function (myArrayOfObjects){
        myArrayOfObjects.forEach(function (d){
          console.log(d.x + ", " + d.y);
        });
      });

## Select 和 Append

```html
<html>
     <head></head>
     <body>
          <p>This is a paragraph ! </p>
          <script>
              d3.select("p").text("Hello World")
               // 结果显示的就是Hello World
          </script>
     </body>
</html>
```

我们也可以：

```html
<html>
     <head></head>
     <body>
          <script>
              d3.select("body").append("p").text("Hello World")
               // 结果显示的就是Hello World
          </script>
     </body>
</html>
```

// 准备一个svg容器

```js
var canvas = d3.select("body")
     .append("svg")
     .attr("width", 500)
     .attr("height", 500);

var circle = canvas.append("circle")
                    .attr("cx", 250)
                    .attr("cy", 250)
                    .attr("r", 50)
                    .attr("fill", "red");

var circle = canvas.append("rect")
                    .attr("width", 100)
                    .attr("height", 50);

var line = canvas.append("line")
                  .attr("x1", 0)
                  .attr("y1", 100)
                  .attr("x2", 400)
                  .attr("y2", 400)
                  .attr("stroke", "green")
                  .attr("stroke-width", 10)
```

再看看数据是怎么显示的！

```js
var dataArray = [20, 40, 50]

var canvas = d3.select("body")
     .append("svg")
     .attr("width", 500)
     .attr("height", 500);

var bars = canvas.selectAll("rect") // 选择所有的矩形，但是现在没有矩形啊！那就返回空的选择内容
                  .data(dataArray) // 目前为止，我们将我们的数据Binding到Empty Selection
                  .enter()
                    .append("rect")
                    .attr("width", function(d){  return d * 10; })   //
                    .attr("height", 50).
                    .attr("y", function(d, i) { return i * 100; });   // d, 表示数据， i 表示数据的索引
```

## 关于Scale
假设我们的数据多了一个，例如为[20, 40, 50, 60]
但是60的状态条和50的结果显示是一样的，这是因为当我们设置width的时候已经达到了容器的宽度，所以，为了保证有效，我们这里的宽度和高度是不应该设置固定值的，而是按比例缩放。

```js
var dataArray = [20, 40, 50, 60]
var width =500;
var height = 500;

var widthScale = d3.scale.linear()
                         .domain([0, 60])
                         .range([0, width])

var color = d3.scale.linear()
                    .domain([0, 60])
                    .range(["red", "blue"])

var canvas = d3.select("body")
     .append("svg")
     .attr("width", width)
     .attr("height", height);

var bars = canvas.selectAll("rect") // 选择所有的矩形，但是现在没有矩形啊！那就返回空的选择内容
                    .data(dataArray) // 目前为止，我们将我们的数据Binding到Empty Selection
                    .enter()
                         .append("rect")
                         .attr("width", function(d){  return widthScale(d); })   //
                         .attr("height", 50)
                         .attr("fill", function(d){return color(d)} )
                         .attr("y", function(d, i) { return i * 100; });   // d, 表示数据， i 表示数据的索引
```

上面的代码中，我们创建了一个线性缩放对象，然后在设置宽度属性的时候，我们通过将值传递给该缩放对象，从而得到一个合理的宽度值。

## 组与坐标

```js
var dataArray = [20, 40, 50, 60]
var width =500;
var height = 500;

var widthScale = d3.scale.linear()
                         .domain([0, 60])
                         .range([0, width])

var color = d3.scale.linear()
                    .domain([0, 60])
                    .range(["red", "blue"])

var axis = d3.svg.axis()
                    .ticks(5)   // 总共显示几个数据
                    .scale(widthScale);

var canvas = d3.select("body")
     .append("svg")
     .attr("width", width)
     .attr("height", height)
     .append("g")
     .attr("transform", "translate(20, 0)");

var bars = canvas.selectAll("rect") // 选择所有的矩形，但是现在没有矩形啊！那就返回空的选择内容
                    .data(dataArray) // 目前为止，我们将我们的数据Binding到Empty Selection
                    .enter()
                         .append("rect")
                         .attr("width", function(d){  return widthScale(d); })   //
                         .attr("height", 50)
                         .attr("fill", function(d){return color(d)} )
                         .attr("y", function(d, i) { return i * 100; });   // d, 表示数据， i 表示数据的索引

canvas.append("g")
     .attr("transform", "translate(0, 400)")
     .call(axis);

```

先创建坐标，然后svg对象使用call函数调用

## 讨论关于数据绑定中的Enter，Update，Exit

DOM elements < data elements  (enter)
DOM elements > data elements  (exit)
DOM elements = data elements  (update)

```js
var data = [10, 20];

var canvas = d3.select("body")
                         .append("svg")
                         .attr("width", 500)
                         .attr("height", 500)

var circle = canvas.append("circle")
                              .attr("cx", 50)
                              .attr("cy", 100)
                              .attr("r", 25)

var circles = canvas.selectAll("circle")
                    .data(data)
                    .attr("fill", "red")          // 这个其实是Update，就是我们有两个数据，但是已经有一个圆了，只需要创建一个就好了
                    .enter()
                         .append("circle")
                         .attr("cx", 50)
                         .attr("cy", 50)
                         .attr("fill", "green")
                         .attr("r", 25);
```

```js
var data = [10];

var canvas = d3.select("body")
                         .append("svg")
                         .attr("width", 500)
                         .attr("height", 500)

var circle1 = canvas.append("circle")
                              .attr("cx", 50)
                              .attr("cy", 100)
                              .attr("r", 25)

var circle2 = canvas.append("circle")
                              .attr("cx", 50)
                              .attr("cy", 200)
                              .attr("r", 25)

var circles = canvas.selectAll("circle")
                    .data(data)
                    .attr("fill", "red")
                    .exit()                         // 如果还有多余的circle，我们就使用exit函数
                         .attr("fill", "blue")
```

## 位移(Transition)

```js
var canvas = d3.select("body")
                         .append("sag")
                         .attr("width", 500)
                         .attr("height" , 500);

var circle = canvas.append("circle")
                         .attr("cx", 50)
                         .attr("cy", 50)
                         .attr("r", 25)

circle.transition()
          .duration(1500)
          .delay(1000)
          .attr("cx", 150)
          .transition()
          .attr("cy", 200)
          .transition()
          .attr("cx", 50);

circle.transition()
          .duration(1500)
          .delay(1000)
          .attr("cx", 150)
          .each("end", function() { d3.select(this). attr("fill", "red") });  // 这里的end可以换成start等，也就是在关键事件触发。

```

D3与数组常见操作

```js
var data = [10, 20, 30, 40, 50];

data.shift();                         // 取出第一个值
data.sort(d3.descending);  // 倒序
d3.max(data)                  //  获取最大值
d3.extent(data)               // 获取值域，结果为[10, 50]
d3.sum(data);
d3.mean(data);
d3.median(data);
d3.shuffle(data); //打乱顺序

data.forEach(function(d){

});
```

导入外部数据

```json
// #mydata.json
[
     {"name": "Maria", "age": 10},
     {"name": "Fred", "age": 50},
     {"name":"", "age": 60}
]
```

```js 
d3.json("mydata.json", function(data){

     var canvas = d3.select("body").append("svg")
                               .attr("width", 500)
                               .attr("height", 500)

     canvas.selectAll("rect")
               .data(data)
               .enter()
                    .append("rect")
                    .attr("width", function(d) { return d.age * 10})
                    .attr("height", 48)
                    .attr("y", function(d, i){ return i * 50})
                    .attr("fill", "blue")

     canvas.selectAll("text")
               .data(data)
               .enter()
                    .append("text")
                    .attr("fill", "white")
                    .attr("y", function(d, i){ return i * 50 + 24})
                    .text(function(d) { return d.name; })
});

```

## Path

SVG的组件之一，可以用来创建任何形状
Path Generator

```js 
var data = [
     {x:10,  y: 20},
     {x: 40, y: 60},
     {x: 50, y: 70},
];

var group = canvas.append("g")
     .attr("transform", "translate(100, 100)");

var line = d3.svg.line()
     .x(function(d) {return d.x})
     .y(function(d) {return d.y});

group.selectAll("path")
          .data([data])
          .enter("path")
          .append("path")
          .attr("d", line)
          .attr("fill", "none")
          .attr("stroke", "#000")
          .attr("stroke-width", 10)
```

这是比较简单的路径绘制，来绘制个更加复杂的吧！
那就来绘制个弧形！

```js
var data = [
     {x:10,  y: 20},
     {x: 40, y: 60},
     {x: 50, y: 70},
];

var group = canvas.append("g")
     .attr("transform", "translate(100, 100)");

var r = 100;
var p = Math.PI * 2;

var arc = d3.svg.arc()
               .innerRadius( r - 20)
               .outerRadius( r )
               .startAngle(0)
               .endAngle(p - 1)

group.append("path")
          .attr("d", arc)
```

那么我们就可以绘制饼状图了：

```js
var data = [10, 50, 80];
var r = 300;

var color = d3.scale.ordinal()
          .range(["red", "blue", "orange"]);

var canvas = d3.select("body").append("svg")
                               .attr("width", 1500)
                               .attr("height", 1500)

var group = canvas.append("g")
     .attr("transform", "translate(300, 300)");

var arc = d3.svg.arc()
     .innerRadius(200)
     .outerRadius(r);

// 接下来我们就要看看Layout
var pie = d3.layout.pie()
     .value(function(d) { return d: })

var arcs = group.selectAll(".arc")
     .data(pie(data))
     .enter()
     .append("g")
     .attr("class", "arc");

arcs.append("path")
     .attr("d", arc)
     .attr("fill", function(d) { return color(d.data); })

args.append("text")
     .attr("transform", function(d){ return "translate (" + arc. centroid(d) + ")"; })
     .attr("text-anchor", "middle")
     .attr("font-size", " 1.5em")
     .text(function(d) { return d.data});
```


## 关于Layout
### 树状
```js
var diagonal = d3.svg.diagonal()
     .source( {x: 10, y: 10} )
     .target( {x: 300, y: 300 } )

canvas.append("path")
     .attr("fill", "none")
     .attr("stroke", "black")
     .attr("d", diagonal)

var tree = d3.layout.tree()
     .size([400, 400])

d3.json("mydata.json", function(data){
     var nodes = tree.nodes(data);
     // console.log(nodes);
     var links = tree.links(nodes);
     //console.log(links); 它们有source 和 target

     var node = canvas.selectAll(".node")
          .data(nodes)
          .enter()
          .append("g")
               .attr("class", "node")
               .attr("transform", function(d) {return "translate(" + d.x + "," + d.y + ")"); }
               // 如果我们想横向显示
               // .attr("transform", function(d) {return "translate(" + d.y + "," + d.x + ")"); }

     node.append("circle")
          .attr("r", 5")
          .attr("fill", "steelblue");

     node.append("text")
          .text(function(d) {return d.name});

     var diagonal = d3.svg.daigonal()
          .projection(function(d) { return[d.x, d.y]; }) // 这是默认的，我们可以换成 d.y, d.x 就可以变为横向显示。

     canvas.selectAll(".link")
          .data(links)
          .enter()
          .append("path")
          .attr("class", "link")
          .attr("fill", "none")
          .attr("stroke", "#ADADAD")
          .attr("d", diagonal)
})
```

### Cluster, Pack, Bubble Layout

```js
var width = 800,
     height = 600;
var canvas = d3.select("body").append("svg")
     .attr("width", width )
     .attr("height", height)
     .append("g")
          .attr("transform ","translate(50, 50)");

var pack = d3.layout.pack()
     .size([width, height - 50])
     .padding(10);

d3.json("my data.json", function(data){
     var node = pack.nodes(data);
     //console.log(node)

     var node = canvas.selectAll(".node")
          .data(nodes)
          .enter()
          .append("g")
               .attr("class", "node")
               .attr("transform", function(d) {return "translate(" + d.x + "," + d.y + ")" ; });

      node..append("circle")
          .attr("r", function(d) { return d.r; })
          .attr("fill", "steel blue")
          .attr("opacity", 0.25)
          .attr("stroke", "#ADADAD")
          .attr("stroke-width", "2");

     node.append("text")
          .text(function(d) { return d.children ? "" : d.name; })
});
```

### 柱状图Histogram

```js
d3.csv("ages.csv", function(data){
     var map = data.map(function(i) { return parseInt(i.age) ; });

     var histogram = d3.layout.histogram()
          .bins(5)
          .(map)

     console.log(histogram ) //有dx , x, y 值
})
```