title: 课程04：Box模型
date: 2016-04-08 00:00:09
tags: [html,css]
categories: HTML And CSS
---

到目前为止，我们已经熟悉了HTML和CSS了，我们知道它们看起来是什么样的，也能完成一些非常基础的内容。现在我们要更加深入的了解下这些HTML元素在网页上显示的原理是什么，以及怎么去控制它们的尺寸。


本课内容，我们将讨论Box模型是什么，以及如何在HTML和CSS中使用它。我们需要接触一些新的CSS属性，及使用在第三章提到的长度值等。现在开始吧！
<!--more-->

## HTML元素是如何显示的？
了解HTML元素是如何显示的会论Box模型。 在第二课中，我们提到了块元素和行内元素的区别，简单回顾一下：
块元素总会开启新的一行，和内容多少无关，其总会占据整个宽度，行内元素会占据和其内容相应的宽度，按照顺序排开。
块元素通常用于大块内容，例如标题和结构性元素。
行内元素通常用于小片段的内容，例如选择几个需要被加粗或倾斜的字符。

### 显示
那是什么决定了这些HTML元素以块元素、行内元素还是其他形式显示的呢？—— 由该元素的display属性决定的。 每个HTML元素都有默认的display属性值，但和其他的属性值一样，可以重写。display属性有好几个值，不过常见的是：block inline inline-block和none。

我们可以通过CSS选择某个HTML元素，然后修改其display属性值。例如将display修改为blcok，那么该HTML元素就会以块元素吸显示。

```css
p {
  display: block;
}
```

将display修改为inline，怎会使该元素以行内样式显示。

```css
p{
	display: inline;
}
```

inline-block属性值就比较有意思了，使用该属性值，会是该元素的行为像块元素，可以接收所有Box模型的属性（我们会在接下来讨论），但该元素却显示在行内，而不会新开启一行。

```css
p {
  display: inline-block;
}
```

> Inline-Block元素之间的间距
> One important distinction with inline-block elements is that they are not always touching, or displayed directly against one another. Usually a small space will exist between two inline-block elements. This space, though perhaps annoying, is normal. We’ll discuss why this space exists and how to remove it in the next lesson.

最后，如果我们将display的值设置为none的化，那么就完全看不到该元素，如同网页没有渲染一样，嵌入在该HTML元素内部的所有元素也会被隐藏。

```css
div {
  display: none;
}
```

由于display属性会影响如何渲染box模型，知道HTML元素是怎么显示的，以及如何修改其display属性值非常重要。当我们讨论Box模型的时候，我们也肯定会讨论这些影响，以及它们是如何影响HTML元素的显示的。

## 什么是Box模型？
根据[Box模型](http://css-tricks.com/the-css-box-model/)的概念,网页中的所有元素都是一个矩形的盒子，它们都有长宽，内边距、边框、外边距。

重要的事儿说三遍：网页中的所有元素都是矩形盒子！网页中的所有元素都是矩形盒子！网页中的所有元素都是矩形盒子！

[Fig04.01.png]
Fig 4 When we look at each element individually, we can see how they are all rectangular, regardless of their presented shapes

所有页面的所有HTML元素都符合Box模型这个概念非常重要！下面我们就仔细研究一下。

## 使用Box模型
每一个HTML元素都是一个矩形盒子，相应的有好几个属性决定了盒子的尺寸。Box关键是由HTML元素的宽高定义的。这些可以通过display属性决定。The core of the box is defined by the width and height of an element, which may be determined by the display property, by the contents of the element, or by specified width and height properties. padding and then border expand the dimensions of the box outward from the element’s width and height. Lastly, any margin we have specified will follow the border. 外边距和边框。。

Box模型对应CSS属性：width height padding border margin

下面看看这些属性是怎么用的：

```css
div {
  border: 6px solid #949599;
  height: 100px;
  margin: 20px;
  padding: 20px;
  width: 400px;
}
```

根据盒子模型，一个HTML元素的总宽度可以通过如下的公式来计算：
```
margin-right + border-right + padding-right + width + padding-left + border-left + margin-left
```

相应的，一个HTML元素的总高度可以通过如下的公司来计算：
```
margin-top + border-top + padding-top + height + padding-bottom + border-bottom + margin-bottom
```

[!Fig04.02]
Fig 4
The box model broken down, including a base height and width plus paddings, borders, and margins

通过上面的公式，我们可以算出来示例代码中的总宽高：
* 宽度： 492px = 20px + 6px + 20px + 400px + 20px + 6px + 20px
* 高度： 192px = 20px + 6px + 20px + 100px + 20px + 6px + 20px

毫无疑问，在HTML和CSS中Box模型是比较让人困惑的。我们设置了width属性值为400像素，但HTML元素的实际宽度确是492像素。默认情况下Box模型是递增的，因此确定一个Box的最终尺寸，我们需要算上四个边上的内边距，边框，外边距，其总宽度不仅仅包括width属性值，同时也包括了左右内边距、左右边框、左右外边距。

到目前为止，很多的属性值看起来没有什么用，那么我们就深入讨论下这些属性：width, height, padding, border, margin.

### Width & Height
每个元素都有默认的宽高，它们可能是0像素，但是浏览器默认都会用些尺寸渲染每个元素。取决于HTML元素是如何显示的，默认的width和height是足够的。 如果一个HTML元素是页面布局的关键元素，那么就需要我么指定恰当的width和height属性值。 在这种情况下, 非行内元素的属性值需要被指定。

#### Width
一个元素的默认宽度取决于其display的属性值。假如水平空间完全可以使用，那么块状元素的默认宽度是100%。 行内元素和inline-block元素会适应其内容的宽度。行内元素不能有固定的尺寸，因此，width和height属性只和非行内元素相关。The default width of an element depends on its display value. Block-level elements have a default width of 100%, consuming the entire horizontal space available. Inline and inline-block elements expand and contract horizontally to accommodate their content. Inline-level elements cannot have a fixed size, thus the width and height properties are only relevant to non-inline elements. 
设置一个非行内元素的宽度，使用width属性值：

```css
div {
  width: 400px;
}
```

#### Height
一个HTML元素的默认高度取决与其内容。HTML元素会在垂直方向随着内容变化而适应An element will expand and contract vertically as necessary to accommodate its content.  设置一个非行内元素的高度，可以使用height属性：

```css
div {
  height: 100px;
}
```

> 行内元素的尺寸
> Please keep in mind that inline-level elements will not accept the width and height properties or any values tied to them. Block and inline-block elements will, however, accept the width and height properties and their corresponding values.
> 时刻记住行内元素不接收width，height以及和这两个值相关的属性。块元素可以。

### Margin & Padding
根据不同的HTML元素，浏览器可能会给该元素赋予默认的外边距和内边距使其更加易读和清晰。在基于文本的HTML元素中常见。不同的浏览器默认的外边距和内边距可能不同。 在第一课中我们使用CSS重置，将所有的这些值都设置为0，这样做的好处是我们从零开始设置我们想要的值。

#### Margin
The margin property allows us to set the amount of space that surrounds an element. Margins for an element fall outside of any border and are completely transparent in color. margin属性让我们可以设置一个HTML元素周围的空间。 HTML元素的Margin部分是指边框以外的部分，并且它是完全透明的。Margin可以用于让HTML元素处于页面的特定位置，或者留白，查看如下代码示例：
```css
div {
  margin: 20px;
}
```
对于margin属性有个奇怪的地方就是垂直外边距，行内元素不接收这样的值，但块元素和inline-block元素接收这样的值。 One oddity with the margin property is that vertical margins, top and bottom, are not accepted by inline-level elements. These vertical margins are, however, accepted by block-level and inline-block elements.


#### Padding
padding属性和margin属性非常相似，只不过它是元素边框以内的部分。padding属性用于元素The padding property is used to provide spacing directly within an element. 以下是示例代码：
```css
div {
  padding: 20px;
}
```
和margin属性不同的是，padding属性在行内元素垂直方向上也有效。The padding property, unlike the margin property, works vertically on inline-level elements. This vertical padding may blend into the line above or below the given element, but it will be displayed.

> 行内元素的Margin和Padding
> 在通过margin和padding属性处理外边距和内边距时候，inline-level元素和 block/inline-block元素的影响不一样。
> inline-level元素中外边距只有左右有效果。内边距四边都有效果，只不过垂直内边距有可能会渗透到上方或下方的元素
> 
> block和inline-block元素的内边距和外边距都能正常使用。

### Margin & Padding的声明方式
在CSS中，一些特定的属性可以有好几种方式来表示其值。既可以使用完整写法，将多个值一个接着一个列举出来，当然，这里每一个值都对应了一个属性。当然也可以使用简洁的方法，一个属性对应多个值。We can use longhand, listing multiple properties and values one after the other, in which each value has its own property. Or we can use shorthand, listing multiple values with one property.  并非所有的属性都有简写方式，因此，我们必须确定我们使用正确的属性值结构。Not all properties have a shorthand alternative, so we must make sure we are using the correct property and value structure.

margin和padding属性既有完整格式也有简洁格式。当使用简写的margin属性给一个元素的4个边设置相同的值时，我们可以使用一个一个值：
```css
div {
  margin: 20px;
}
```

如果分开设置一个元素的上下部分和左右部分，就需要两个值，第一个值表示上下，第二个值表示左右。如下案例中，<div>元素的margin的上下部分值为10像素， 左右部分值为20像素
```css
div {
  margin: 10px 20px;
}
```

如果需要为4边都设置值，那么就按照顺时针，top, right, bottom, left来设置，如下案例中，我们将<div>元素的上部外边距设置为10px， 右外边距设置为20px，下外边距设为0px，左外边距设置为15px
```css
div {
  margin: 10px 20px 0 15px;
}
```

配合不同数量的值单独使用margin或padding称为简写方式。完整的写法是，我们可以为每一个边单独使用一个属性和值。它们的格式是margin-跟上top, right, bottom, left。如下：
```css
div {
  margin-top: 10px;
  padding-left: 6px;
}
```
当仅仅需要设置内边距或外边距的一个值的时候，可以使用完整的写法。这样可以保证我们的代码明晰并避免在后续的过程中困惑。例如，我们真的需要将top, right, left的外边距值设置为0像素吗？还是我们仅仅需要将bottom的外边距值设置为10像素？在这种情况下使用完整写法会让我们的目标看起来更明确。当然，如果要多个边的情况下，简写是非常好用的！。

> Margin和Padding的颜色
> margin和padding属性是完全透明，且不接收颜色值的。但是由于其是透明的，那么它们的背景色就和一些HTML元素相关。对于margin来说，其需要参考父元素的背景色，而对于padding来说，是当前元素的背景色。for padding, we see the background color of the element the padding is applied to.

### 边框
border是处于内边距和外边距用来表示HTML元素轮廓的部分。border属性需要三个值：width，style，color，如使用简写的方式来表示border属性，那么其值的顺序是：width style color，如果使用完整的写法，这三个值可以分开用border-width，border-style，border-color属性来分别表示，它们对我们想修改border的某一个属性的时候非常有用。

CSS中border的width和color值可以用我们在第三课讨论的常见的长度单位和颜色来定义，

border有不同的[外观](http://www.quackit.com/html/codes/html_borders.cfm),最常用的style值有solid double dashed dotted none。

如下的示例代码中定义了div元素的border为宽度是6像素，solid，灰色。

```css
div {
  border: 6px solid #949599;
}
```
`Border Demo`

```HTML
<code class="border-solid">2px <br> solid</code>

<code class="border-double">6px <br> double</code>

<code class="border-dashed">8px <br> dashed</code>

<code class="border-dotted">4px <br> dotted</code>
```

```css
code {
  background: #eaeaed;
  color: #666;
  font: 14px/24px "Source Code Pro", Inconsolata, "Lucida Console", Terminal, "Courier New", Courier;
  display: inline-block;
  height: 70px;
  margin: 0 14px;
  padding-top: 20px;
  text-align: center;
  width: 90px;
}
.border-solid {
  border: 2px solid #9799a7;
}
.border-double {
  border: 6px double #9799a7;
}
.border-dashed {
  border: 8px dashed #9799a7;
}
.border-dotted {
  border: 4px dotted #9799a7;
}
```

#### 单个边框的边
和margin，padding属性一样，border可以一次设置一个边，这样做的话，我们需要新的属性：border-top border-right border-bottom border-left，这些属性的值和单独使用border属性的值一样，都有:width style color三个值。 下面的代码展示了如何只设置下边框：
```css
div {
  border-bottom: 6px solid #949599;
}
```

此外，单个边框的样式可以更加细微的控制，例如我们只想控制下边框的宽度：
```css
div {
  border-bottom-width: 12px;
}
```



#### 边框的半径
在我们讨论边框的不同属性的时候，顺带讨论一下border-radius属性，可以让我们绘制圆角。

border-radius属性可以接收如百分比和像素这样的长度单位，它可以定义HTML元素的某个角的圆角半径。如果有两个值，则会按照从左上/右下到右上/左下的顺序来设置。如果4个值则会按照top-left top-right bottom-right bottom-right bottom-left的边角顺序来设置。只要记住它们都是顺时针方向的就好。

```css
div {
  border-radius: 5px;
}
```

`Border Radius Demo`

HTML
``` html
<code class="border-rounded">5px</code>
<code class="border-circle">50%</code>
<code class="border-football">15px 75px</code>
```

CSS

``` css
code {
  background: #eaeaed;
  color: #666;
  font: 14px/24px "Source Code Pro", Inconsolata, "Lucida Console", Terminal, "Courier New", Courier;
  display: inline-block;
  height: 90px;
  line-height: 90px;
  margin: 0 14px;
  text-align: center;
  width: 90px;
}
.border-rounded {
  border-radius: 5px;
}
.border-circle {
  border-radius: 50%;
}
.border-football {
  border-radius: 15px 75px;
}
```

border-radius属性也可以划分为更加细的写法，让我们改变某个角的圆角半径。 它们都以border开始，接着是垂直位置（top/bottom）与水平位置（left/right）,然后是radius，例如：border-top-right-radius

```css
div {
  border-top-right-radius: 5px;
}
```



### 边框尺寸

到目前为止Box模型都是用的递增式设计，也就是假设你设置一个HTML元素的width值为400像素，四周的padding值为20像素，四周的border为10像素，那么其实该元素的总宽度值是460像素。

然而Box模型是可以修改为不同的计算方式的。CSS3中引入了box-sizing属性，可以让我们Box模型的工作方式以及HTML元素的尺寸是怎么计算的。该属性有三个主要的值：content-box, padding-box，border-box每个值对如何计算box的尺寸都有影响。

#### content-box
content-box是默认值，也就是让box模型保持递增方式。如果我们不用box-sizing属性，它将会是所有HTML元素的默认值，那么某个元素的尺寸计算方式就是从width和height属性值开始，累加padding, border, margin属性值。

```css
div {
  -webkit-box-sizing: content-box;
     -moz-box-sizing: content-box;
          box-sizing: content-box;
}
```

> 基于浏览器的属性和值 Browser-Specific Properties & Values
> box-sizing属性之前的连字符和字符串是什么呢？
>
> As CSS3 was introduced, browsers gradually began to support different properties and values, including the box-sizing property, by way of vendor prefixes. As parts of the CSS3 specification are finalized and new browser versions are released, these vendor prefixes become less and less relevant. As time goes on, vendor prefixes are unlikely to be a problem; however, they still provide support for some of the older browsers that leveraged them. We may run across them from time to time, and we may even want to use them should we wish to support older browsers.

> Vendor prefixes may be seen on both properties and values, all depending on the CSS specification. Here they are shown on the box-sizing property. Browser vendors were free to chose when to use a prefix and when not to. Thus, some properties and values require vendor prefixes for certain browser vendors but not for others.

> Moving forward, when a property or value needs a vendor prefix, the prefix will only be used in the introduction of that property or value (in the interest of keeping our code digestible and concise). Do not forget to add the necessary vendor prefixes when you’re actually writing the code.

>For reference, the most common vendor prefixes are outlined here:

> * Mozilla Firefox: -moz-
> * Microsoft Internet Explorer: -ms-
> * Webkit (Google Chrome and Apple Safari): -webkit-

#### padding-box
padding-box值让box模型让padding的属性值归于HTML元素的width和height内。当我们使用padding-box值时候，如果一个HTML元素的width值为400像素，且它的padding值是20像素，那么该元素的实际值仍然是400像素。随着padding值的增加，内容的尺寸会缩小。

如果我们添加了border和margin值，在计算box尺寸是这些值会追加到width和height属性值上。例如我们有一个border值为10像素，padding值为20像素，其width值为400像素，其实际宽度是420像素。

```css
div {
  box-sizing: padding-box;
}
```

#### border-box
最后一个值是border-box，当我们设置HTML元素的width和height属性值后，就已经包含了border和padding属性值范围。当我们使用了 ，假设我么设置了一个HTML元素的width为400像素，每边的padding值为20像素，每边的border值为10像素，，那么其总宽度依旧是400像素。

如果我们设置的margin值，这些值需要被添加到box的尺寸中去，也就是，无论box-sizing的值设置为什么，margin的值总是需要添加的。
```css
div {
  box-sizing: border-box;
}
```

Fig 4
Different box-sizing values allow the width of an element—and its box—to be calculated from different areas

#### 选择一个合适box-sizing值
通常来说，最好的box-sizing值是border-size，它会使我们的计算更加简单，假设，我们需要设置一个元素的宽度为400像素，那么不管我们如何设置padding和border的值，该元素的宽度总是保持为400像素。

此外，我们还可以混用长度值。假设我们需要将我们的box设为40%的宽度，并设置四周的padding值为20像素，border值为10像素也不难，尽管我们在其他地方使用了像素，但我们依旧可以保证我们的box为40%。

使用box-sizng属性值的唯一确定就是，这个内容是在CSS3中提出来的，并不是所有的浏览器都支持，尤其是老版本的浏览器并不支持。幸运的是在新的浏览器中这种情况比较少见了。也就是说我们可以使用box-sizing属性，但需要注意可能出现的问题，知道这些问题会在哪些浏览器中产生将会很有帮助。


## 开发者工具
大部分浏览器都有开发者工具。这些工具让我们可以查看网页的各个元素，比如位置，使用了什么CSS属性和值等等，这些工具中大部分包括了Box模型图用来与计算元素的尺寸。

以Chrome为例，找到菜单-> 更多工具 -> 开发者工具


---
在学HTML和CSS时，Box模型是最复杂的部分之一，但也是HTML和CSS中最强大的部分之一，一旦我们熟练掌握，其他的各项内容，比如内容位置排放就会显得尤其简单。



## 实践
Let’s jump back into our Styles Conference website to center it on the page and add some more content.

1. Let’s start by adjusting our box size to use the border-box version of the box model, which will make sizing all of our elements much easier. Within our main.css file, just below our reset, let’s add a comment to identify the code for what will become our grid and help determine the layout of our website. We’re putting this below our reset so that it falls in the proper position within the cascade.

From there, we can use the universal selector, *, along with universal pseudo-elements, *:before and *:after, to select every imaginable element and change the box-sizing to border-box. Remember, we’re going to want to include the necessary vendor prefixes for the box-sizing property, as it is a relatively new property.

``` css
/*
  ========================================
  Grid
  ========================================
*/

*,
*:before,
*:after {
  -webkit-box-sizing: border-box;
     -moz-box-sizing: border-box;
          box-sizing: border-box;
}
```

2. Next we’ll want to create a class that will serve as a container for our elements. We can use this container class on different elements to set a common width, center the elements on the page, and apply some common horizontal padding.

Just below our universal selector rule set, let’s create a selector with a class of container. Within this selector let’s set our width to 960 pixels, our left and right padding to 30 pixels, our top and bottom margins to 0, and our left and right margins to auto.

Setting a width tells the browser definitively how wide any element with the class of container should be. Using a left and right margin of auto in conjunction with this width lets the browser automatically figure out equal left and right margins for the element, thus centering it on the page. Lastly, the left and right padding ensures that our content isn’t sitting directly on the edge of the element and provides a little breathing room for the content.

```css
.container {
  margin: 0 auto;
  padding-left: 30px;
  padding-right: 30px;
  width: 960px;
}
```

3. Now that we have a container class available to use, let’s go ahead and apply the class of container throughout our HTML to the <header> and <footer> elements on each page, including the index.html, speakers.html, schedule.html, venue.html, and register.html files.

```html
<header class="container">...</header>

<footer class="container">...</footer>
```

4. While we’re at it, let’s go ahead and center the rest of the content on our pages. On the home page, our index.html file, let’s add the class of container to each <section> element on the page, one for our hero section (the section that introduces our conference) and one for our teasers section.

```html
<section class="container">...</section>
```
Additionally, let’s wrap all of the <h1> elements on each page with a <section> element with the class of container.
```html
<section class="container">
  <h1>...</h1>
</section>
```
We’ll come back and adjust these elements and classes later, but for now we’re headed in the right direction.

5. Now that all of our content is centered, let’s create some vertical spacing between elements. For starters let’s place a 22-pixel bottom margin on a few of our heading and paragraph elements. We’ll place and comment on these typography styles below our grid styles.

```css
/*
  ========================================
  Typography
  ========================================
*/

h1, h3, h4, h5, p {
  margin-bottom: 22px;
}
```
We intentionally skipped <h2> and <h6> elements, as the design does not call for margins on <h2> elements and as we won’t be using any <h6> elements at this time.

6. Let’s also try our hand at creating a border and some rounded corners. We’ll start by placing a button within the top <section> element on our home page, just below the header.

Previously we added an <a> element within this <section> element. Let’s add the classes of btn and btn-alt to this anchor.

```html
<a class="btn btn-alt">...</a>
```
Now let’s create some styles for those classes within our CSS. Below our typography rule set, let’s create a new section of the CSS file for buttons.

To begin let’s add the btn class and apply some common styles that can be shared across all buttons. We’ll want all of our buttons to have a 5-pixel border-radius. They should be displayed as inline-block elements so we can add padding around all four sides without issue; we’ll remove any margin.

```html
/*
  ========================================
  Buttons
  ========================================
*/

.btn {
  border-radius: 5px;
  display: inline-block;
  margin: 0;
}
```

We’ll also want to include styles specific to this button, which we’ll do by using the btn-alt class. Here we’ll add a 1-pixel, solid, gray border with 10 pixels of padding on the top and bottom of the button and 30 pixels of padding on the left and right of the button.

```css
.btn-alt {
  border: 1px solid #dfe2e5;
  padding: 10px 30px;
}
```
Using both the btn and btn-alt classes on the same <a> element allows these styles to be layered on, rendering all of the styles on a single element.

7. Because we’re working on the home page, let’s also add a bit of padding to the <section> element that contains our <a> element with the classes of btn and btn-alt. We’ll do so by adding a class attribute value of hero to the <section> element, alongside the container class attribute value, as this will be the leading section of our website.

```html
<section class="hero container">
  ...
</section>
```

Next we’ll want to create a new section within our CSS file for home page styles, and, once we’re ready, we’ll use the class of hero to apply padding around all four sides of the <section> element.

```css
/*
  ========================================
  Home
  ========================================
*/

.hero {
  padding: 22px 80px 66px 80px;
}
```
Our website is starting to come together, especially the home page.

[!Fig04.05.png]
Fig 4
Our Styles Conference home page, taking shape after a few updates

### Demo 和源代码
* [Demo](http://learn.shayhowe.com/practice/opening-the-box-model/index.html)
* [源代码](http://learn.shayhowe.com/practice/opening-the-box-model.zip)

> 通用选择器
> 在上面第一步的时候，我们简单介绍了通用选择器，在CSS中，* 就是一个通用选择器，它可以选择全部的HTML元素。
> 在第一步中，我们也提到了:before和:after伪元素，它们可以通过CSS动态生成，尽管在我们的项目中不会使用这些元素 however, when using the universal selector it’s a good practice to also include these pseudo-elements in case they should ever appear.


## 总结
学习Box模型的各个部分不是小成绩。这些概念经过简单介绍了，但要成为大师，则需要一段时间，而我们正在往这个方向发展。
简单回顾下，我们这节课讲了什么内容：
* 不同的元素是如何显示的
* Box模型是什么以及为什么很重要
* 如何修改元素的尺寸，包括高度和宽度
* 如何给元素添加margin，padding和border
* 如何修改元素的box-sizing值，已经它们是如何影响这个box模型的。

现在我们已经更加了解了HTML元素是如何显示以及调节尺寸的，接下来就该设置这些元素的位置了。


## 资源与链接
* [The CSS Box Model](http://css-tricks.com/the-css-box-model/) via CSS-Tricks 
* [HTML Borders](http://css-tricks.com/the-css-box-model/) via Quackit.com

## 课程链接
* [课程03：了解CSS](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_03_Getting_to_Know_CSS.md)
* [课程05：内容定位](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_05_Positioning_Content.md)