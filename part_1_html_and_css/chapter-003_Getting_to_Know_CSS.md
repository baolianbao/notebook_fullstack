title: 课程03：了解CSS
date: 2016-04-08 00:00:10
tags: [html,css]
categories: HTML And CSS
---

CSS是个比较强大而稍微复杂的语言。

其让我们对页面进行布局与设计，其可以在不同的元素、页面分享这些样式。 在解锁它全部的技能之前，我们需要对这个语言的几个方面有完全的掌握。

首先，至关重要的是理解样式是如何渲染的。更加具体来说是需要知道不同种类的选择器是如何工作的，这些选择器的先后顺序是怎样影响样式的渲染的。我们还需要知道在CSS中不断出现和常用的属性值，尤其是那些颜色和距离。

下面就仔细探讨一下CSS是如何工作的吧？
<!--more-->

## 层叠样式 Cascade
We’ll begin breaking down exactly how styles are rendered by looking at what is known as the cascade and studying a few examples of the cascade in action. Within CSS, all styles cascade from the top of a style sheet to the bottom, allowing different styles to be added or overwritten as the style sheet progresses.我们将通过所谓的级联（Cascade）和一些Cascade案例来彻底了解样式（布局和设计）是如何渲染的。在CSS中所有的样式层叠从头到尾，允许添加或重写不同样式。

例如在样式表的上部分，我们选择了所有的段落元素设置其背景色为orange，它们的字体尺寸为24像素。然后在样式表的下部分，我们依旧选择所有的段落元素，然后设置其背景色为绿色，如下所示：

```css
p {
  background: orange;
  font-size: 24px;
}
p {
  background: green;
}
```

由于继设置段落背景色orange之后又设置其背景色为green，在cascade中其优先级别较高，所有的段落的背景都会是绿色的（下面的优先级高于上面的）。由于第二个选择器没有定义字体的尺寸，所以字体尺寸仍然是24。

### Cascade 属性
除了在不同的选择器之外Cascade发挥作用外，在同一个选择器内也有用。例如，我们选择所有的段落元素然后设置它们的背景为orange，紧接其后，我们有设置背景属性值为green，代码如下：

```css
p {
  background: orange;
  background: green;
}
```

由于设置green背景颜色在设置orange背景颜色之后，其会覆盖原来的orange背景色，和之前一样，我们的段落依旧会是绿色的。

All styles will cascade from the top of our style sheet to the bottom of our style sheet. There are, however, times where the cascade doesn’t play so nicely. Those times occur when different types of selectors are used and the specificity of those selectors breaks the cascade.样式表内从上到下所有的样式都是后面的层叠在前面的。然而这样的层叠效果并不总是如我们所愿。它们会在我们使用不同类型的选择器的时候发生这写不同类型的选择器会破坏原来的层叠样式。下面我们就探讨一下（高级的覆盖低级的，下面的覆盖上面的 ）。

## Calculating Specificity
CSS中每个选择器都有特定的权重。A selector’s specificity weight, along with its placement in the cascade, identifies how its styles will be rendered.一个选择器的权重，随着其放置到Cascade中，决定了它的样式是怎样被渲染的。

在课程一中，我们讨论了类型选择器、类选择器和ID选择器，每种选择器都有不同的权重。
类型选择器的权重最低，他的点值是 0 – 0 -1
类选择器  的权重中等，它的点值是 0 – 1 – 0
ID选择器  的权重较高，它的点值是 1- 0 – 0

正如我们看到的，使用了3列来权重点数的计算，第一列计算ID选择器，第二列计算类选择器， 第三列计算类型选择器。也就是需要明确的是，ID选择器的权重高于类选择器，高于类型选择器。

> Specificity Points
> Specificity points are intentionally hyphenated, as their values are not computed from a base of 10. Class selectors do not hold a point value of 10, and ID selectors do not hold a point value of 100. Instead, these points should be read as 0-1-0 and 1-0-0 respectively. 
> We’ll take a closer look at why these point values are hyphenated shortly, when we combine selectors.


如果我们各自通过类型选择器 和 ID选择器选择了段落元素，ID选择器的优先级比类型选择器的优先级高，无论ID选择器放在Cascade的什么位置。

`HTML`

```html
<p id="food">...</p>
```

`CSS`

```css
#food {
  background: green;
}
p {
  background: orange;
}
```

如上的代码中段落元素有id属性值为food，在CSS中，我们通过两种类型的选择器选择了该段落，一个是类型选择器、一个是ID选择器，尽管在Cascade中我们将类型选择器放在ID选择器的后面，ID选择器的优先级高于类型选择器，因此段落的背景色是green.

记住不同类型的选择器的权重非常重要。

理解Cascade的工作原理以及不同选择器的权重，我们以后会继续讨论这个话题，现在我们讨论下如何混合使用这些选择器，记住，当我们混合选择器之后，它们的权重会相应变化。

## 混合选择器
目前位置我们都是单独使用选择器，掌握混合使用选择器会帮我们更加精确的选择某个元素或某组元素。

假设我们想选择位于class属性值为hotdog内的所有段落元素，将其背景色设置为brown，同时，在这些段落中恰巧有个段落的class属性值为mustard，我们想将它的背景色设置为yellow，那么我们的HTML和CSS看起来可能如下：

`HTML`

```html
<div class="hotdog">
  <p>...</p>
  <p>...</p>
  <p class="mustard">...</p>
</div>
```

`CSS`

```css
.hotdog p {
  background: brown;
}
.hotdog p.mustard {
  background: yellow;
}
```


当我们混合使用选择器的时候，它们应当从右向左读。
在花括号之前的一个选择器称为关键选择器。 关键选择器表明了该样式会应用到什么元素上。所有出现在关键选择器之前的选择器都称为预修饰符。

解析：
第一个混合选择器，.hotdog p 包含了两个选择器：一个类选择器，一个类型选择器，它们之间通过单个空格分开。关键选择器是指向段落元素的类型选择器。由于这个混合选择器使用了hotdog类选择器这样的预编译符。这样的混合选择器就会仅仅选择位于class属性值为hotdog内的所有段落元素。

第二个混合选择器， .hotdog p.mustard，包含了3个选择器：两个类选择器和一个类型选择器。

> 选择器之间的间隔
> 上面的选择器 .hotdog p.mustard， 在hotdot类选择器和段落选择器之间有空格，但段落选择器和其后的mustard类选择器没有空格。 使用或遗漏空格会使得选择器有很大的不同。
> 
> 由于段落选择器和mustard类选择器之间没有空格这表示选择器仅仅会选择class属性值为mustard的段落元素。如果去掉段落选择器，且mustard类选择器左右都有空格，那么其会选择所有class属性为mustard的元素，而不仅仅是段落元素。
> 
> 最好的用法是不要在类选择器使用类型选择器前缀。
>
> 一般来说我们希望选择给定class的所有元素，而不是某一类型的元素。
> 
> 根据这样的最佳的做法，我们的新的混合选择器.hotdog .mustard比较好。

不同的选择器可以混合起来指向页面中的某个元素。在以后我们会使用不同的混合选择器，我们会了解到它们是多么强大。 在此之前，我们来了解下混合选择器是如何改变了选择器的权重的？

### 混合选择器的权重
当我们混合选择器的同时，这些彼此独立的选择器的权重也混合了。
这些混合选择器的权重的计算方式可以通过统计每个类型选择器出现的次数来知道。
如上 .hotdog p 选择器由两个选择器器组成
.hotdog   0-1-0
P         0-0-1
结果是    0-1-1

而.hotdog p.mustard 选择器有三个选择器组成：
.hotdog   0-1-0
P         0-0-1
.mustard  0-1-0
结果是    0-2-1

这两个混合选择器很显然，第二个选择器的权重点数比第一个选择器的权重点数高，在Cascade中，第二个混合选择器的优先级比较高，所以即使我们改变了其所在CSS中的位置也不会改变样式外观

```css
.hotdog p.mustard {
  background: yellow;
}
.hotdog p {
  background: brown;
}
```
通常情况下，我们需要时刻注意着选择器的权重。我们选择器的权重越高，我们的Cascade破坏的可能性越高。


## 通过多类对样式分层
有个途径可以让我们的选择器的权重尽量低，那就是尽量模块化，在元素之间共享类似的样式。有一个方法能实现尽可能模块化，就是使用多个类来对样式进行分层。

HTML中的元素可以有多个class属性值，只要它们之间用空格分开。With that, we can place certain styles on all elements of one sort while placing other styles only on specific elements of that sort. 通过它，我们将

We can tie styles we want to continually reuse to one class and layer on additional styles from another class.

例如看看一些按钮示例， 假设我们希望所有的字体为16像素，但我们希望根据不同的使用给按钮设置不同的背景色。我们可以创建几个类并按照需求放到HTML元素中来实现想要的样式

`HTML`

```html
<a class="btn btn-danger">...</a>
<a class="btn btn-success">...</a>
```

`CSS`

```css
.btn {
  font-size: 16px;
}
.btn-danger {
  background: red;
}
.btn-success {
  background: green;
}
```

如上，我们看到两个锚元素，它们都有多个class属性值，第一个class属性值btn为每个元素应用了16像素的字体，然后第一个元素使用了一个额外的btn-dange属性值，用于应用红色背景，类似第二个元素使用了额外的btn-success属性值来应用green背景色。这样我们的样式就更加清晰、模块化。

Using multiple classes, we can layer on as many styles as we wish, keeping our code lean and our specificity weights low. 和理解Cascade 及计算权重一样，随着实践，我们会越来月熟练掌握。

## 常见的CSS属性值
到目前位置，我们已经使用了几个常见的CSS属性值了，比如color，以及其值为red, green之类的。

下面我们就看看有哪些常用的属性值，尤其是颜色和长度。

### 颜色
在CSS中所有的颜色值都是通过sRGB颜色空间来定义的，在这个颜色空间内的颜色都是通过混合红，绿，蓝颜色通道，和电视机、显示器一样。通过混合我们可以创建上百万的颜色，几乎可以找到任何我们想要的颜色。

目前在CSS中，主要有4种表示颜色的方式：关键字，十六进制、RGB值和HSL值。
#### 关键字颜色
关键字颜色也就是名字（例如red, green，或者blue）对应颜色，其名字和对应的颜色是有CSS所指定的，大部分常见及少部分奇怪的颜色都有关键字名称。
完整的CSS关键字名称颜色列表可以在[CSS specification](http://www.w3.org/TR/css3-color/)找到
[!](Fig03.x.png)
下面的案例中，我们将背景色maroon运用到所有类属性值为task的HTML元素，将背景色yellow应用到所有类属性值为count的HTML元素
```css
.task {
  background: maroon;
}
.count {
  background: yellow;
}
```

关键字颜色非常简单，提供的选项有限，因此并不是最受欢迎的颜色选择。While keyword color values are simple in nature, they provide limited options and thus are not the most popular color value choice.

#### 十六进制颜色
十六进制颜色有#后跟上3个或6个字符组成。字符串的范围是0~9，a~f，不区分大小写，这些值对应红，绿，蓝三个颜色通道。

如果是用6个字符表示，那么前两个字符表示红色通道，中间两个字符字符表示绿色通道，最后两个字符表示蓝色通道，如果是3个字符，第一个字符表示红色通道，中间字符表示绿色通道，最后一个字符表示蓝色通道。如果6个字符的前两个字符相同，中间两个字符相同，后两个字符相同，那么就可以使用3个字符的缩写，例如#ff6600可以简写成#f60
(!images/Fig.03.02)
Fig 3
Six-character hexadecimal values may be written as three-character hexadecimal values when the red, green, and blue color channels each contain a repeating character
The character pairs are obtained by converting 0 through 255 into a base-16, or hexadecimal, format. The math is a little tricky—and worthy of its own book—but it helps to know that 0 equals black and f equals white.

> The Millions of Hexadecimal Colors
> 有上千万的十六进制的颜色，大约1670多万
> 在16进制颜色中，每个字符都有16中可能性，There are 16 options for every character in a hexadecimal color, 0 through 9 and a through f. With the characters grouped in pairs, there are 256 color options per pair (16 multiplied by 16, or 16 squared).

And with three groups of 256 color options we have a total of over 16.7 million colors (256 multiplied by 256 multiplied by 256, or 256 cubed).

使用和上文所提到的maroon和Yellow颜色，我们需要将关键字颜色改为十六进制颜色，示例如下：

```css
.task {
  background: #800000;
}
.count {
  background: #ff0;
}
```
16进制颜色由来已久，由于其可以提供大量的颜色让其越来越受欢迎。但如果你不熟悉它使用起来就不顺手，幸运的是Adobe创建了[Adobe Color CC](https://color.adobe.com/zh/create/color-wheel/)可以帮我们找到任何我们想要的颜色所对应的16进制值。
此外，大部分图像编辑应用，例如Adobe Photoshop，提供查找16进制颜色的功能。
[!images/]
Fig 3
The color picker tool within Adobe Photoshop displays the hexadecimal and RGB color values

#### RGB & RGBa颜色
RGB颜色值使用了rgb()函数，接收三个0~255的参数，分别用来表示红色通道，绿色通道，蓝色通道三种颜色，0表示纯黑，255表示纯白。

如果想用RGB颜色值来创建上面所提到的shade of orange，它的值应该是rgb(244, 102, 0);

同样，如上文提到的maroon和yellow背景色，可以使用RGB颜色值来替代关键字颜色或16进制颜色值

```css
.task {
  background: rgb(128, 0, 0);
}
.count {
  background: rgb(255, 255, 0);
}
```

RGB颜色值通过rgba()函数，还可以包括alpha通道或者透明通道，rgba()函数必须有第4个参数，该参数的范围是0~1，包含小数。 如果为0 则表示完全透明，1表示完全不透明。在0~1直接的值都会生成相应的透明的颜色。

假设我们将shade of orange的透明度设置为 50%， 那么其对应的RGB值就是rgba(255, 10, 0, .5)。

同样我们也可以修改背景色maroon 和yellow的透明度，下面的示例中，我们将maroon背景色设置为 25%， yellow的背景色为完全不透明

```css
.task {
  background: rgba(128, 0, 0, .25);
}
.count {
  background: rgba(255, 255, 0, 1);
}
```

RGB 颜色值也越来越受欢迎，尤其是在其提供了透明度的功能。



#### HSL & HSLa 颜色
HSL颜色值使用hsl()函数，其接收三个参数，分别用于表示 hue, saturation, 和 lightness.

hue值是一个0~360无单位的值，其0~360表示了色环，它的值表示色环中颜色的角度。
saturation和lightness都是0 ~ 100%的百分比值，saturation值用来表示色相的饱和度，0表示grayscale，灰阶， 100%表示完全饱和。亮度表示色相的亮度值， 0 表示纯黑，100%表示全白。

回到我们的shade of orange颜色上，如果用HSL颜色表示，那么应该是hsl(24, 100%, 50%);
我们的maroon和yello背景色也可以用HSL值表示，代码如下：
```css
.task {
  background: hsl(0, 100%, 25%);
}
.count {
  background: hsl(60, 100%, 50%);
}
```

和RGBa一样，HSL颜色值也可以通过hsla()函数包含alpha或透明通道，它的第4个参数的作用和rgba()函数中第4个参数作用一致。

如果我们希望将shade of orange的透明度设为50%，那么可以用hsla(24, 100%, 50%, .5)来表示

同样，25%透明度的maroon背景色，和完全不透明的yellow背景色可以使用如下的HSLa颜色值表示：

```css
.task {
  background: hsla(0, 100%, 25%, .25);
}
.count {
  background: hsla(60, 100%, 50%, 1);
}
```

在CSS中，HSL颜色值是新增的，由于其出现的时间不久且各个浏览器支持程度，它还未广泛应用。

长时间以来，16进制的颜色使用比较广泛，由于透明度的需要，RGBa颜色由倍受推崇，这些偏好在未来也许会改变，目前为止，我们将使用16进制和RGBa颜色值。


### 长度
CSS中的长度值和颜色相似，也有几种不同类型的长度值，它们都在不同的场合下使用。长度值有两种形式，绝对长度和相对长度，它们分别使用不同的单位来度量。

现在，我们集中了解常用也比较直白的值，其他更加复杂，强大的值，现在我们也用不着。


#### 绝对长度
绝度长度值是最简单的长度值，和英尺、厘米、米一样物理测量都是固定的，最常用的测量单位是像素，我们用px表示。

##### 像素
一个像素等于1/96英尺。 实际测量像素时，由于设备的密度问题可能会有偏差  The exact measurement of a pixel, however, may vary slightly between high-density and low-density viewing devices.

像素已经使用很久了，经常用于不同的属性。以下的代码将所有的段落的字体尺寸设置为14像素

```css
p {
  font-size: 14px;
}
```

随着各种可视设备及其屏幕尺寸的变化，像素不再如之前那样受欢迎。 作为测量的绝对单位，没有带多的灵活性。但使用像素是个很好的开始。在学习HTML和CSS的过程中它正如绳索一样。With the changing landscape of viewing devices and their varying screen sizes, pixels have lost some of their popularity. As an absolute unit of measurement, they don’t provide too much flexibility. Pixels are, however, trustworthy and great for getting started. We’re going to lean on them quite a bit as we’re learning the ropes of HTML and CSS.


#### 相对长度
和绝对长度对应的是相对长度，相对长度稍微复杂些，它们不是固定的测量单位，其依赖与其它测量长度。


##### 百分比
百分比的单位是%，是最受欢迎的相对值。定义百分比长度和其他对象的长度。例如，设置HTML元素的width值为 50%， 我们就必须知道其父元素，也就是当前元素嵌套在那个元素，然后定义其宽度是父元素宽度的50%

```css
.col {
  width: 50%;
}
```

上面的案例中，我们设置类属性值为col的元素的width值为50%， 该50%会基于其父元素的宽度值计算。
在网页布局及设置元素的宽高时候尤其有用，We’re going to rely on them often to help us out in these areas.


##### Em
作为相对值，em单位也比较受欢迎。em单位使用em单位符合表示，其长度计算基于一个元素的字体尺寸。

一个em单位等于该元素的字体尺寸，因此，如果一个元素的字体的尺寸是14像素，且其宽度是 5em， 那么宽度也就是 70像素（14 * 5）

```css
.banner {
  font-size: 14px;
  width: 5em;
}
```

当一个元素的字体尺寸未明确规定时候，该em单位将会参考其最近的明确规定字体尺寸的父元素。

em单位通常用于文本样式，例如字体尺寸，间隔，边距等等，我们将在第六课 排版中深入讨论。

除了上面提到的以外，其他还有很多绝对和相对值的测量单位。然而，像素，百分百和em这三个单位，使用得最广泛，也是主要使用的。


## 总结
在本节课中我们没有继续更新我们嗯的Sytles Conference网站，我们在学习CSS基础，掌握了CSS的工作原理以及我们肯定要用到的常见的值。

简单回顾一下，本节课中，我们讨论了如下的内容：
* 样式表是如何从上到下层叠的
* 权重是什么，怎么计算的
* 如何混合选择器来选择特定元素或一组元素
* How to use multiple classes on a single element to layer on different styles for more modular code
* CSS中使用的不同种类的颜色值，包括关键字，十六进制，RGB和HSL值
* CSS中使用的不同类型的长度值，包括像素，百分比和em单位。

我们还有很多内容需要掌握，但基础内容开始水到渠成了。在接下来的几节课中，我们会更加深入了解CSS，并且，我们的网站也终于开始有模有样了。

## 资源与链接
* [CSS Color Module](http://www.w3.org/TR/css3-color/) via W3C
* [Adobe Color CC](https://kuler.adobe.com/create/color-wheel/)
* [CSS Length Values](https://developer.mozilla.org/en-US/docs/Web/CSS/length) via Mozilla Developer Network

## 课程链接
* [课程02：了解HTML](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_02_Getting_to_Know_HTML.md)
* [课程04：Box模型解析](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_04_Opening_the_Box_Model.md)