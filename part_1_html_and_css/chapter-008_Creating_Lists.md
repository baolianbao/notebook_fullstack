title: 课程08：创建列表
date: 2016-04-08 00:00:05
tags: [html,css]
categories: HTML And CSS
---

## 概述
---
列表是日常生活中不可或缺的部分，任务列表、方向导航列表，菜单列表等等。

在网站中使用列表我们有三个选择：无序列表、有序列表和解释列表。

除了默认的三种类型的列表外，我们有多种方式来设置列表的样式，例如使用什么标记，是方块、圆点，数字，字母或者根本不用。同样我们也可以设置是水平显示还是垂直显示列表。

<!--more-->

`HTML`
* 无序列表
* 有序列表
* 描述列表
* 嵌套列表

`CSS`
* 列表元素样式
* 水平显示列表


## 无序列表
---
可以使用`<ul>`块元素来创建无序列表其中每个列表元素通过`<li>`创建。
默认情况下，大部分浏览器会给`<ul>` 元素添加垂直`margin`值和左侧`padding`值，并让每个`<li>`元素用实心点开始，该实心点称为列表元素的标记，可以通过CSS来修改。
```html
<ul>
  <li>Orange</li>
  <li>Green</li>
  <li>Blue</li>
</ul>
```

## 有序列表
---
可以使用`<ol>`元素来创建有序列表，使用方法和无序列表差不多，只不过它不是用实心点来作为列表元素的标记，而是数字。

```HTML
<ol>
  <li>Head north on N Halsted St</li>
  <li>Turn right on W Diversey Pkwy</li>
  <li>Turn left on N Orchard St</li>
</ol>
```
有序列表还有独特的属性`start` 和`reversed`

### `start`属性
`start`属性定义了有序列表从什么数字开始排序，默认情况下是1，虽然有序列表可以使用不同的数值系统例如罗马数值，但`start`属性只可以接收实数值。

```html
<ol start="30">
  <li>Head north on N Halsted St</li>
  <li>Turn right on W Diversey Pkwy</li>
  <li>Turn left on N Orchard St</li>
</ol>
```

### `reversed`属性
`reversed` 属性可以让有序列表反向排序，`reversed` 属性是布尔值属性，也就是不接收其他值，要么true要么false，false是默认值。仅仅在属性名称`reversed`出现在`<ol>`元素中的时候才表示`true`。
```html
<ol reversed>
  <li>Head north on N Halsted St</li>
  <li>Turn right on W Diversey Pkwy</li>
  <li>Turn left on N Orchard St</li>
</ol>
```

### `value`属性
`value` 属性可以用于有序列表中任意一个`<li>` HTML 元素，在指定了`value`属性值以下的所有列表元素的`value` 属性都会重新计算。
例如，如果第二个元素的`value`属性值被设置为`9` 那么它的列表元素的标记就是 `9` ，它以下的所有元素的标记就从`9`开始递增。

```html
<ol>
  <li>Head north on N Halsted St</li>
  <li value="9">Turn right on W Diversey Pkwy</li>
  <li>Turn left on N Orchard St</li>
</ol>
```

## 描述列表
---
在网上见到的另外一种列表（不如有序列表和无序列表常见）是描述列表。描述列表往往用于表示多个词语以及词语的描述，例如词汇表之类的。

我们可以通过块元素`<dl>`来创建创建列表，它的元素不适用`<li>` 元素，而是适用两个块元素：`<dt>` 描述术语(term)元素，`<dd>` 描述内容(description)元素。

一个描述列表可以有多个术语和描述，此外，每个术语可以有一个描述或多个描述，一个术语可能有多个意思和多个描述，相反的，一个描述也可能对应多个术语。

当创建描述列表的时候，`<dt>`元素必须在`<dd>`元素之前。 它们的显示顺序与定义顺序一致。

默认情况下`<dl>`元素和`<ul>` `<ol>`元素一样保护了垂直margin，此外`<dd>`元素默认保证左`margin`

```html
<dl>
  <dt>study</dt>
  <dd>The devotion of time and attention to acquiring knowledge on an academic subject, especially by means of books</dd>
  <dt>design</dt>
  <dd>A plan or drawing produced to show the look and function or workings of a building, garment, or other object before it is built or made</dd>
  <dd>Purpose, planning, or intention that exists or is thought to exist behind an action, fact, or material object</dd>
  <dt>business</dt>
  <dt>work</dt>
  <dd>A person's regular occupation, profession, or trade</dd>
</dl>
```

## 嵌入列表
---
列表有一个很强大的属性就是它们之间可以互相嵌套。But the potential to nest lists indefinitely doesn’t provide free rein to do so. Lists should still be reserved specifically for where they hold the most semantic value.

使用嵌套列表的一个技巧就是知道从哪儿开始从哪儿结束。常常使用嵌套类别的是有序列表和无序列表，包含`<ul>` `<ol>`元素的仅仅是`<li>`元素。


```html
<ol>
  <li>Walk the dog</li>
  <li>Fold laundry</li>
  <li>
    Go to the grocery and buy:
    <ul>
      <li>Milk</li>
      <li>Bread</li>
      <li>Cheese</li>
    </ul>
  </li>
  <li>Mow the lawn</li>
  <li>Make dinner</li>
</ol>
```

在使用嵌套列表是需要注意的一点是，取决于嵌套列表的嵌套程度，它们的列表元素的标记会相应的变化。


## 列表元素样式
无序列表和有序列表默认会使用列表元素标记。无序列表默认会使用实心点，有序列表默认会使用数字。[通过CSS](http://www.smashingmagazine.com/2009/12/11/styling-html-lists-with-css-techniques-and-resources/)，这些列表元素的标记的样式和位置都可以调整。

### 列表样式类型属性
`list-style-type` 属性用于设置列表元素标记的内容，其[值范围](https://developer.mozilla.org/en-US/docs/Web/CSS/list-style-type) 从方块，数值一直到亚美尼亚编号，这些样式可以放到`<ul>` `<ol>` `<li>`中。

任何`list-style-type`属性值都可以被添加到有序列表或者无序列表中。也就是说，通过这个属性可以对无序列使用数值列表元素标记，以及对有序列表使用非数值列表元素标记。

```html
<ul>
  <li>Orange</li>
  <li>Green</li>
  <li>Blue</li>
</ul>
```

```css
ul {
  list-style-type: square;
}
```

#### 列表样式类型值
正如之前所提到的，`list-style-type`属性几个不同的值。

| 列表样式值                   | 内容|
|--------                     |---  |
| `none`                      | No list item |
| `disc`                      | A filled circle |
| `circle`                    | A hollow circle |
| `square`                    | A filled square |
| `decimal`                   | Decimal numbers |
| `decimal-leading-zero`      | Decimal numbers padded by initial zeros |
| `lower-roman`               | Lowercase roman numerals |
| `upper-roman`               | Uppercase roman numerals |
| `lower-greek`               | Lowercase classical Greek |
| `lower-alpha / lower-latin` | Lowercase ASCII letters |
| `upper-alpha / upper-latin` | Uppercase ASCII letters |
| `armenian`                  | Traditional Armenian numbering |
| `georgian`                  | Traditional Georgian numbering |


### 使用图片作为列表元素标记
有些时候`list-style-type`的属性值不能完全满足我们的需求，我们想自定义列表的标记，可以通过设置每个`<li>`元素的背景图片来实现。

实现的过程是，先一处默认的`list-style-type`属性值，也就是讲其属性值设置为`none`， 然后设置`<li>` 元素的背景图，当然需要设置背景图片的一些属性值，例如用什么图片，位置，平铺值，如果有必要，还需要设置`padding`值。

```HTML
<ul>
  <li>Orange</li>
  <li>Green</li>
  <li>Blue</li>
</ul>
```

```css
li {
  background: url("arrow.png") 0 50% no-repeat;
  list-style-type: none;
  padding-left: 12px;
}
```

### 列表样式定位属性

默认情况下列表元素标记位于`<li>`元素的左侧，这是通过`list-style-position`的属性值`outside` 来指定的，它表示所有的内容都在列表元素标记意外，并位于列表元素标记右侧，这是默认值，我们可以将其修改为`inside` `inherit`。

`inside`属性值很少使用，它会将列表元素标记？？？The inside property value (which is rarely seen or used) places the list item marker in line with the first line of the <li> element and allows other content to wrap below it as needed.

```html
<ul>
  <li>Cupcakes...</li>
  <li>Sprinkles...</li>
</ul>
```

```css
ul {
  list-style-position: inside;
}
```

### 列表样式属性简写形式
到目前为止我们所讨论的列表样式属性`list-style-type` 和`list-style-position`可以通过`list-style`属性来简单表示。它的值可以是一个值或多个，值得顺序是`list-style-type` `list-style-position`。
```css
ul {
  list-style: circle inside;
}
ol {
  list-style: lower-roman;
}
```

## 水平显示列表
有些时候我们想水平显示列表，比如我们希望将列表分为多个列用于建立导航列表， 或者将少量列表元素放到一行。 取决与内容和外观，我们有几种不同的方式来讲列表设置于一行，例如通过设置`<li>`元素的属性值为`inline` 或
`inline-block` 或者 将列表元素浮动。

### 显示列表
将所有的列表元素一行显示的最快的方式是将`<li>`元素的`display`属性值修改为`inline`或`inline-block`，其结果是所有的`<li>`位于一行，每个列表元素之间的间隔是一个空格。

如果`<li>`元素之间的间距出现问题，我们可以使用在第五课中使用得技术来处理。

通常情况下，我们会使用`inline-block`值而非`inline`属性值。`inline-block`属性值可以让我易于设置垂直margin，以及`<li>`元素之间的其他间隔。

当我们将`display`属性修改为`inline`或者`inline-block`的时候，列表元素的标记会消失。

```html
<ul>
  <li>Orange</li>
  <li>Green</li>
  <li>Blue</li>
</ul>
```

```css
li {
  display: inline-block;
  margin: 0 10px;
}
```

### 浮动列表
修改`display`属性值的方法比较快，但是它去除了列表元素的标记，如果列表元素标记是必须的话，将每个`<li>`列表元素设置为浮动是个好的选项。

将所有的`<li>`元素的`float`值设置为`left` 会将所有的`<li>`元素水平紧挨。当我浮动每个`<li>`元素的时候，列表元素标记默认会显示在紧挨的列表元素的上方，为避免这种情况的出现，需要设置水平方向的`margin` 或`padding` 值。

```html
<ul>
  <li>Orange</li>
  <li>Green</li>
  <li>Blue</li>
</ul>
```

```css
li {
  float: left;
  margin: 0 20px;
}
```
和浮动其他元素一样，会破坏页面的设计流，我们必须记住清除浮动——通常使用得是`clearfix`技术——其会将页面恢复到正常流布局。

### 导航列表示例
同在在开发，查找，导航菜单时使用无序列表。通常情况下，我们会使用如上的技术让列表元素水平显示。如下的示例展示了如何使用无序列表，将其 `display`属性修改为`inline-block`制作的导航菜单
```html
<nav class="navigation">
  <ul>
    <li><a href="#">Profile</a></li><!--
    --><li><a href="#">Settings</a></li><!--
    --><li><a href="#">Notifications</a></li><!--
    --><li><a href="#">Logout</a></li>
  </ul>
</nav>
```

```css
.navigation ul {
  font: bold 11px "Helvetica Neue", Helvetica, Arial, sans-serif;
  margin: 0;
  padding: 0;
  text-transform: uppercase;
}
.navigation li {
  display: inline-block;
}
.navigation a {
  background: #395870;
  background: linear-gradient(#49708f, #293f50);
  border-right: 1px solid rgba(0, 0, 0, .3);
  color: #fff;
  padding: 12px 20px;
  text-decoration: none;
}
.navigation a:hover {
  background: #314b60;
  box-shadow: inset 0 0 10px 1px rgba(0, 0, 0, .3);
}
.navigation li:first-child a {
  border-radius: 4px 0 0 4px;
}
.navigation li:last-child a {
  border-right: 0;
  border-radius: 0 4px 4px 0;
}
```


### 实践
Now that we know how to build lists within HTML and CSS, let’s loop back to our Styles Conference website and see where we might be able to use lists.
1. Currently the navigation menus within the <header> and <footer> elements on our pages consist of a handful of anchor elements. These anchor elements could be better organized in an unordered list.

Using an unordered list (via the <ul> element) and list items (via the <li> element) will give structure to our navigation menus. These new elements, however, will display our navigation menus vertically.

We’re going to want to change the display value of our <li> elements to inline-block to get all of them to align in a horizontal row. When we do that, though, we’ll also need to account for the blank space left between each <li> element. Thinking back to Lesson 5, “Positioning Content,” we know that opening an HTML comment at the end of a <li> element and closing an HTML comment at the beginning of a <li> element will remove this space.

Keeping this in mind, the markup for the navigation menu within our <header> element will now look like this:
```html
<nav class="nav primary-nav">
  <ul>
    <li><a href="index.html">Home</a></li><!--
    --><li><a href="speakers.html">Speakers</a></li><!--
    --><li><a href="schedule.html">Schedule</a></li><!--
    --><li><a href="venue.html">Venue</a></li><!--
    --><li><a href="register.html">Register</a></li>
  </ul>
</nav>
```
Along these same lines, the markup for the navigation menu within our <footer> element will now look like this:
```html
<nav class="nav">
  <ul>
    <li><a href="index.html">Home</a></li><!--
    --><li><a href="speakers.html">Speakers</a></li><!--
    --><li><a href="schedule.html">Schedule</a></li><!--
    --><li><a href="venue.html">Venue</a></li><!--
    --><li><a href="register.html">Register</a></li>
  </ul>
</nav>
```
Let’s not forget to make these changes in all of our HTML files.

2. With the unordered list in place, let’s make sure the list items align horizontally, and let’s clean up their styles a bit. We’ll use the existing nav class to help target our new styles.

We’ll begin by setting all of the <li> elements within any element with the class attribute value of nav to be displayed inline-block, to include some horizontal margins, and to be vertically aligned to the top of the element.

Additionally, we’ll use the :last-child pseudo-class selector to identify the last <li> element and reset its right margin to 0. Doing so ensures that any horizontal space between the <li> element and the edge of its parent element is removed.

Within our main.css file, below our existing navigation styles, let’s add the following CSS:
```css
.nav li {
  display: inline-block;
  margin: 0 10px;
  vertical-align: top;
}
.nav li:last-child {
  margin-right: 0;
}
```
You may be wondering why our unordered list didn’t include any list item markers or default styles. These styles were removed by the reset at the top of our style sheet. If we look at the reset, we’ll see our <ol>, <ul>, and <li> elements all include a margin and padding of 0, and our <ol> and <ul> elements have a list-style value of none.

3. Our navigation menus aren’t the only places we’ll be using lists. We’ll also use them on some of our internal pages, including the Speakers page. Let’s add some speakers to our conference.

Within our speakers.html file just below our lead section, let’s create a new section where we’ll present all of our speakers. Reusing some existing styles, we’ll use a <section> element with a class attribute value of row to wrap all of our speakers and apply a white background and padding behind them. Inside the <section> element, we’ll add a <div> element with a class attribute value of grid to center our speakers on the page and allow us to use multiple columns in doing so.

So far our HTML below the lead section looks like this:
```html
<section class="row">
  <div class="grid">

  </div>
</section>
```
4. Inside the grid every speaker will be marked up with his or her own <section> element, which will include two columns. The first column will span two-thirds of the <section> element and will be marked up using a <div> element. The second column will span the remaining one-third of the <section> element and will be marked up using an <aside> element, as its content is secondary to the speaker and his or her specific talk.

Using our existing col-2-3 and col-1-3 classes, the outline for a speaker section will look like this:
```html
<section id="shay-howe">

  <div class="col-2-3">
    ...
  </div><!--

  --><aside class="col-1-3">
    ...
  </aside>

</section>
```
There are a few items to notice here. First, each <section> element for each speaker includes an ID attribute with the speaker’s name as the attribute value. Later, when we create the schedule for our conference, these ID attributes will serve as anchors, allowing us to link from the schedule to a speaker’s profile.

Additionally, the closing tag of the <div> element is followed by the opening of an HTML comment, and the opening tag of the <aside> element is preceded by the closing of an HTML comment. Because the column-based classes will display these elements as inline-block elements, we are removing the blank space that will appear between them.

5. Inside the two-thirds column, marked up with the <div> element, we’ll use a few headings and paragraphs to show the speaker’s name, the title and abstract of the talk, and a short biography.

Including this content, a speaker section will look like this:
```html
<section id="shay-howe">

  <div class="col-2-3">

    <h2>Shay Howe</h2>
    <h5>Less Is More: How Constraints Cultivate Growth</h5>

    <p>By setting constraints, we force ourselves...</p>

    <h5>About Shay</h5>

    <p>As a designer and front-end developer, Shay...</p>

  </div><!--
  --><aside class="col-1-3">
    ...
  </aside>
</section>
```

6. Within the one-third column, marked up with an <aside> element, we’re going to add a <div> element with a class attribute value of speaker-info. We’ll use a <div> element because we’ll be adding styles to this element soon.

Before getting into any styles, though, let’s add an unordered list within the <div> element that includes as list items some relevant links for the speaker.

Now our HTML for a speaker will look like this:
```html
<section id="shay-howe">

  <div class="col-2-3">

    <h2>Shay Howe</h2>
    <h5>Less Is More: How Constraints Cultivate Growth</h5>

    <p>By setting constraints, we force ourselves...</p>

    <h5>About Shay</h5>

    <p>As a designer and front-end developer, Shay...</p>

  </div><!--

  --><aside class="col-1-3">
    <div class="speaker-info">

      <ul>
        <li><a href="https://twitter.com/shayhowe">@shayhowe</a></li>
        <li><a href="http://learn.shayhowe.com/">learn.shayhowe.com</a></li>
      </ul>
    </div>
  </aside>
</section>
```

7. With the <div> element with a class attribute value of speaker-info ready, we can add some styles to it.

We’ll begin by adding a new section within our main.css file for the Speaker page styles. From there, let’s add a 1-pixel solid gray border with a 5-pixel radius around any element that includes the class attribute value of speaker-info.

Next, let’s add a top margin of 88 pixels to position the element on the same vertical line as the first paragraph of the talk description, and let’s also add 22 pixels of vertical padding inside the element to provide room for the nested unordered list.

Lastly, let’s center all of the text within the element.

In all, our CSS for the speaker-info class rule set looks like this:
```css
/*
  ========================================
  Speakers
  ========================================
*/

.speaker-info {
  border: 1px solid #dfe2e5;
  border-radius: 5px;
  margin-top: 88px;
  padding: 22px 0;
  text-align: center;
}
```
Let’s take a minute to review why we’re using a <div> element here and the corresponding styles.

We’re placing a <div> element inside the <aside> element with the class attribute value of col-1-3 because we’ll want the padding inherited from the col-1-3 class to be outside of the border on the <div> element. Before long we’ll be including an image within the <div> element, alongside the unordered list; therefore we created a <div> element as opposed to applying these styles directly to the <ul> element.

8. As we add more and more speakers to the page, we’ll want to ensure that they remain an equal distance apart vertically. To do so, we’ll create a speaker class rule set which includes a bottom margin of 44 pixels, like this:
```css
.speaker {
  margin-bottom: 44px;
}
```
We can then apply this class to the <section> element for each speaker, provided it isn’t the last speaker. We’ll omit this class on the last speaker, as we don’t want to create any unnecessary margins before our <footer> element. With more than one speaker, our layout will look like this:
```html
<section class="row">
  <div class="grid">

    <section class="speaker" id="chris-mills">

      <div class="col-2-3">
        ...
      </div><!--

      --><aside class="col-1-3">
        ...
      </aside>

    </section>

    <section id="shay-howe">

      <div class="col-2-3">
        ...
      </div><!--

      --><aside class="col-1-3">
        ...
      </aside>

    </section>

  </div>
</section>
```

Notice how the first speaker <section> element, for Chris Mills, includes the class attribute value of speaker, which vertically separates it from the speaker <section> element for myself, Shay Howe. The last speaker <section> element, again for myself, doesn’t include a class attribute value of speaker in order to keep it a proper distance from the <footer> element.

Our navigation menus are now complete, and the Speakers page is taking shape.

![](Fig08.01.png)
Fig 8
Our Speakers page after updating our navigation menus and adding speakers

## Demo 和源码
* [Demo](http://learn.shayhowe.com/practice/creating-lists/index.html)
* [源码](http://learn.shayhowe.com/practice/creating-lists.zip)

## 总结
[列表]() 在HTML中比较常见，经常会出现在那些不是显而易见的地方  The key is to use them as semantically as possible and to leverage them where they best fit.

简单回顾：
* 如何创建有序、无序、描述列表
* 如何嵌套列表
* 如何修改列表元素的标记和位置
* 如何使用背景图作为列表元素标记
* 列表如何水平显示或浮动

现在我们知道了如何在页面中添加列表，接下来学习如何在列表中添加多媒体，包括如何添加图片，音频，视频等等。


## 资源和链接
* [Styling HTML Lists with CSS](http://www.smashingmagazine.com/2009/12/11/styling-html-lists-with-css-techniques-and-resources/) via Smashing Magazine
* [List Style Type](https://developer.mozilla.org/en-US/docs/Web/CSS/list-style-type) via Mozilla Developer Network
* [CSS Design: Taming Lists](http://alistapart.com/article/taminglists) via A List Apart







## 课程链接
* [课程07：背景和渐变](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_07_Setting_Backgrounds_And_Gradients.md)
* [课程09：添加多媒体](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_09_Adding_Media.md)
