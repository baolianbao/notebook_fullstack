# SVG核心内容

## 系统论

- 目标：用来表示可缩放的矢量图形
- 组成元素：
    - 标签：<svg> <g> <rect> <circle> <eclipse> <line> <polygon> <polyline> <path><text> <stroking>
    - 属性:
        - 通过默认标签属性：width, height, cx, cy ….
        - 通过css
        - 特效：
    - 值
- 连接

参考教程：
http://www.w3schools.com/svg/default.asp

- SVG的关键元素
- SVG的坐标系统
- SVG中的主要元素（line，rect，circle， polygon和path）

## 容器
元素定位：二维坐标系统，D3中没有z，关于深度，取决于图形绘制的先后顺序

## 元素
常见元素的模式

- 标签指定是什么元素
- 元素坐标，取决于元素特征，
- 元素的关键组成部分定义，例如线的两个顶点，圆的半径等
- 元素填充色及透明度：fill, fill-opacity
- 元素的外框颜色、外框宽度，外框样式等

举例：

- line        :  x1, y1, x2,y2  stroke, stroke-width, stroke-linecap
- rect        :  x, y, width, height, stroke, stroke-width，rx, ry（弯角）
- circle      : cx, cy, r
- polygon  : points(e.g. points=“60,5 10,120 115,120” 注意这里会从60,5开始，并以它为结束 )
- path       :  d (e.g. d=“M 120 120 L 220 220, 420 120z" Note：我们使用D3创建地图时，path用得最多，就好像我们手绘一样)

          使用路径，还可以配合曲线，核心概念还是一样，就是连接关键点，区别就是在连接点与点的时候应用曲线，总过有三种曲线：

    - Cubic Bezier
    - Quadratic Bezier
    - Elliptical Arc

         这些在关于Path的文档有介绍，SVG的路径是绘制地图的主要工具，但是如果手绘，那工作量可想而知，到底该怎么做，以后说。Colorado 是什么？

Transform 形变
它可以让我们动态更新可视化，它可以附加到目前为止我们所讨论的所有元素中常用的方法：

- Traslate
- Scale
- rotate

Translate 位移
transform=“traslate(x, y)” 这是将元素移动偏移量为(x, y)，而不是绝对位置，例如
circle cx=10 cy=10, transfrom=“trasnlate(50, 50)” 那就是在cx和cy的基础上再加上50， 50

Scale 缩放
<circle cx="62" cy="62" r="50" stroke-width="5" fill="red"
   transform="scale(2,2)"></circle>
将原来的cx, cy, 半径，stroke-width放大两倍

Rotate 旋转

Grouping分组
为什么使用g元素？

- 可以让一组元素完成形变操作
- 可以同时设定一组元素的属性避免代码重复
- 对于大型的SVG节点集的形变操作，对比修改每一个节点的属性有很好的性能优势

Text文本
<text x=“250” y=“200”> Hello world! </text>
