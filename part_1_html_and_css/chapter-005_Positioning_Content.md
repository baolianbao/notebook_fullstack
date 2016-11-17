title: 课程05：内容定位
date: 2016-04-08 00:00:08
tags: [html,css]
categories: HTML And CSS
---

## 概述
* Positioning with Floats
* Positioning with Inline-Block
* Creating Reusable Layouts
* Uniquely Positioning Elements

<!--more-->
## 漂浮
CSS 强大的地方之一在于可以让我们随心所欲的将内容放在页面中任何我们想要的地方。也使我们的设计结构化，内容易于理解和消化。

CSS中有集中不同的定位方式，每个都有不同的应用场景。在本课程中我们将讨论几种不同的场景：creating reusable layouts and uniquely positioning one-off elements—and describe a few ways to go about each. 通过集中方法来实现创建可复用的布局和一次性定位元素。



### 关于float定位
页面元素的定位方法之一就是用float属性，float属性非常强大，且可以在多种场合使用。

基本情况是，float属性可以使一个元素脱离原理的页面的流布局，而让其[定位](http://www.smashingmagazine.com/2007/05/01/css-float-theory-things-you-should-know/)到父对象的左侧或者右侧。 页面中其他所有元素围绕浮动元素……？ All other elements on the page will then flow around the floated element. 假设一个<img>元素浮动到几个文本段落的一侧，那么该段落就会根据需要而环绕该图片。

如果同一时间多个元素都使用了float属性，其提供了属性可以让这几个元素一个挨着一个，也可以向反方向，正如我们看到的多列布局方式。When the float property is used on multiple elements at the same time, it provides the ability to create a layout by floating elements directly next to or opposite each other, as seen in multiple-column layouts.

float属性接收几个值，最常使用的是left和right，它让HTML元素可以漂浮到其父元素的左侧或者右侧。

```css
img {
  float: left;
}
```

### 使用float
现在我们通过在第2课介绍的<header> <section><aside><footer>几个元素来创建最上面是头部，中间有两列，下面有底部的布局，以下是HTML代码:

```html
<header>
  <code>&#60;header&#62;</code>
</header>

<section>
  <code>&#60;section&#62;</code>
</section>

<aside>
  <code>&#60;aside&#62;</code>
</aside>

<footer>
  <code>&#60;footer&#62;</code>
</footer>
```

```css
HTML  CSS   Result
Edit on 
code {
  background: #2db34a;
  border-radius: 6px;
  color: #fff;
  display: block;
  font: 14px/24px "Source Code Pro", Inconsolata, "Lucida Console", Terminal, "Courier New", Courier;
  padding: 24px 15px;
  text-align: center;
}
header,
section,
aside,
footer {
  margin: 0 1.5% 24px 1.5%;
}
footer {
  margin-bottom: 0;
}
```

如上的代码中，由于<section> <aside>元素是块元素，所以默认情况下它们是层叠的。但是现在我们想它们左右放置，让<section>位于左侧，<aside>位于右侧。我希望它们作为两列的时候向反向偏移。那么我们的CSS一概这样：
```css
section {
  float: left;
}
aside {
  float: right;
}
```

提示一下，当一个元素是浮动的时候，它会浮动到其父元素的最靠边的地方，如果它没有父元素，那么就会浮动到网页的边上。

当我们将HTML设置为浮动的时候，它就不属于常规的HTML文档中的流了。这会导致俄该元素的宽度恢复到默认内容的宽度了。有时，例如当我们想创建几个列用于布局的时候，这中情形我们并不希望看到这时候我们可以通过width属性来说修复。此外，为了放置浮动的元素相互接触，导致内容紧凑，我们可以使用margin属性来设置它们之间的间距。

下面我们将基于如上的代码块中添加margin和width属性到每列中去让我们的元素更加合理。

```css
section {
  float: left;
  margin: 0 1.5%;
  width: 63%;
}
aside {
  float: right;
  margin: 0 1.5%;
  width: 30%;
}
```

怎么样，新的结果看起来是不是好多了？

> float属性值也许会改变元素的Display属性值。
> 当我们将一个HTML元素设置为浮动的情况下，需要意识到的是，由于其已经不在原来的HTML流中了，这样会改变一个元素默认的display属性值。The float property relies on an element having a display value of block, and may alter an element’s default display value if it is not already displayed as a block-level element.
> 
> 例如，一个元素的display属性值是Inline，比如<span>这样的行内元素。会忽略任何height和width属性值。然而当我们将该元素设置为float的情况下，该元素的display值将会改为block，然后其可以接收height和width属性值了
> 当我们浮动元素的时候时刻需要盯着它们的display值是否改了。


当有两列情况下我们可以让其一个靠左一个靠右，但如果我们有多列的情况下，就需要改变实现方法了。假设在我们的网页中，中间部分需要三列：

```html
<header>...</header>
<section>...</section>
<section>...</section>
<section>...</section>
<footer>...</footer>
```

将上面代码中的三个<section>元素改为一行三列，我们可以将三个元素的float值都设置为靠左浮动，而不是，一个向左，一个向右，同时还需要调整<section>元素的width值，margin值来保证其宽度和相互间距
```css
section {
  float: left;
  margin: 0 1.5%;
  width: 30%;
}
```
现在我们就有三列了，且它们之间是等距的。

### Clearing & Containing Floats
float属性设计的最初目的是允许内容围绕图片。也就是一个图片浮动，然后内容像流水一样围绕在周围。对于图片来说目的达到了，但float属性从一开始就没有打算用于布局和定位的目的，，这也导致真正用它来完成这些任务的时候会有一些缺陷（陷阱）。

其中一个缺陷是……  One of those pitfalls is that occasionally the proper styles will not render on an element that it is sitting next to or is a parent element of a floated element.当一个元素是浮动的时候，该元素就从原来的页面流布局脱离了，结果就是围绕该元素周围的元素的样式有可能会受到不好的影响。

常常出现的情况是Margin和padding属性不能正确解读，导致它们也成为了浮动的元素，其他的一些属性也可能收到影响。

另外一个缺陷是有时，我们不期望的内容会围绕那个到浮动元素的周围。将一个元素从HTML文档流布局中移除后会导致浮动元素周围的所有元素能围绕浮动元素并消耗浮动元素周围的间隔，通常情况下都不是我们想要的。Another pitfall is that sometimes unwanted content begins to wrap around a floated element. Removing an element from the flow of the document allows all the elements around the floated element to wrap and consume any available space around the floated element, which is often undesired.

通过之前的两列的案例，在我们将<section>和<aside>元素设置为浮动之后，在我们设置其width属性值之前，<footer>元素的内容会占据任何可用的空间然后围绕在该两个元素之间及上方。相应的<footer>元素就位于<sction>和<aside>元素之间。

为了防止HTML内容围绕浮动元素，我们需要清楚或包含那些浮动内容使页面恢复到正常的流布局。接下来我们看看如何清除浮动，以及包含浮动。

#### Clearing Floats
想清除浮动需要通过clear属性，该属性接收以下几个值：left, right, both

```css
div {
  clear: left;
}
```

left值会清除左边浮动，right会清除右边的浮动，both你懂的，也是最常使用的理想值。

回到我们之前的案例中，如果我们在<footer>元素使用了both，这样我们就可以清除浮动了，It is important that this clear be applied to an element appearing after the floated elements, not before, to return the page to its normal flow.

```css
footer {
  clear: both;
}
```

#### Containing Floats
除了清除浮动外，还有个选项就是包含浮动。包含浮动的最终效果看起来和清除浮动看起的效果是一样的；然而包含浮动可以确保让我们所有的样式都被正确渲染。

要包含浮动，浮动元素必须位于一个父元素。该父元素会作为一个容器，让容器以外的所有元素和HTML文档正常的流布局一样。，该父元素的CSS通过group的类属性表示：

```css
.group:before,
.group:after {
  content: "";
  display: table;
}
.group:after {
  clear: both;
}
.group {
  clear: both;
  *zoom: 1;
}
```

代码内容看起来有点多，但基本内容用就是CSS清除class属性值为group的HTML元素内的所有浮动元素，然后返回给文档一个正常的流布局元素。
具体来说就是正如在第4课所提到的:before和:after这些伪代码，会东塔生成元素  More specifically, the :before and :after pseudo-elements, as mentioned in the Lesson 4 exercise, are dynamically generated elements above and below the element with the class of group. 

More specifically, the :before and :after pseudo-elements, as mentioned in the Lesson 4 exercise, are dynamically generated elements above and below the element with the class of group. Those elements do not include any content and are displayed as table-level elements, much like block-level elements. The dynamically generated element after the element with the class of group is clearing the floats within the element with the class of group, much like the clear from before. And lastly, the element with the class of group itself also clears any floats that may appear above it, in case a left or right float may exist. It also includes a little trickery to get older browsers to play nicely.

相比clear:both， 包含使用了更多的代码，使用了单独声明的方法，但更加有效。

看看我们之前的两列布局，现在我们可以将<section>和<aside>两个元素放到一个父元素中，该父元素需要将浮动元素包含在内，代码如下：
```html
<header>...</header>
<div class="group">
  <section>...</section>
  <aside>...</aside>
</div>
<footer>...</footer>
```

```css
.group:before,
.group:after {
  content: "";
  display: table;
}
.group:after {
  clear: both;
}
.group {
  clear: both;
  *zoom: 1;
}
section {
  float: left;
  margin: 0 1.5%;
  width: 63%;
}
aside {
  float: right;
  margin: 0 1.5%;
  width: 30%;
}
```
我们用于包含浮动元素的父元素子在其他网站一般称为"clearfix"或cf，我们选择使用了group， 它代表了一组元素，和符合。

当元素浮动的时候，随时关注它们是如何影响页面的流布局的，如果需要的画则通过清除或包含的方式来重置。如果不能搞清楚浮动元素带来的影响，会很麻烦，尤其是在页面有多行多列的情况下。


## 实践
回到Styles Conference网站项目上：

1. First things first, before we begin floating any elements, let’s provide a way to contain those floats by adding the clearfix to our CSS. Within the main.css file, just below our grid styles, let’s add the clearfix under the class name group, just like before.

```css
/*
  ========================================
  Clearfix
  ========================================
*/
.group:before,
.group:after {
  content: "";
  display: table;
}
.group:after {
  clear: both;
}
.group {
  clear: both;
  *zoom: 1;
}
```

2. Now that we can contain floats, let’s float the primary <h1> within the <header> element to the left and allow all of the other content in the header to wrap to the right of it.

To do this, let’s add a class of logo to the <h1> element. Then within our CSS, let’s add a new section of styles for the primary header. In this section we’ll select the <h1> element with the logo class and then float it to the left.

HTML

```html
<h1 class="logo">
  <a href="index.html">Styles Conference</a>
</h1>
```

CSS

```css
/*
  ========================================
  Primary header
  ========================================
*/

.logo {
  float: left;
}
```

3. While we’re at it, let’s add a little more detail to our logo. We’ll begin by placing a <br> element, or line break, between the word “Styles” and the word “Conference” to force the text of our logo to sit on two lines.

Within the CSS, let’s add a border to the top of our logo and some vertical padding to give the logo breathing room.

HTML

``` html
<h1 class="logo">
  <a href="index.html">Styles <br> Conference</a>
</h1>
```
CSS

```css
.logo {
  border-top: 4px solid #648880;
  padding: 40px 0 22px 0;
  float: left;
}
```

4. Because we floated the <h1> element, we’ll want to contain that float. The closest parent element of the <h1> element is the <header> element, so we’ll want to add the class of group to the <header> element. Doing this applies the clearfix styles we set up earlier to the <header> element.

```html
<header class="container group">
  ...
</header>
```

5. The <header> element is taking shape, so let’s take a look at the <footer> element. Much like we did with the <header> element, we’ll float our copyright to the left within the <small> element and let all other elements wrap around it to the right.

Unlike the <header> element, though, we’re not going to use a class directly on the floated element. This time we’re going to apply a class to the parent of the floated element and use a unique CSS selector to select the element and then float it.

Let’s start by adding the class of primary-footer to the <footer> element. Because we know we’ll be floating an element within the <footer> element, we should also add the class of group while we’re at it.

```html
<footer class="primary-footer container group">
  ...
</footer>
```

6. Now that the class of primary-footer is on the <footer> element, we can use that class to prequalify the <small> element with CSS. We’ll want to select and float the <small> element to the left. Let’s not forget to create a new section within our main.css file for these primary footer styles.

```css
/*
  ========================================
  Primary footer
  ========================================
*/

.primary-footer small {
  float: left;
}
```
To review, here we are selecting the <small> element, which must reside within an element with the class attribute value of primary-footer, such as our <footer> element, for example.

7. Lastly, let’s put some padding on the top and bottom of the <footer> element to help separate it a little more from the rest of the page. We can do this directly by using the primary-footer class with a class selector.

``` css
.primary-footer {
  padding-bottom: 44px;
  padding-top: 44px;
}
```

With all of these changes to the <header> and <footer> elements, we have to be sure to make them on every page, not just the index.html page.
[!Fig05.01.png]
Fig 5
With a few floats, the <header> and <footer> elements on our Styles Conference home page are coming together

## Inline-Block 定位
除了使用float来定位外，我们还可以使用display属性的inline-block值来定位。

它主要的对页面铺设或HTML元素行内排放很有帮助。is primarily helpful for laying out pages or for placing elements next to one another within a line.

回顾一下，inline-block值的作用是让行内元素接收Box模型的height, width, padding, border和margin属性。使用inline-block元素让我们可以尽情使用Box模型的优势却不用担心清除任何浮动元素。

### Inline-Block实践
和之前一样，假设我们有三列元素，还保存HTML原样
```html
<header>...</header>
<section>...</section>
<section>...</section>
<section>...</section>
<footer>...</footer>
```

现在我们不让<section>元素浮动而是将其display值修改为inline-block，margin和width属性值也不改，CSS看起来如下：
```css
section {
  display: inline-block;
  margin: 0 1.5%;
  width: 30%;
}
```

貌似没有达成我们想要的效果，最后一个<section>元素换到下一行了，需要记住的是，由于Inline-block元素是在同一行显示的，它们之间本来就有间隔，我们再添加了width值和margin之后，总值就过大了，最终导致了最后一个<section>元素换行。为了使其位于一行，我们必须移除<section>元素之间的间隔。

### 移除两个Inline-Block元素之间的间隔
有好几种方式来移除inline-block元素之间的间隔，其中一些比较复杂。我们集中使用其中两种比较简单的方式，都是通过修改HTML来实现。

第一种方案是将新的<section>元素的开口标签放在上一个<section>元素的闭口标签之后，而不是我们之前的每次声明一个<section>元素都另起一行。现在我们的代码如下：
```html
<header>...</header>
<section>
  ...
</section><section>
  ...
</section><section>
  ...
</section>
<footer>...</footer>
```

这个方案确保了inline-block元素之间的间隔不存在，相应的，在页面渲染时两个元素之间的空白也消失了。

另外一种方法是在<section>元素之间使用HTML注释，来保证它们之间没有间隔（也就是将默认的间隔注释掉了），代码如下：
```html
<header>...</header>
<section>
  ...
</section><!--
--><section>
  ...
</section><!--
--><section>
  ...
 </section>
 <footer>...</footer>
```
以上两种方法都不是完美的，但都能用，没有优劣，你自己挑。



## 创建可复用的布局
建网站的时候，使用可以导出复用模块化的样式总是最好的，而且可复用的布局代码的优先级更高。

布局可以通过浮动或Inline-block元素来创建，哪种更好以及为什么呢？

到底使用浮动元素还是Inline-block元素来布局页面结构是个开放的讨论话题。我的方法是使用inline-block元素来创建页面的网格或布局，当我想让内容围绕指定的元素（正如最初的为了围绕图片的目的）时我会用float，一般来说，我认为inline-block元素更加简单易用。

也就是说，没有绝对的答案，哪个对你来说简单就用哪个。

目前CSS有新的方式来用于布局，基于flex-和grid-的属性，它们将会产生最好的页面布局途径。需要时刻关注这些方法什么时候推广使用。



## 实践
With a solid understanding of reusable layouts, the time has come to implement one in our Styles Conference website.
1. For the Styles Conference website, we’ll create a three-column reusable layout using inline-block elements. We’ll do so in a way that allows us to have three columns of equal width or two columns with the total width split between them, two-thirds in one and one-third in the other.

To begin, we’ll create classes that define the width of these columns. The two classes we’ll create are col-1-3, for one-third, and col-2-3, for two-thirds. Within the grid section of our main.css file, let’s go ahead and define these classes and their corresponding widths.

```css
.col-1-3 {
  width: 33.33%;
}
.col-2-3 {
  width: 66.66%;
}
```

2. We’ll want both of the columns to be displayed as inline-block elements. We’ll need to make sure that their vertical alignment is set to the top of each column, too.

Let’s create two new selectors that will share the display and vertical-alignment property styles.

```css
.col-1-3,
.col-2-3 {
  display: inline-block;
  vertical-align: top;
}
```
Looking at the CSS again, we’ve created two class selectors, col-1-3 and col-2-3, that are separated with a comma. The comma at the end of the first selector signifies that another selector is to follow. The second selector is followed by the opening curly bracket, {, which signifies that style declarations are to follow. By comma-separating the selectors, we can bind the same styles to multiple selectors at one time.

3. We’ll want to put some space in between each of the columns to help break up the content. We can accomplish this by putting horizontal padding on each of the columns.

This works well; however, when two columns are sitting next to one another, the width of the space between them will be double that of the space from the outside columns to the edge of the row. To balance this we’ll place all of our columns within a grid and add the same padding from our columns to that grid.

Let’s use a class name of grid to identify our grid, and then let’s identify the same horizontal padding for our grid, col-1-3, and col-2-3 classes. With commas separating our selectors again, our CSS looks like this:

```css
.grid,
.col-1-3,
.col-2-3 {
  padding-left: 15px;
  padding-right: 15px;
}
```

4. When we’re setting up the horizontal padding, we’ll need to be careful. Remember, in the last lesson we created a container element, known by the class of container, to center all of our content on a page within a 960-pixel-wide element. Currently if we were to put an element with the class of grid inside an element with the class of container, their horizontal paddings would add to one another, and our columns would not appear proportionate to the width of the rest of the page.

We don’t want this to happen, so instead, we’ll have to share some of the styles from the container rule set with the grid rule set. Specifically, we’ll need to share the width property and values (to make sure our page stays fixed at 960 pixels wide) and the margin property and values (to center any element with the class of grid on the page).

We’ll accomplish this by breaking up the old container rule set into the following:

``` css
.container,
.grid {
  margin: 0 auto;
  width: 960px;
}
.container {
  padding-left: 30px;
  padding-right: 30px;
}
```
Now any element with the class of container or grid will be 960 pixels wide and centered on the page. Additionally, we’ve preserved the existing horizontal padding for any element with the class of container by moving it into a new, separate rule set.

5. All right—all of the heavy lifting needed to get our reusable grid styles into place is finished. Now it’s time to work in our HTML and to see how these classes perform.

We’ll begin with the teasers on the home page, within our index.html file, aligning them into three columns. Currently, the teasers are wrapped in a <section> element with the class of container. We’ll want to change that class from container to grid so that we can begin placing columns within it.

```html
<section class="grid">
  ...
</section>
```

6. Next, we’ll want to add a class of col-1-3 to each of the <section> elements within the <section> element with the class of grid.

```html
<section class="grid">

  <section class="col-1-3">
    ...
  </section>

  <section class="col-1-3">
    ...
  </section>
  
  <section class="col-1-3">
    ...
  </section>

</section>
```
7.And lastly, because each of our columns is an inline-block element, we’ll want to make sure we remove the empty white space between them. We’ll use comments to do this, and we’ll add a little bit of documentation noting each upcoming section while we’re at it to better organize our code.

```html
<section class="grid">
  
  <!-- Speakers -->
  
  <section class="col-1-3">
    ...
  </section><!--
  
  Schedule
  
  --><section class="col-1-3">
    ...
  </section><!--
  
  Venue
  
  --><section class="col-1-3">
    ...
  </section>

</section>
```

To review, on line 3 we leave a comment identifying the “Speakers” section to follow. At the end of line 7, we open a comment immediately after the closing </section> tag. Within that comment, on line 9 we identify the “Schedule” section to come. We then close the comment at the beginning of line 11, just before the opening <section> tag. This same comment structure reappears on lines 13 through 17 between the two <section> elements, right before the “Venue” section. In all, we’ve commented out any potential white space between the columns while also using those comments to identify our sections.



需要翻译We now have a reusable three-column grid that supports multiple arrangements, using both one-third- and two-thirds-width columns. Our home page now has three columns, breaking up all the different teasers.

[!Fig.05.02.png]
Fig 5
Our Styles Conference home page now includes a three-column layout



### Demo和源码
* [Demo](http://learn.shayhowe.com/practice/positioning-content/index.html)
* [源码](http://learn.shayhowe.com/practice/positioning-content.zip)

## Uniquely Positioning Elements
时不时的，我们想[精确定位](http://alistapart.com/article/css-positioning-101)一个元素，但float和inline-block元素都不好弄。浮动元素会将一个元素从原来的页面流布局中移掉，会产生不是我们预期的结构，例如周围的HTML元素围绕浮动元素。inline-block元素，除非我们创建列的时候可以勉强让元素处于差不多的位置。 对于需要准确定位的条件，我们可以使用position 属性。

position属性标识了一个元素是如何在页面上定位的，以及它是否会出现在一个文档的流布局中。这需要配合Box的偏移属性 top, right, bottom, left来使用，这样可以通过控制元素在各个方向的值来精确的定位。

默认情况下，每个元素的position的属性值都是static， 这表示该元素会以正常的流布局形式出现在文档中，且它不接收任何box偏移属性。该static值可以被relative或absolute值覆盖，接下来我们就讨论该内容。

### Relative 定位
当position属性值为relative时，它允许元素继续以正常的流出现在页面中。按照预期给该元素刘熏爱空白不让其他元素flow around它。 同时也可以通过修改box偏移属性来显示位置。查看如下的HTML和CSS
```html
<div>...</div>
<div class="offset">...</div>
<div>...</div>
```

```css
div {
  height: 100px;
  width: 100px;
}
.offset {
  left: 20px;
  position: relative;
  top: 20px;
}
```
这里的第二个div元素其class属性值为offset，将其position值设置为relative，同时修改了它的偏移属性left 和 top，这会占用原来的位置使其他元素不能占用（就像占座儿），然后偏移属性设置让其按照其初始位置距左20像素，距顶20像素。

对于relative定位需要记住的就是它的偏移量是相对于它的初始位置的。同时，当我们通过偏移量来定位元素时，该元素会覆盖在其他元素的上面，而不会导致其他元素的位置变动。


### Absolute 定位
和相对定位不同的是，绝对定位的元素不会出现在页面的流布局中，也就是不会在原页面流布局中占据任何位置。Additionally, absolutely positioned elements are moved in relation to their closest relatively positioned parent element. Should a relatively positioned parent element not exist, the absolutely positioned element will be positioned in relation to the <body> element.此外，绝对定位的元素会根据其最近的相对定位父对象来移动。如果它的父对象不存在，则会以<body>元素作为参考的父对象。看看具体怎么操作：

```html
<section>
  <div class="offset">...</div>
</section>
```

```css
section {
  position: relative;
}
div {
  position: absolute;
  right: 20px;
  top: 20px;
}
```

该示例中<section>元素是相对定位的，但没有设置任何偏移量，因此它的位置不会移动。class属性值为offset的元素的position属性值为absolute。由于<section>元素是<div>元素最近的相对定位的元素，那么<div>元素会以<section>元素为参考来定位。

结果就是，<div>元素以<section>元素位置为参考，距离右侧20px，距离顶部20px，且由于其不会出现在页面的流布局中，所以也不会在默认的页面中占据位置。
通常情况下，不需要通过position属性和其box偏移值来定位，但在一些特殊情况下它们会很有用。

## 总结
学习如何定位是精通HTML和CSS的了不起的一步，结合Box模型，我们已经走在成为前端工程师的陆上了。

回顾一下本课都讲了什么内容：
* 浮动元素是什么以及如何使用它们来定位
* 如何清除或包含浮动元素
* 如何移除inline-block元素之间的空白间距
* 如何通过相对定位和绝对定位来单独定位内容

在每一节可我们都积累了新的技能，继续加油，下一节可，排版！

## 资源与链接
* [CSS Float Theory](http://www.smashingmagazine.com/2007/05/01/css-float-theory-things-you-should-know/) via Smashing Magazine 
* [CSS Positioning 101](http://alistapart.com/article/css-positioning-101) via A List Apart

## 课程链接
* [课程04：Box模型](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_04_Opening_the_Box_Model.md)
* [课程06：排版](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_06_Working_with_Typography.md)