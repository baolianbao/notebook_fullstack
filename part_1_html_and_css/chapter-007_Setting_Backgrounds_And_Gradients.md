title: 课程07：背景与渐变
date: 2016-04-08 00:00:06
tags: [html,css]
categories: HTML And CSS
---

## 概要
* 背景色
* 背景图片
* 渐变背景
* 多背景图
* CSS背景属性

背景对网站设计有很大的作用，它对网站的整体外观，感觉，建立分组，设置优先级等等都能派上用场。

通过CSS，我们可以将背景元素色画质为单色，单图，渐变色或者混合使用。

在本课程中我们将学习如何使用不同类型的背景，以及尝试使用CSS3中的和背景设置相关的几个属性。
<!--more-->

## 添加背景色
`background`和`background-color` 可以用于设置背景色，`background`可以通过简写形式接收颜色和图片值， `background-color` 仅仅可以接收纯背景色。

```css
div {
background-color: #b2b2b2;
}
```
在使用颜色值的时候，我们可以有多个选项：关键字颜色值、十六进制颜色值、RGB、RGBa、HSL或HSLa值，大部分情况下我们使用十六进制颜色，偶尔需要使用RGBa或HSLa设置透明背景色。

> 透明背景
> 当使用RGBa或HSLa设置透明背景色的时候，最好设置备选颜色以免有些浏览器不支持该特性。这样当浏览器不能识别透明背景色的时候，可以直接忽略而使用备用颜色了。
> 怎么做？
> CSS的Cascade是从上到下来渲染的，因此我们可以在同一处设置两个背景色。第一个`background-color` 用于做安全色，第二个用来设置RGBa和HSLa值，这样的话，如果浏览器可以识别，就会使用RGBa或HSLa颜色，如果不可以就使用纯色。
> ```css
> div {
>   background-color: #b2b2b2;
>   background-color: rgba(0, 0, 0, .3);
> }
> ```


## 添加背景图
---
除了给HTML元素设置背景色外，我们还可以使用设置背景图片，除了单单设置使用什么背景图外，还提供了很多其他的一些属性用于优化背景图片，和之前一样，我们可以使用`background` 或 `background-image`来设置背景图片， 无论使用哪种方式，我们都需要用到`url()`函数来表示图片源，该函数接收的参数是图片路径。
案例：
```css
div {
  background-image: url("alert.png");
}
```

单独使用`url`来设置背景图得到的效果可能不是我们想要的，默认情况下，背景图片会以垂直和水平方向上平铺直达填充整个页面，但是我们可以使用`background-repeat` 和`background-poistion`属性来设置图片平铺方式。

### 背景图片平铺方式
背景图片默认会水平和垂直平铺整个页面，`background-repeat` 可以用于改变平铺方式，甚至不要平铺。

```css
div {
  background-image: url("alert.png");
  background-repeat: no-repeat;
}
```
`background-repeat` 属性可以接收4个不同类型的值：
* `repeat`  ： 默认方式
* `repeat-x` ：仅仅水平方向平铺
* `repeat-y` ： 仅仅垂直方向平铺
* `no-repeat`： 不使用平铺

### 背景图定位
默认情况下背景图会定位在HTML元素左上角，但我们可以通过`background-position`来修改背景图片相对于左上角的位置。
```css
div {
  background-image: url("alert.png");
  background-position: 20px 10px;
  background-repeat: no-repeat;
}
```

该属性接收两个值：第一个值设置水平偏移量，第二个值设置垂直偏移量，如果仅仅设置了一个值，会作为水质偏移量值，垂直偏移量值会被默认设置为 50%

因为我们是从元素的左上角开始移动图片的，长度值设置的时候会以左上角为参考。

设置`background-position`的值，我们可以使用`top` `right` `bottom` `left` 和 `center` 关键字值，像素，百分比以及任何长度值。 关键字值和百分比值比较相似，关键字值`left` `top` 和百分比 `0` `0` 一样，会将图片的位置设置在元素的左上角，关键字`right` `bottom` 和百分比`100%` `100%` 对应，会将图片的位置设置到元素的右下角。


![](Fig07.01.png)
Fig 7
Background images are positioned from the left top corner of an element

使用像素设置`background-position`属性值也很常见，它可以让我们更加精确的控制偏移量。

### 设置背景图的简写方式
我们可以通过当个`background` 的简写方式来设置`background-color` `background-image` `background-position` `background-repeat`几个属性，这些属性值的设置顺序是`background-color` `background-image` `background-position` 最后是`background-repeat`。

```css
div {
  background: #b2b2b2 url("alert.png") 20px 10px no-repeat;
}
```

### 设置背景图案例
以下的案例将展示如何通过简写的`background`属性来设置背景。

需要注意的是在设置`background-position`的时候，即使用了绝对值，比如水平偏移量 20像素，也使用了相对值，比如垂直偏移量 50%。

```html
<div class="notice-success">
  Woo hoo! Congratulations, you did it!
</div>
```

```css
.notice-success {
  background: #67b11c url("tick.png") 20px 50% no-repeat;
  border: 2px solid #467813;
  border-radius: 5px;
  color: #fff;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  padding: 15px 20px 15px 50px;
}
```

## 实践
---
Returning to our Styles Conference website, let’s add some background colors. While we do that, we’ll change a few other styles to keep all of our styles working together and to keep all of our content legible.

1. We’ll begin by taking a big step and applying a blue background to the <body> element alongside the existing color and font properties. All of the styles for the <body> element rule set now include the following:
```css
body {
  background: #293f50;
  color: #888;
  font: 300 16px/22px "Lato", "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
}
```
We’ve placed a blue background on the <body> element purposely, as our website will have a few different rows of background colors, and the most frequent background color will be blue.

2. Now that every page on our Styles Conference website includes a blue background, let’s clean up a few areas that will keep that blue background. Specifically, our <header> and <footer> elements will remain blue, as will the hero section on the home page.

Within our <header> and <footer> elements let’s make all of our link colors start as white and then, when hovered over, turn the same green as our headings.

We’ll begin with our <header> element. In order to select all <a> elements within the <header> element, we’ll add a class of primary-header to the <header> element (in addition to the existing container and group classes). Don’t forget, we’ll need to add this class to the <header> elements across all of our pages.

```html
<header class="primary-header container group">
  ...
</header>
```
With the primary-header class in place on the <header> element, and the existing primary-footer class in place on the <footer> element, we can add two new rule sets to the bottom of the links section within our main.css file.

The first rule set will select all <a> elements within an element with the class attribute value of primary-header or primary-footer and set their color to white, as defined by comma separating two individual selectors that share the same property and value. The second rule set will select the same <a> elements as before but will change their color to green when a user hovers over them.

```css
.primary-header a,
.primary-footer a {
  color: #fff;
}
.primary-header a:hover,
.primary-footer a:hover {
  color: #648880;
}
```

3. While we’re making some of our text white, let’s make the text within the hero section of our home page white also, as it will remain on a blue background. We have the existing hero class rule set available to add styles to, so let’s add our white text color there. In all, our hero class rule set should include the following:
```css
.hero {
  color: #fff;
  line-height: 44px;
  padding: 22px 80px 66px 80px;
  text-align: center;
}
```

4. Also within the hero section of our home page, let’s clean up some of the button styles. We’ll begin by adding some new properties to our btn class rule set, within the buttons section of our main.css file.

Specifically, let’s set the button text color to white, make sure our cursor is always a pointer, increase the font-weight, add a small amount of letter-spacing, and change our text-transform to uppercase.

In all, our new btn class rule set should look like this:
```css
.btn {
  border-radius: 5px;
  color: #fff;
  cursor: pointer;
  display: inline-block;
  font-weight: 400;
  letter-spacing: .5px;
  margin: 0;
  text-transform: uppercase;
}
```
We’ll also clean up some of the alternate button styles by way of the btn-alt class rule set. Specifically, let’s make the buttons’ borders white and add hover styles including a white background and blue text color.

With all of the additions, our new btn-alt class rule set should look like this:

```css
.btn-alt {
  border: 1px solid #fff;
  padding: 10px 30px;
}
.btn-alt:hover {
  background: #fff;
  color: #648880;
}
```

5. Now that we have all of the areas with blue backgrounds cleaned up, let’s add styles for the rows that have white backgrounds. Let’s create a new section within our main.css file for rows, just below the clearfix section. Within this new rows section, let’s create a new class selector named row.

Within our new row class rule set, let’s add a white background, a minimum width of 960 pixels (to make sure our row elements are always larger than the width of our container or grid elements), and some vertical padding. Altogether our new row section within our main.css file should look like this:
```css
/*
  ========================================
  Rows
  ========================================
*/

.row {
  background: #fff;
  min-width: 960px;
  padding: 66px 0 44px 0;
}
```

6. With our row class styles in place, let’s add a row with a white background to our home page. We’ll do this on our teasers section. Currently this area has a <section> element with the class of grid wrapping three additional <section> elements with the classes of teaser and col-1-3.

To add a white background to this section, we’re going to wrap all of these elements in an element with the class of row.

Because we’ll want the entire teasers section wrapped in a <section> element, we’re going to add a new <section> element with the class of row that surrounds the existing <section> element with the class of grid.

Having two <section> elements wrapping the exact same content diminishes semantic value. To correct this we’ll change the second <section> element, the one with the class of grid, to a <div> element. After all, at this point this element is only adding styles, not semantic meaning, and is appropriate as a <div> element.

The structure of our new teasers element should look like this:
```html
<section class="row">
  <div class="grid">

    <!-- Speakers -->

    <section class="teaser col-1-3">
      ...
    </section><!--

    Schedule

    --><section class="teaser col-1-3">
      ...
    </section><!--

    Venue

    --><section class="teaser col-1-3">
      ...
    </section>

  </div>
</section>
```
It is amazing how a few background colors can affect the design of a website. Our Styles Conference website is coming along quite nicely, and our home page is proof.
![](Fig07.01.png)
Fig 7 Our Styles Conference website home page after adding some background colors

## 设计渐变式背景

渐变背景是在CSS3中引入的，设计师和前端的开发人员都非常开心。尽管渐变背景在老版本的浏览器中不支持，但新的浏览器都开始支持这属性。

在CSS中渐变背景是作为背景图片来处理的，也就是设计师做好了渐变背景图，然后开发人员使用。渐变背景的属性值取决于我们是使用线性还是径向渐变。

> 渐变背景的供应商前缀
> 在第四课中，我们讨论了给新的CSS属性或值添加供应商前缀，这样浏览器就可以支持当前开发中的CSS特性。 渐变背景正是需要使用供应商前缀的属性之一。 幸运的是，大部分浏览器已经淘汰为了设置渐变背景而添加供应商请罪的要求。 但是，为了保证最大程度的支持，添加该供应商前缀还是有必要的。
> 首先我们讨论线性渐变背景，其中会包含每个供应商前缀。之后大胆点忽略供应商前缀讲解径向渐变。

### 线性渐变背景
长期以来设计师和开发人员对做渐变背景很头疼知道CSS开始支持[线性渐变背景](http://dev.opera.com/articles/css3-linear-gradients/)。有了它，如果有要修改颜色之类的需求，不需要再次切图上传之类的，直接修改CSS就可以了。

```css
div {
  background: #466368;
  background: -webkit-linear-gradient(#648880, #293f50);
  background:    -moz-linear-gradient(#648880, #293f50);
  background:         linear-gradient(#648880, #293f50);
}
```

线性渐变是通过在`background` 或`background-image`属性中使用`linear-gradient()` 函数来定义的。该函数必须输入两个参数，第一个参数是开始颜色值，第二个参数是结束颜色值。浏览器会处理过渡。
在使用渐变之前，我们先设置纯色，用作备用颜色，这样万一浏览器不支持渐变色还饿可以使用该背景色。

### 修改渐变背景的渐变方向
默认情况下，线性渐变的方式是从元素的顶端到底部渐变。然而渐变方向可以通过在颜色值之前添加关键字或度数来修改。

例如，我们想将渐变方向设置为从元素的左侧到右侧，我们可以使用`to right` 关键字来实现，同理，如果我们想将渐变方向设置为从元素的左上角到右下角，我们可以使用`to right bottom` 关键字。
```css
div {
  background: #466368;
  background: linear-gradient(to right bottom, #648880, #293f50);
}
```

如果将对角线的渐变方向运用到一个非矩形的元素上，背景渐变则不会从一个角到另外一个角。取而代之的是，该渐变将会从元素的中心开始，在垂直方向角落（其需要处理的地方）放置一个锚点，然后？？Instead, the gradient will identify the absolute center of the element, place anchors in the perpendicular corners from where it should progress, and then move to the general direction of the corner stated within the value.  这些渐变通向的边角称为“魔性边角”，并不是绝对的，Eric Meyer在他的文章 [Liner Gradient Keywords](http://meyerweb.com/eric/thoughts/2012/04/26/lineargradient-keywords/) 中梳理了该语法。

除了关键字外，还可以输入度数值。如果我们希望渐变方向是想元素的左上角，我们可以设置度数为 `315deg`， 或者我们希望渐变方向是元素的右下角，我们可以使用`135deg`， 也就是我们可以使用 `0~360`综合那个的任何角度值。

### 径向渐变背景
通过给`background` 和 `background-image`属性使用`radial-gradient()`函数来实现。

```css
div {
  background: #466368;
  background: radial-gradient(#648880, #293f50);
}
```
径向渐变的方向冲从内到外。因此`radial-gradient()` 函数的第一个值元素中心的颜色，第二值是元素的外部值，浏览器会实现颜色从内到外的过渡。 和线性渐变主要不同的方面在于，径向渐变可以非常复杂，例如值的位置，尺寸，半径等等。我们这里只介绍简单的，如果想知道更多，查看[radial gradients](http://dev.opera.com/articles/css3-radial-gradients/)。

> CSS3渐变背景生成器
> 如果你是新手，直接使用CSS3中的渐变功能可能比较难，幸运的是，一些 [CSS3渐变生成器](http://www.cssmatic.com/gradient-generator#'\-moz\-linear\-gradient\%28left\%2C\%20rgba\%28248\%2C80\%2C50\%2C1\%29\%200\%25\%2C\%20rgba\%28241\%2C111\%2C92\%2C1\%29\%2050\%25\%2C\%20rgba\%28246\%2C41\%2C12\%2C1\%29\%2051\%25\%2C\%20rgba\%28240\%2C47\%2C23\%2C1\%29\%2071\%25\%2C\%20rgba\%28231\%2C56\%2C39\%2C1\%29\%20100\%25\%29\%3B') 相应而生。它们各自工作方式各不相同，如果感兴趣，可以尝试。

### 渐变色标
最简单的情况下，渐变背景会从一个颜色渐变到另外一个颜色，然而我们可以在渐变中添加多个颜色，浏览器会在它们直接过渡。要实现这个效果，我们需要在给定的渐变函数中添加色标就可以。

```css
div {
  background: #648880;
  background: linear-gradient(to right, #f6f1d3, #648880, #293f50);
}
```

默认情况下浏览器会给每两个色标之间分配相同的距离，如果想给它们设置不同的比重，可以通过设置百分比（其他长度值可以么？）来完成If more control over how colors are positioned is desired, a location along the gradient may be identified for each color stop. The location should be declared as a length value and should fall after the color value.
```css
div {
  background: #648880;
  background: linear-gradient(to right, #f6f1d3, #648880 85%, #293f50);
}
```
除非特别指定，第一个色标会位于`0%`，最后一个颜色会位于`100%`。

### 渐变背景案例
和上面的案例相似，我们将原来的背景图片换成线性渐变的背景。

```html
<div class="notice-success">
  Woo hoo! Congratulations, you did it!
</div>
```

```css
.notice-success {
  background: #67b11c;
  background: linear-gradient(#72c41f, #5c9e19);
  border: 2px solid #467813;
  border-radius: 5px;
  color: #fff;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  padding: 15px 20px;
}
```








## 实践
---
With gradient backgrounds now in the mix, let’s create a new row for our Styles Conference website, this time using a gradient.
1. We’ll create a new row with a gradient background by using the class of row-alt. Because the new row will share the same min-width property and value as the row class selector, we’ll combine these two selectors.

```css
.row,
.row-alt {
  min-width: 960px;
}
```
Next we’ll want to create new rule sets to apply styles specifically to the row-alt class selector. These new styles will include a gradient background that starts with green and transitions to yellow, from left to right.

Using the linear-gradient() function with the appropriate values and vendor prefixes, we’ll add the gradient background to the row-alt class rule set. We’ll also include a single background color before the gradient background as a fallback, just in case a browser doesn’t support gradient backgrounds.

Lastly, we’ll also add in some vertical padding. Our updated row section now looks like this:
```css
.row,
.row-alt{
  min-width: 960px;
}
.row {
  background: #fff;
  padding: 66px 0 44px 0;
}
.row-alt {
   background: #cbe2c1;
   background: -webkit-linear-gradient(to right, #a1d3b0, #f6f1d3);
   background: -moz-linear-gradient(to right, #a1d3b0, #f6f1d3);
   background: linear-gradient(to right, #a1d3b0, #f6f1d3);
   padding: 44px 0 22px 0;
 }
```

2. With our row-alt styles in place, let’s put them to use on all of our interior pages. Currently, all of our interior pages have a <section> element with a class of container. Then, inside each <section> element is an <h1> element containing the heading of the page.

We’re going to alter these <section> elements much like we did the teaser <section> element on our home page. We’ll wrap each <section> element with a class of container in a <section> element with the class of row-alt. We’ll then change each <section> element with a class of container to a <div> element for better semantic alignment.

Each of our interior pages should now include the following:
```html
<section class="row-alt">
  <div class="container">

    <h1>...</h1>

  </div>
</section>
```
3.Because we are updating our interior pages, let’s make their introductions, or leads, a little more appealing. We’ll begin by adding a paragraph introducing each page just below the <h1> element in each <section> element with a class of row-alt. Our speakers.html page, for example, may now include the following lead section:
```html
<section class="row-alt">
  <div class="container">

    <h1>Speakers</h1>

    <p>We&#8217;re happy to welcome over twenty speakers to present on the industry&#8217;s latest technologies. Prepare for an inspiration extravaganza.</p>

  </div>
</section>
```

4. In addition to inserting the paragraph, let’s also change some of the styles within the lead section. To do this, we’ll add a class of lead to the <div> element that already has a class of container; this can be found nested directly inside the <section> element with a class of row-alt. Our lead section for each interior page will now look like this:
```html
<section class="row-alt">
  <div class="lead container">

    ...

  </div>
</section>
```

5. Once the lead class is in place, we’ll center all of the text within these <div> elements. We’ll also increase the font-size and line-height of any paragraphs within these <div> elements.

We’ll create a new section for leads within our main.css file, just below the typography section, and add the following styles:
```css
/*
  ========================================
  Leads
  ========================================
*/

.lead {
  text-align: center;
}
.lead p {
  font-size: 21px;
  line-height: 33px;
}
```
The interior pages of our Styles Conference website have now received some long-overdue love in the form of gradient background rows and leads. Make sure to review the code for all of the interior pages to see their newly enhanced content, headings, and paragraphs.

![](Fig07.02.png)

Fig 7 The Speakers page of our Styles Conference website, complete with a gradient background row

## Demo和源码
* [Demo](http://learn.shayhowe.com/practice/setting-backgrounds-and-gradients/index.html)
* [源码](http://learn.shayhowe.com/practice/setting-backgrounds-and-gradients.zip)

## 使用多个背景图片
长期以来，HTML元素只允许一次只允许设置一个背景图，这给我们设计网页时候带来很多约束。幸运的是在CSS3中，在`background` 和`background-image`属性中通过赋给其多个值，每个值之间通过逗号分隔，就能实现添加多个背景图的需求。

属性值的第一个值是靠前的背景图，排在最后的也是最靠后的，其他的图片按照顺序。以下是`<div>` 元素使用了三张背景图的案例：
```css
div {
  background:  url("foreground.png") 0 0 no-repeat, url("middle-ground.png") 0 0 no-repeat, url("background.png") 0 0 no-repeat;
}
```

以上的案例中使用了设置背景的简写形式，但也可以通过以逗号分隔的`background-image` `background-position` `background-position` 来表示。

### 多背景图案例
让我们再次回到上面的案例，这次我们将混合背景图片好线性渐变背景图片。
要实现这个效果，我们需要在第二个`background`属性中设置两个值，第一个值，也就是靠前的图片，会是tick图片，第二个值，也就较远的图，将回事线性渐变，两个值通过逗号分隔。
```html
<div class="notice-success">
  Woo hoo! Congratulations, you did it!
</div>
```

```css
.notice-success {
  background: #67b11c;
  background: url("tick.png") 20px 50% no-repeat, linear-gradient(#72c41f, #5c9e19);
  border: 2px solid #467813;
  border-radius: 5px;
  color: #fff;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  padding: 15px 20px 15px 50px;
}
```
## 探索新的背景属性
除了渐变背景和多图背景的特性外，CSS3还介绍 了3个[新的CSS特性](http://css3files.com/background/):
* `background-size` ：可以让我们设置背景图的尺寸；
* `backgroud-clip`： 裁剪图片的哪个部分
* `background-origin` ：背景图位于元素哪里（例如在边框内，在内边距以内）

### CSS3背景图尺寸
`background-size` ：可以让我们设置背景图的尺寸，可以接收几种不同种类的值，包括长度和关键字值。

当使用长度值的时候，我们可以通过值来指定宽高，第一个值表示宽度，第二表示高度，需要注意的是，百分比值以HTML元素被参考，而不是以背景图片为参考。
自然而然的，谁知`background-size` 属性中宽度为 `100%`的时候会让背景图占据元素的整个宽度，如果第二值没有设定的画，则会按照图片的比例设置。

关键字`auto` 可以用于设置宽度或高度值来位置背景图的宽高比例。例如，如果我们希望将图片的高度设为HTML元素高度的`75%` 并同时保持图片的宽高比，则可以惊啊`background-size`属性值设置为 `auto 75%`

```css
div {
  background: url("shay.jpg") 0 0 no-repeat;
  background-size: auto 75%;
  border: 2px dashed #9799a7;
  height: 240px;
  width: 200px;
}
```

### 覆盖和包含关键字值
`background-size`属性值除了可以用长度来表示外，还可以使用`cover` `contain`关键字来使用。

`cover` 关键字会将背景图调整到和HTML元素宽度和高度完全一致的尺寸。The cover keyword value specifies that the background image will be resized to completely cover an element’s width and height. The background image’s original aspect ratio will be preserved, yet the image will stretch or shrink as necessary to cover the entire element. Often when using the cover keyword value, part of the background image is cut off in order for the image to occupy the full available space of the element.

The contain keyword value, on the other hand, specifies that the background image will be resized to reside entirely contained within an element’s width and height. In doing so the background image’s original aspect ratio will be preserved, but the image will stretch or shrink as necessary to remain within the width and height of the element. In contrast with the cover keyword value, the contain keyword value will always show the full background image; however, oftentimes it will not occupy the full available space of the element.

Both the cover and contain keyword values may result in slightly distorted background images, particularly when the images are stretched beyond their original dimensions. We’ll want to keep an eye out for this when using these values, to make sure the resulting styles are satisfactory.

### CSS3背景图片段和Background Origin
The background-clip property specifies the surface area a background image will cover, and the background-origin property specifies where the background-position should originate. The introduction of these two new properties corresponds with the introduction of three new keyword values: border-box, padding-box, and content-box. Each of these three values may be used for the background-clip and background-origin properties.

```css
div {
  background: url("shay.jpg") 0 0 no-repeat;
  background-clip: padding-box;
  background-origin: border-box;
}
```
The background-clip property value is set to border-box by default, allowing a background image to extend into the same area as any border. Meanwhile, the background-origin property value is set to padding-box by default, allowing the beginning of a background image to extend into the padding of an element.

![](Fig07.04.png)
Fig 7
The border-box value extends the background into the border of an element

![](Fig07.05.png)
Fig 7
The border-box value extends the background into the border of an element

![](Fig07.06.png)
Fig 7
The border-box value extends the background into the border of an element

We first discussed these keyword values when we covered the box-sizing property back in Lesson 4, “Opening the Box Model.” The values themselves haven’t changed in meaning, but their functions do change with the use of the different background properties.

## 总结
给页面添加背景和渐变让我们将色彩带到设计的最前沿。同时也帮助我们定义内容是如何分组的从而提高页面的整体布局。

简单回顾：
* 如何给HTML元素添加背景色和背景图片
* CSS线性渐变和径向渐变，以及如何定义。
* 如何给单个HTML元素赋予多个背景图
* 新的CSS3属性让我们可以修改背景图的尺寸，覆盖区域以及背景图的中心。

添加背景色，渐变、背景图等给提升页面的整体设计带来了更多的可能性，很快我们就会讨论如何语义化在网页中添加图片（背景图除外）和其他多媒体，但在此之前，我们看看如何语义化创建列表。

## 资源与链接
* [CSS3 Linear Gradients](http://dev.opera.com/articles/css3-linear-gradients/) via Dev.Opera  
* [CSS3 Radial Gradients](http://dev.opera.com/articles/css3-radial-gradients/) via Dev.Opera
* [CSSmatic Gradient Generator](http://www.cssmatic.com/gradient-generator)
* [CSS3 Files Background](http://css3files.com/background/)


## 课程链接
* [课程06：排版](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_06_Working_with_Typography.md)
* [课程08：创建列表](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_08_Creating_Lists.md)
