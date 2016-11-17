title: 课程06：排版
date: 2016-04-08 00:00:07
tags: [html,css]
categories: HTML And CSS
---

[网页排版](http://webtypography.net/)的越来越广，有很多原因导致的，其中广为认可的是我们可以在网页中嵌入特定的字体。

之前的网页开发中，只能使用限定的字体，也就是那些默认安装在本地的字体。如果在本地安装了，在网页上就可以渲染，如果没安装就不行。现在我们可以在网页中嵌入任何我们想要的字体了。

尽管我们可以使用任何字体，但我们还需要掌握排版的基本原则。在本节课内容我们将深入讨论该内容。

<!--more-->

> Typeface 与 Font 中文没有这样的问题
> 字体与字体文件的问题。The terms “typeface” and “font” are often interchanged, causing confusion. Here is a breakdown of exactly what each term means.
> A typeface is what we see. It is the artistic impression of how text looks, feels, and reads.
>
> A font is a file that contains a typeface. Using a font on a computer allows the computer to access the typeface.
>
> One way to help clarify the difference between a typeface and a font is to compare them to a song and an MP3. A typeface is very similar to a song in that it is a work of art. It is created by an artist or artists and is open to public interpretation. A font, on the other hand, is very similar to an MP3 in that it is not the artistic impression itself, but only a method of delivering the artistic value.


## 设置文本颜色
---
通常情况下当我设计网站时第一个决策就是选用什么字体和颜色，无论是字体的大小、字重，颜色、字体等等，对网页看起来的效果和可读性都有很大的影响。

设置文本只需要一个color 属性，它可以接收一个颜色值，不过可以是多个形式的，这个我们在 “了解CSS”那节课中讨论过 包括关键字颜色，十六进制颜色，RGB，RGBa，HSL，HSLa值。其中十六进制颜色是使用最广泛的。

如下代码展示了如何将`<html>`标签中的所有字体修改颜色的：
```css
html {
  color: #555;
}
```


## 设置字体属性
---

CSS 提供了大量的属性用来编辑网页文本的外观和感觉的属性，这些属性分为两类：基于字体属性和基于文本属性。它们中的大部分属性都有`font-*` 或 `text-*` 前缀， 我们先讨论基于字体的属性。

### 字体系列
font-family属性用于决定使用哪个字体文件，以及在默认指定的字体缺失的情况下的备用或替换字体是什么。 font-family属性值包括多个字体名称，它们之间通过 `,` 分隔。

第一个声明的字体，也就是最左边的字体是默认字体。如果该字体找不到，则查找下一个，以此类推。

字体名字由两个或多个词组成时需要用`""` 括起来，此外，最后一个字体必须为使用系统默认字体的关键字值，一般来说是`sans-serif` 或 `serif`。

示例：
```css
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
```

在上面的案例中，"Helvetica Neue"是希望使用的字体。如果该字体无法获取或设备上没有安装改字体，则会查找下一个字体Helvetica，以此类推。

### 字体尺寸

font-size是用来设置字体尺寸的属性，它接收长度值，也就是像素，`em`，百分比，点数以及font-size关键字。
以下代码将`body`元素中的字体设置为14像素：
```css
body {
  font-size: 14px;
}
```

### 字体样式
设置字体是否倾斜，我们使用font-style属性，它接收4个关键字值：`normal` `italic` `oblique` `inherit`。 这四个值中，最常用的是`italic`(设置为斜体) 和`normal`(字体设置为正常)

如下的案例中将所有class属性值为special的元素的字体修改为斜体。

```css
.special {
  font-style: italic;
}
```



### 字体变化（Font Variant）
这种情况不常见，但偶尔文本需要全部设置为小写，这样的情况下我们需要用到font-variant属性，该属性可以接收三种值：`normal` `small-caps`和 `inherit` 最常用的是`normal` 和 `small-caps`，也就是用于将字体改为小写或正常。

如下代码中将所有class属性值为firm的HTML元素的字体改为小写。
```css
.firm {
  font-variant: small-caps;
}
```

### 字重
某些情况下，我们需要对字体进行加粗或修改为特定的字重。这种情况下我们使用font-weight属性。font-weight属性可以接收关键字值或数字值。

关键字值包括`normal` `bold` `bolder` `lighter` 和`inherit`， 这些值中常用的是`bold` 和 `normal` 也就是用于加粗或正常。 对于用`bolder` 还是 `lighter` ，推荐使用数值来进行更加精确的控制。
以下案例中将所有class属性值为daring的HTML元素的字重设置为加粗：
```css
.daring {
  font-weight: bold;
}
```

数值 100, 200, 300, 400, 500, 600, 700, 800, 900 可以指定字体的不同权重，从最细的权重100开始，到最粗的权重900结束。 作为参考，关键值 `normal` 和 400权重对应， `bold` 和 700对应，因此任何低于400的字体都比较细，超过700的会比较粗。

如下的案例中将所有class属性为daring的HTML元素的字重改为 600，看起来会没有之前使用的`bold`字粗。

> 字体权重
> 在使用数值设置字重之前，我们需要检测该字体是否支持我们指定的字重，使用指定字体不支持的权重会使该字体的权重设置为离数值最近的默认值。
> 例如，字体 `Times New Roman` 只支持两种权重: `normal` 或 400 ， `bold` 或700， 假设我们将其权重修改为900的时候，则会回到最近的权重，700.


### 行高
行高，是指文本中两行之间的距离，它可以通过`line-height` 来定义， `line-height` 属性接收我们在第3课中提到的任何长度值。

易读性最好的行高设置是设置`font-size`属性值的 1.5倍。 这可以简单的通过设置`line-height` 值为`150%`或 `1.5` 来实现。 然而，如果要按照网格的基准线来调整的话，我们可以通过像素更加精确的控制。

如下的案例中，我们将`body` 元素中的所有行高修改为 22 像素。

```css
body {
  line-height: 22px;
}
```

行高也可以用于将HTML元素中一行文本实现垂直居中，如下的代码就可以实现：
```css
.btn {
  height: 22px;
  line-height: 22px;
}
```
这样的应用往往出现在如按钮，弹出信息，或其他单行文本块中。



### 字体属性简写形式
以上所有的基于字体的属性都可以通过`font`属性和[简写形式的值](http://www.impressivewebs.com/css-font-shorthand-property-cheat-sheet/)来实现。 `font` 属性可以接收多个基于 `font`属性的值。这些值的顺序是：
`font-style` `font-variant` `font-weight` `font-size` `line-height` 和 `font-family`

简写形式的值从左到右排开，除了`font-family` 属性外不需要使用 `,` 分隔， 在 `font-size` 和 `line-height` 之间需要使用 `/`

在使用简写形式时候，除了`font-size` 和 `font-family` 属性外的所有属性值都是可选项，也就是说，如果想，我们只要包含`font-size` 和 `font-family` 这两个属性值就可以了。

```css
html {
  font: italic small-caps bold 14px/22px "Helvetica Neue", Helvetica, Arial, sans-serif;
}
```

### 字体全部属性用法示例
我们来看看使用了所有基于字体的样式。以下的HTML和CSS展示了设置文本的不同方式。
```html
<h2><a href="#">I Am a Builder</a></h2>

<p class="byline">Posted by Shay Howe</p>

<p>Every day I see designers and developers working alongside one another. They work intelligently in pursuit of business objectives. They work diligently making exceptional products. They solve real problems and take pride in their work. They are builders. <a href="#">Continue&#8230;</a></p>
```

```css
h2,
p {
  color: #555;
  font: 13px/20px "Helvetica Neue", Helvetica, Arial, sans-serif;
}
a {
  color: #0087cc;
}
a:hover {
  color: #ff7b29;
}
h2 {
  font-size: 22px;
  font-weight: bold;
  margin-bottom: 6px;
}
.byline {
  color: #9799a7;
  font-family: Georgia, Times, "Times New Roman", serif;
  font-style: italic;
  margin-bottom: 18px;
}
```

> CSS 伪类
> 上面的示例中使用了我们之前没有看过的:hover CSS伪类， 伪类是用于加在宣州后面用来设置HTML元素在特定状态下的样式。
> `:hover` 伪类设置了当用户将鼠标浮动在该元素上的样式。


## 实践
---
Diving back into our Styles Conference website, let’s start adding some font-based properties.
1. We’ll begin by updating the font on all of our text. To do this, we’ll apply styles to our <body> element. We’ll start with a color, and we’ll also add in font-weight, font-size, line-height, and font-family values by way of the font property and shorthand values.

In an attempt to keep our main.css file as organized as possible, let’s create a new section for these custom styles, placing it just below our reset and above our grid styles.

We need to add the following:

```css
/*
  ========================================
  Custom styles
  ========================================
*/
body {
  color: #888;
  font: 300 16px/22px "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
}
```

2. In Lesson 4, “Opening the Box Model,” we began adding some typographic styles, specifically adding a bottom margin to a few different levels of headings and paragraphs. Within the same section of the main.css file, let’s add a color to the level-one through level-four headings.

```css
h1, h2, h3, h4 {
  color: #648880;
}
```
While we’re at it, let’s also add in font sizes for these different heading levels. Our <h1> and <h2> elements will use fairly large font-size values; consequently, we’ll also want to increase their line-height values to keep the text within these elements legible. For reference, we’ll make their line-height values 44 pixels, double the value of the base line-height set within the <body> element rule set.

``` css
h1 {
  font-size: 36px;
  line-height: 44px;
}
h2 {
  font-size: 24px;
  line-height: 44px;
}
h3 {
  font-size: 21px;
}
h4 {
  font-size: 18px;
}
```

3. Our <h5> elements are going to be a little more unique than the rest of our headings. Accordingly, we’re going to change their styles a bit.

We’ll use a different color property value and a slightly smaller font-size for these elements, and we’re going to change the font-weight to 400, or normal.

By default, browsers render headings with a font-weight of bold. Our headings, however, are currently all set to a font-weight of 300. Our reset at the top of our main.css file changed the font-weight to normal, and then our font-weight of 300 within the <body> element rule set changed all headings to a font-weight of 300.

The font-weight of 400 on the <h5> element will actually make it slightly thicker than the rest of our other headings and text.

```css
h5 {
  color: #a9b2b9;
  font-size: 14px;
  font-weight: 400;
}
```

4. Our reset at the beginning of our style sheet also reset the browser default styles for the <strong>, <cite>, and <em> elements, which we’ll want to add back in. For our <strong> elements we’ll want to set a font-weight of 400, which actually equates to normal, not bold, as the typeface we’re using is thicker than most typefaces. Then, for our <cite> and <em> elements we’ll want to set a font-style of italic.
```css
strong {
  font-weight: 400;
}
cite, em {
  font-style: italic;
}
```
5. We’re on a roll, so let’s keep going by adding some styles to our anchor elements. Currently they are the browser default blue. Let’s make them the same color as our <h1> through <h4> heading elements. Additionally, let’s use the :hover pseudo-class to change the color to a light gray when a user hovers over an anchor.

```css
/*
  ========================================
  Links
  ========================================
*/

a:hover {
  color: #a9b2b9;
}
a {
  color: #648880;
}
```

6. Now let’s take a look at our <header> element and update our styles there. We’ll begin updating our logo by adding the font-size and line-height properties within the logo rule set. Adding to the existing border-top, float, and padding properties, the new rule set should look like this:

```css
.logo {
  border-top: 4px solid #648880;
  float: left;
  font-size: 48px;
  line-height: 44px;
  padding: 40px 0 22px 0;
}
```

7. Because we’ve bumped up the size of the logo quite a bit, let’s add a margin to the <h3> element within the <header> element to balance it. We’ll do so by placing a class attribute value of tagline on the <h3> element and then using that class within our CSS to apply the proper margins.

Let’s not forget that the changes to the <h3> element need to happen on every page.

`HTML`
```html
<h3 class="tagline">August 24&ndash;26th &mdash; Chicago, IL</h3>
```


`CSS`
```css
.tagline {
  margin: 66px 0 22px 0;
}
```

8. After the <h3> element with the class attribute value of tagline comes the <nav> element. Let’s add a class attribute value of primary-nav to the <nav> element and add font-size and font-weight properties to make the navigation stand out against the rest of the header.

`HTML`
```html
<nav class="primary-nav">
  ...
</nav>
```

`CSS`

```css
.primary-nav {
  font-size: 14px;
  font-weight: 400;
}
```

9. With the <header> element in slightly better shape, let’s also take a look at our <footer> element. Using the primary-footer class, let’s change the color and font-size for all the text within the <footer> element. Additionally, let’s bump up the font-weight of the <small> element to 400.

Including the existing styles, the styles for our primary footer section should look like this:

```css
.primary-footer {
  color: #648880;
  font-size: 14px;
  padding-bottom: 44px;
  padding-top: 44px;
}
.primary-footer small {
  float: left;
  font-weight: 400;
}
```

10. Let’s update our home page a bit, too. We’ll start with the hero section, increasing the overall line-height of the section to 44 pixels. We’ll also make the text within this section larger, increasing the <h2> element’s font-size to 36 pixels and the <p> element’s font-size to 24 pixels.

We can make all of these changes by using the existing hero class selector and creating new selectors for the <h2> and <p> elements. Our styles for the hero section will now break down in this way:

```css
.hero {
  line-height: 44px;
  padding: 22px 80px 66px 80px;
}
.hero h2 {
  font-size: 36px;
}
.hero p {
  font-size: 24px;
}
```

11. Lastly, we have one small issue to fix on our home page. Previously we gave all of our anchor elements a light gray color value when a user hovers over them. This works great, except for within the three teasers on our home page where the anchor element wraps both <h3> and <h5> elements. Because the <h3> and <h5> elements have their own color definition, they are not affected by the :hover pseudo-class styles from before.

Fortunately we can fix this, although it’s going to require a fairly complicated selector. We’ll begin by adding a class attribute value of teaser to all three columns on the home page. We’ll use this class as a qualifying selector shortly.

```html
<section class="grid">

  <!-- Speakers -->

  <section class="teaser col-1-3">
    <a href="speakers.html">
      <h5>Speakers</h5>
      <h3>World-Class Speakers</h3>
    </a>
    <p>Joining us from all around the world are over twenty fantastic speakers, here to share their stories.</p>
  </section>

  ...

</section>
```
With a qualifying class in place, we’re ready to do some CSS heavy lifting and create a fairly complex selector. We’ll begin our selector with the teaser class, as we only want to target elements within an element with the class of teaser. From there we want to apply styles to elements that reside within anchor elements that are being hovered over; thus we’ll add the a type selector along with the :hover pseudo-class. Lastly, we’ll add the h3 type selector to select the actual <h3> elements we wish to apply styles to.

Altogether, our selector and styles for these <h3> elements will look like this:

```css
.teaser a:hover h3 {
  color: #a9b2b9;
}
```
Whew, that was quite a bit. The good news is that our Styles Conference home page is starting to look really nice and is showing a bit of personality.

## 设置文本属性
---

了解如何设置字体类型，尺寸，样式，变形，字重，和行高这些属性才算了解了排版的一半内容。此外我们还需要如何对齐、修饰、缩进、变换文本以及设置文本间距。我们先从文本对齐方式开始。

### 文本对齐方式
在设计页面节奏与页面流的时候如何对齐文本特别重要。我们使用 `text-align`属性来完成，`text-align` 属性有5个值：`left`  `right` `center` `justify` `inherit`。 这些值简单直白。

如下代码将文本居中设置

```css
p {
  text-align: center;
}
```

对于`text-align` 属性不可以与 `float` 属性混淆。 `text-align` 属性值会使文本在HTML元素内左对齐或右对齐，但`float`属性值却会移动整个元素。


### 文本修饰
`text-decoration` 属性提供了几种方式来美化文本。它可以接收 `none` `underline` `overline` `line-though` 和 `inherit` 这样的关键字值。但最常使用的是`underline`，作为链接使用。

示例代码：
```css
.note {
  text-decoration: underline;
}
```

一个HTML元素可以设置多个 `text-decoration` 值，值与值之间通过空格分开。

### 缩进
`text-indent` 属性可以用来将HTML元素的首行文本进行缩进，和我们看到的印刷品一样。该属性接收任何长度值，包括像素，点数，百分比等等。 正值会向内缩进，负值会向外推进。
示例代码：

```css
p {
  text-indent: 20px;
}
```

### 阴影
`text-shadow`属性可以给文本添加单个或多个投影效果。该属性需要同时接收4个值，一一排列，前三个值是长度值，最后一个值是颜色。

在三个长度值中，第一个值决定了投影的水平偏移量。，第二个值决定了投影的垂直偏移量，第三个值决定了投影的模糊半径。第四个值，也就是投影的颜色，可以接收任何颜色值。

如下的案例中，会有30%透明，向右偏移3像素，向下偏移6像素，模糊2像素的阴影
```css
p {
  text-shadow: 3px 6px 2px rgba(0, 0, 0, .3);
}
```
使用负的长度值的时候，可以让投影向左和上方移动。

多个文本投影可以使用逗号分隔实现连续拼接，这样可以给文本添加多个投影。

> 盒子投影
> `text-shadow`属性让我们可以设置文本的投影， 而`box-shadow`属性可以让我们设置整个元素的投影
> 和`text-shadow` 一样的是，`box-shadow` 也接收 水平，垂直偏移量，模糊，颜色值。
> 此外 `box-shadow` 在颜色值之前还可以接收可选的长度值。如果值为正的，其会放大整个元素的阴影的尺寸，如果值为负的，则会缩小整个元素阴影的尺寸。
> 最后， `box-shadow` 属性在第一个位置可以包含一个可选值`inset`，用于设置阴影是向内投还是向外投？？？？Lastly, the box-shadow property may include an optional inset value at the beginning of the value to place the shadow inside an element as opposed to outside the element.


### 变换
和`font-variant`属性一样，我们有`text-transform`属性， 但`font-variant`属性是查找字体的变换，而`text-transform`属性会改变行内而不需要修改字体？？？ While the font-variant property looks for an alternate variant of a typeface, the text-transform property will change the text inline without the need for an alternate typeface.  `text-transform` 属性接收5种值：`none`, `capitialize`, `uppercase`, `lowercase`和`inherit`。

`capitialize`值会将每个词的首字母大写，`uppercase`值会将每个字母都大写，`lowercase` 会将所有字母都小写，`none` 会将所有这些值复位。

下面的CSS会将所有的`<p>`元素的文本改为大写字母：
```css
p {
  text-transform: uppercase;
}
```

### 字母间距
使用`letter-spacing`属性，我们可以调整（跟踪）页面内字母之间的间距。正的值越大，字母之间的间距就会越大，如果是负值，值越小，字母会越靠近，如果设置为`none`值，字母之间的间距会复位。
给`letter-spacing`赋予相对长度值可以确保我们在调节`font-size`值的时候，字母之间的间距保持一致。理想的情况下是这样的，但我们需要随时检查是否真的奏效。

如下的示例代码所有的`<p>` 元素中的字母会比原来靠近`.5em`.

```css
p {
  letter-spacing: -.5em;
}
```

### 词间距
和`letter-spacing`属性类似， 我们还可以通过`word-spacing` 来调整单词之间的间距, `word-spacing` 接收和`letter-spacing`属性一样的长度或关键字值。

示例代码：
```css
p {
  word-spacing: .25em;
}
```

### 所有文本属性示例
接着上面的案例，我们添加一些基于文本的属性。
```html
<h2><a href="#">I Am a Builder</a></h2>

<p class="byline">Posted by Shay Howe</p>

<p class="intro">Every day I see designers and developers working alongside one another. They work intelligently in pursuit of business objectives. They work diligently making exceptional products. They solve real problems and take pride in their work. They are builders. <a href="#">Continue&#8230;</a></p>

```

```css
h2,
p {
  color: #555;
  font: 13px/20px "Helvetica Neue", Helvetica, Arial, sans-serif;
}
a {
  color: #0087cc;
}
a:hover {
  color: #ff7b29;
}
h2 {
  font-size: 22px;
  font-weight: bold;
  letter-spacing: -.02em;
  margin-bottom: 6px;
}
h2 a {
  text-decoration: none;
  text-shadow: 2px 2px 1px rgba(0, 0, 0, .2);
}
.byline {
  color: #9799a7;
  font-family: Georgia, Times, "Times New Roman", serif;
  font-style: italic;
  margin-bottom: 18px;
}
.intro {
  text-indent: 15px;
}
.intro a {
  font-size: 11px;
  font-weight: bold;
  text-decoration: underline;
  text-transform: uppercase;
}
```


## 实践
---
With text-based properties under our belts, let’s jump back into our Styles Conference website and put them to work.

1. Currently every link on the page is underlined, which is the default style for anchor elements. This style is a little overbearing at times, though, so we’re going to change it up a bit.

Adding to our links section within our main.css file, we’ll begin by removing the underline from all anchor elements by way of the text-decoration property. Next, we’ll select all anchor elements that appear within a paragraph element and give them a bottom border.

We could use the text-decoration property instead of the border-bottom property to underline all the links within each paragraph; however, by using the border-bottom property we have more control over the underline’s appearance. Here, for example, the underline will be a different color than the text itself.

Our links section, which includes our previous hover styles, should look like this:

```css
a {
  color: #648880;
  text-decoration: none;
}
a:hover {
  color: #a9b2b9;
}
p a {
  border-bottom: 1px solid #dfe2e5;
}
```

2. Going back to our <h5> elements from before, which have slightly different styles than the rest of the headings, let’s make them all uppercase using the text-transform property. Our new <h5> element styles should look like this:

```css
h5 {
  color: #a9b2b9;
  font-size: 14px;
  font-weight: 400;
  text-transform: uppercase;
}
```

3. Let’s revisit our <header> element to apply additional styles to our navigation menu (to which we previously added the primary-nav class attribute value). After the existing font-size and font-weight properties, let’s add some slight letter-spacing and change our text to all uppercase via the text-transform property.

Our styles for the <nav> element with the primary-nav class attribute value should now look like this:
```css
.primary-nav {
  font-size: 14px;
  font-weight: 400;
  letter-spacing: .5px;
  text-transform: uppercase;
}
```

4. Previously, we floated our logo to the left within the <header> element. Now our tagline sits directly to the right of the logo; however, we’d like it to appear all the way to the right of the <header> element, flush right.

We need to add the text-align property with a value of right to the <h3> element with the class attribute value of tagline to get the tagline to sit all the way to the right.

When added to the existing margin property, our new styles for the <h3> element with the class attribute value of tagline will look like this:

```css
.tagline {
  margin: 66px 0 22px 0;
  text-align: right;
}
```

5. We’d also like our navigation menus, both in the <header> and <footer> elements, to sit flush right. Because both the <header> and <footer> elements have child elements that are floated to the left, we can use the same approach as we did with our tagline.

The floated elements within the <header> and <footer> elements are taken out of the normal flow of the page, and this causes other elements to wrap around them. In this specific case, our navigation menus are the elements wrapping around the floated elements.

Because we’ll be sharing the same styles across both navigation menus, we’ll give them each the class of nav. Our <header> element will now look like this:

```html
<header class="container group">

  <h1 class="logo">...</h1>

  <h3 class="tagline">...</h3>

  <nav class="nav primary-nav">
    ...
  </nav>

</header>
```

And our <footer> element will now look like this:

```html
<footer class="primary-footer container group">

  <small>...</small>

  <nav class="nav">
    ...
  </nav>

</footer>
```

Let’s not forget, changes to our <header> and <footer> elements need to be made on every page.

6. With the nav class in place on both navigation menus, let’s create a new section within our main.css file to add shared navigation styles. We’ll begin by adding the text-align property with a value of right to a nav class rule set. We’ll expand these styles later on, but this will serve as a great foundation.

```css
/*
  ========================================
  Navigation
  ========================================
*/

.nav {
  text-align: right;
}
```

7. While we’re adding the text-align property to a few different elements, let’s also add the text-align property with a value of center to our hero class selector rule set. For reference, these styles, including our existing line-height and padding properties, are located within the home page section of our main.css file.

```css
.hero {
  line-height: 44px;
  padding: 22px 80px 66px 80px;
  text-align: center;
}
```
Our Styles Conference now has some serious style. (Bad joke, sorry.) Seriously, though, all of our styles are coming along quite well, and our website is progressing.

## 使用Web-Safe字体
---
每台电脑、平板、智能手机或其他可使用浏览器的设备都默认安装了几种字体。正是由于它们安装到了这些设备中，在设计网页的时候，我们可以放心的使用这些字体，而不用担心它们不可以正常渲染，所以这些字体也称为 网站安全字体，不过只有少量这样的字体，列表如下：

* `Arial`
* `Courier New, Courier`
* `Garamond`
* `Georgia`
* `Lucida Sans, Lucida Grande, Lucida`
* `Palatino `
* `Linotype`
* `Tahoma`
* `Times New Roman, Times`
* `Trebuchet`
* `Verdana`

## 嵌入Web字体
---
我们也可以上传字体到服务器，然后CSS中通过`@font-face`来加载字体。它让在线排版成为了可能。

嵌入字体到网站中的步骤如下，首先用`@font-face`通过`font-family`来定义字体的名称，同时通过`src`定义字体源，然后我们就可以通过`font-family`来使用我们导入的字体了。
```css
@font-face {
  font-family: "Lobster";
  src: local("Lobster"), url("lobster.woff") format("woff");
}
body {
  font-family: "Lobster", "Comic Sans", cursive;
}
```

在网站中可以嵌入字体，不代表我们有权限可以这么做，字体是艺术作品，当我们上传到服务器的时候，其他人可以轻易的窃取，所以是否可以使用关键得看授权。

幸运的是，在网站中嵌入字体的方式开始被人们接收，一些公司开始开发一些方式让字体可以在网站上使用。包括[Typekit](https://typekit.com/) [Fontdeck](http://fontdeck.com/) work off a subscription model for licensing fonts, 一些其他的如[Google Fonts](https://www.google.com/fonts) 则是免费的，在上传字体之前，请确保我们有权限这么做。



## 实践
---
To add a little character to our Styles Conference website, let’s try using a Google Font on our website.

1. Let’s head over to the Google Fonts website and search for the font we’d like to use: Lato. Once we’ve found it, let’s proceed with adding it to our collection and following the steps on their website to use the font.

When the time comes to choose which font weights we’d like to use, let’s make sure to select 300 and 400, as we’ve already been using those within our CSS. Let’s also add 100 to the collection for another variation, too.

Google will give us an additional <link> element to include in the <head> element of all of our pages. We’ll place this new <link> element directly below our existing <link> element. The new element will include the proper style sheet reference to Google, which will take care of including a new CSS file with the proper @font-face at-rule necessary for us to use the Lato font.

With the addition of the new <link> element, our <head> element will look like this:

``` html
<head>
  <meta charset="utf-8">
  <title>Styles Conference</title>
  <link rel="stylesheet" href="assets/stylesheets/main.css">
  <link rel="stylesheet"
  href="http://fonts.googleapis.com/css?family=Lato:100,300,400">
</head>
```

2. Once we have added the new <link> element to all of our pages, we are ready to begin using the Lato font. We’ll do so by adding it to our primary font stack within the font property inside our <body> element styles.

Let’s add Lato to the beginning of our font stack to make it "Lato", "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif.

Although Lato is a single word, because it is an embedded web font we’ll want to surround it with quotation marks within any CSS reference. Our new <body> element styles will look like this:

```css
body {
  color: #888;
  font: 300 16px/22px "Lato", "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
}
```

3. Lato should now be up and running, visible in all of our text across the Styles Conference website. Let’s take a closer look at our logo and update it a bit.

Within our logo class selector rule set, we’ll begin by adding the font-weight property with a value of 100 to make the text fairly thin. We’ll also use the text-transform property with a value of uppercase to make all of the letters uppercase, as well as the letter-spacing property with a value of .5 pixels to add a tiny bit of space between each letter within the logo.

Altogether the styles for our logo will look like this:

```css
.logo {
  border-top: 4px solid #648880;
  float: left;
  font-size: 48px;
  font-weight: 100;
  letter-spacing: .5px;
  line-height: 44px;
  padding: 40px 0 22px 0;
  text-transform: uppercase;
}

```

4. Because we have a font-weight property value of 100 available, let’s also set the paragraph element within our hero section to that weight. We can use the existing selector to do so, and the new rule set will look like this:
```css
.hero p {
  font-size: 24px;
  font-weight: 100;
}
```

Our Styles Conference website has taken quite a few large steps this lesson, and the look and feel of our website is starting to really shine.

### Demo和源码
* [Demo](http://learn.shayhowe.com/practice/working-with-typography/index.html)
* [源码](http://learn.shayhowe.com/practice/working-with-typography.zip)


## Including Citations & Quotes
---
在线写作的时候会涉及到引述不同的信息来源或直接引用。所有的引述或引用在HTML中都可以通过`<cite>` 和 `<q>` `<blockquote>` 元素语义化。由于其外观和常规的文本看起来不一样，所以我们在排版这课讨论。

知道在什么情况下使用什么元素和属性，需要些练习，一般情况下：
* `<cite>`: 用于引用创意型工作，作者及资源
* `<q>`: 用于简短的，行内引用
* `<blockquote>`: 用于较大的外部引用

### 引用创意作品

HTML行内元素`<cite>`可以用于指定引用创意作品，该元素必须要么包含作品标题，作者名称或者作品URL链接。默认情况下浏览器会将`<cite>` 所包含的内容显示为斜体。
For additional reference, it helps to include a hyperlink to the original source of the citation when relevant.
以下是Walter Isaacson所著的《Steve Jobs》，被引用到<cite>元素，在该引用中同时包含了该书的超链接。

```html
<p>The book <cite><a href="http://www.amazon.com/Steve-Jobs-Walter-Isaacson/dp/1451648537">Steve Jobs</a></cite> is truly inspirational.</p>
```

### 对话和散文引用
在文本中引用对话或散文很常见。这种情况下应该使用`<q>`元素，`<q>`元素语义化使用就是引用对话或者散文，而不该用于其他目的。

默认情况下，浏览器会为我们插入恰当的引号，甚至会根据全局属性`lang`的属性值来修改引号格式。

下面是案例：
```html
<p>Steve Jobs once said, <q>One home run is much better than two doubles.</q></p>
```

### 对话和散文引文
An optional attribute to include on the <q> element is the cite attribute. The cite attribute acts as a citation reference to the quote in the form of a URL. This attribute doesn’t alter the appearance of the element; it simply adds value for screen readers and other devices. Because the attribute isn’t viewable within the browser, it’s also helpful to provide a hyperlink to this source next to the actual quotation.

`<q>`元素有个可选属性`cite` 该属性通过引用URL的形式作为引述参考，且不在HTML元素中显示。 其简单的为屏幕阅读器和其他设备添加了值。 由于该属性在浏览器中不可见，对于提供该源头

示例如下：

```html
<p><a href="http://www.businessweek.com/magazine/content/06_06/b3970001.htm">Steve Jobs</a> once said, <q cite="http://www.businessweek.com/magazine/content/06_06/b3970001.htm">One home run is much better than two doubles.</q></p>
```

### 外部引用
To quote a large block of text that comes from an external source and spans several lines, we’ll use the <blockquote> element. The <blockquote> is a block-level element that may have other block-level elements nested inside it, including headings and paragraphs.

对于来自外部源的引用我们将使用`<blockquote>` 来引用大块文本， `<blockquote>`元素是块元素，其可以嵌套其他块元素，比如标题或段落。

示例如下：
```html
<blockquote>
  <p>&#8220;In most people&#8217;s vocabularies, design is a veneer. It&#8217;s interior decorating. It&#8217;s the fabric of the curtains, of the sofa. But to me, nothing could be further from the meaning of design. Design is the fundamental soul of a human-made creation that ends up expressing itself in successive outer layers of the product.&#8221;</p>
</blockquote>
```

### 外部引述
Longer quotes used within the <blockquote> element will often include a citation. This citation may comprise both the cite attribute and the <cite> element.
`<blockquote>`元素中所使用的较长的引用常常会包括一个引述，该引述可能同时包含`cite`属性和`<cite>`元素。

The cite attribute can be included on the <blockquote> element—in the same way that it was used on the <q> element earlier—to provide a citation reference to the quote in the form of a URL. The <cite> element then can fall after the actual quote itself to specify the original source of the quote, if relevant.

The HTML here outlines an extended quote from Steve Jobs that originally appeared in Fortune magazine. The quotation is marked up using the <blockquote> element with a cite attribute to specify where the quote originally appeared. In the <blockquote> element, the <cite> element, along with an <a> element, provides an additional citation and reference for the quote that is visible to users.

```html
<blockquote cite="http://money.cnn.com/magazines/fortune/fortune_archive/2000/01/24/272277/index.htm">
  <p>&#8220;In most people&#8217;s vocabularies, design is a veneer. It&#8217;s interior decorating. It&#8217;s the fabric of the curtains, of the sofa. But to me, nothing could be further from the meaning of design. Design is the fundamental soul of a human-made creation that ends up expressing itself in successive outer layers of the product.&#8221;</p>
  <p><cite>&#8212; Steve Jobs in <a href="http://money.cnn.com/ magazines/fortune/fortune_archive/2000/01/24/272277/index.htm"> Fortune Magazine</a></cite></p>
</blockquote>
```


## 总结
---
当感觉到我们的内容开始传递某种情绪的时候，学习设置文本样式是不是很激动？！我们还可以试试内容的层次结构，使我们的网站更加清晰和易于理解。

快速回顾一下：
* 设置文本颜色
* 应用诸如`font-family` `font-size` `font-style` `font-weight`等字体属性
* 应用诸如`text-align` `text-decoration` `text-indent` `text-shadow` 等文本属性
* 安全web字体的历史及如何在网站中嵌入字体
* 如何正确引述和引用。

Sharpening up our text and dabbling（涉及） a bit with typography has brought our design along quite a way.
下节课我们将通过背景和渐变给我们的网站带来一点颜色。


## 资源和链接
---
* [The Elements of Typographic Style Applied to the Web](http://webtypography.net/) via Richard Rutter
* [CSS Font Shorthand Property Cheat Sheet](http://webtypography.net/) via Impressive Webs
* [Google Fonts](https://www.google.com/fonts)


## 课程链接
---
* [课程05：内容定位](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_05_Positioning_Content.md)
* [课程07：背景和渐变](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_07_Setting_Backgrounds_And_Gradients.md)
