title: 课程02： 了解HTML
date: 2016-04-08 00:00:11
tags: [html,css]
categories: HTML And CSS
---

在介绍完HTML和CSS之后，我们需要深入了解HTML，找到组成该语言的不同组件。

在开始构建网站之前，我们需要知道什么类型的内容使用什么HTML元素最好，知道HTML元素是如何在网页上显示及不同的HTML元素在语意上是什么意思的也非常重要。

在恰当的环境下使用恰当的HTML元素。
<!-- more -->

## 语意概述
---
语意是什么意思？
HTML中的语意表示使用正确的HTML元素来表示其意思及结构。语意代码仅仅描述网页内容的价值，而不管内容的外观或样式。

使用语意元素有如下的好处：
包括让计算机，Screen Readers， 搜索引擎，或其他设备能充分读取和理解网页的内容。此外，语意代码在工作时更加容易管理，它展示了每段内容是用来干什么的。

往后，当我们介绍一个新元素的时候，我们会讨论这些元素实际上是什么意思，这些元素最好用来展示什么内容。 在开始之前，我们看看两个并没有什么语意价值的元素——<div> 和 <span> ，它们存在仅仅是为了样式。

## 区分Div和Span
---
Div和 span仅仅是作为HTML元素容器。 作为一个容器，它们并没有什么语意，<p>元素包裹的内容在语意上解释就是段落， div 和 span所包裹的内容没有任何这方面的意义。
> **块状 和 行内元素**
>
> 大部分HTML元素不是块状元素就是行内元素的，区别是什么？
>
>块状元素永远开启新的一行，占据整整一行，并一行一行累加，它们可以互相嵌套，也可以包裹行内元素，我们经常用块状元素来表示一大块内容，比如段落。

行内元素不会开启新的一行，正如文档的流一样，一个接着一个，只占据和其内容长度一样的宽度，行内元素可以互相嵌套，但是行内元素不可以包裹块状元素。我们经常会看到行内元素和一小段内容出现在一起，比如几个词。


在构建网站的时候，div和span可以让我们对其包含的内容赋予样式， 都是非常有价值的。

Div是块状元素，常用来标识一组内容，帮住设置网站布局设计，span是行内元素，常常用来表示块状元素内一小组文本内容

我们经常使用看到div 和 span使用 class和id属性来用于修改样式的目的。在设置class和id属性值的时候需要注意点，我们希望选择一个值和内容相关的，而不是该元素的外观。

例如， 假设我们有一个包含社交媒体链接的orange背景的div ，一开始我们也许想给这个div的class属性值设为orange，如果之后我们修改背景色为蓝色呢？这时候class的属性值就没有意义了，更好的选择是将class的值设置为social，它属于div块的内容，而不是样式。

```html
<!-- Division -->
<div class="social">
  <p>I may be found on...</p>
  <p>Additionally, I have a profile on...</p>
</div>

<!-- Span -->
<p>Soon we'll be <span class="tooltip">writing HTML</span> with the best of them.</p>
```


> ** HTML& CSS中的注释**
>
> ***HTML***
>
> `<!-- comment -->`
>
> ***CSS***
>
> `/* */`


## 使用基于文本的HTML元素
---
尽管网上有各种格式的媒体和内容，然而主导的还是文本。相应的也有不同的HTML元素用来在网页上展示文本。 现在我们主要关注那些常用的元素：标题、段落、显得重要的加粗、用于强调的倾斜。之后在课程6中，如何排版，我们将深入探讨如何设置文本样式。？

### 标题
Headings是块状元素，它们有6个级别，`<h1>` 到`<h6>`。标题有助于分散内容建立层次。它们是用户阅读页面的关键标识符。
它们也可以帮助搜索引擎索引及确定网页的内容。

标题使用的时候应该和其内容相关，主标题应该使用`<h1>`元素，子标题根据需要设置为`<h2>` `<h3>`等,每个标题级别的内容应该使用和其语意相符的HTML元素，而不是仅仅让文本加粗或自己变大。

示例：
```html
<h1>Heading Level 1</h1>
<h2>Heading Level 2</h2>
<h3>Heading Level 3</h3>
<h4>Heading Level 4</h4>
<h5>Heading Level 5</h5>
<h6>Heading Level 6</h6>
```
网页：
Heading Level 1
Heading Level 2
Heading Level 3
Heading Level 4
Heading Level 5
Heading Level 6


## 段落
标题之后往往跟着的是段落。段落使用块状元素`<p>`来定义， 段落可以一个接着一个，根据需要向页面添加。 如下是如何设置段落：

```html
<p>Steve Jobs was a co-founder and longtime chief executive officer at Apple. On June 12, 2005, Steve gave the commencement address at Stanford University.</p>

<p>In his address Steve urged graduates to follow their dreams and, despite any setbacks, to never give up&ndash;advice which he sincerely took to heart.</p>
```


## 字体加粗
让文本加粗赋予其重要性，我们使用行内元素`<strong>`。 有两种html元素用于加粗字体：`<strong>` 和<b>元素。明白这两者的语意区别特别重要。

`<strong>`元素语意上是赋予文本很重要的特性，因此使用得比较广泛。 `<b>`元素semantically means to stylistically offset text, which isn’t always the best choice for text deserving prominent attention. We have to gauge the significance of the text we wish to set as bold and to choose an element accordingly. 我们需要根据

以下是如何使用HTML元素示例：
```html
<!-- Strong importance -->
<p><strong>Caution:</strong> Falling rocks.</p>

<!-- Stylistically offset -->
<p>This recipe calls for <b>bacon</b> and <b>baconnaise</b>.</p>
```


### 文本倾斜
让文本倾斜，我们将使用行内元素`<em>`。和让文本加粗一样，有两种不同的HTML元素让文本倾斜，它们有不同的语意区别。

`<em>`元素，用来强调重点文本，因此它也是广泛使用的，另外一个选项`<i>` 用于将一段文本作为语音和语调相关的，几乎是所有放在引号内的情况下。Again, we will need to gauge the significance of the text we want to italicize and choose an element accordingly.

以下是用于倾斜的HTML代码：

```html
<!-- Stressed emphasis -->
<p>I <em>love</em> Chicago!</p>

<!-- Alternative voice or tone -->
<p>The name <i>Shay</i> means a gift.</p>
```

这些文本级的HTML元素给我们的内容带来活力相当方便。 此外，还有基于结构的HTML元素。基于文本的HTML元素用来表示标题和段落，结构元素用来表示一组内容，例如Header，Articles，Footers等等。


## 建立结构
---
长期以来一直使用div来搭建网页结构。 问题是div没有语意，并且确定这些div的实际表示目的很难。幸运的是在HTML5中引入了新的结构化HTML元素，包括`<header>` `<nav>` `<article>` `<section>` `<aside>`和`<footer>`元素。

All of these new elements are intended to give meaning to the organization of our pages and improve our structural semantics.所有这些元素就是想让我们的页面提高结构化语意， 它们都是块状元素，且没有隐含的位置或样式，此外，这些元素根据其正确的语意，在一个页面中可能会使用多次。
来，深入讨论一下。

Fig 2
One possible example of HTML5 structural elements giving meaning to the organization of our pages

### Header 头部
<header>元素，正如其名，用于标识网页、文章、部分、或其他段（segment）的头部，一般来说，<header>元素可能包含标题，介绍，甚至是导航。

<header>...</header>

> `<header>` vs `<head>` vs `<h1>`到`<h6>`
> 这几个元素很容易混淆，它们都有不同的语意，我们应该根据其意思来使用。
>
> `<header>` 元素是结构化元素，用来展示网页的一个片段的头部，且它在`<body>`元素内部
>
> `<head>`元素不会在页面中显示，用来存放包括文档标题，链接的外部文件等元数据，他直接放在`<html>`元素中。


标题元素`<h1>`到`<h6>`在整个页面中用来定义不同层次的文字标题。

### Navigation 导航
The `<nav>` element identifies a section of major navigational links on a page. The <nav> element should be reserved for primary navigation sections only, such as global navigation, a table of contents, previous/next links, or other noteworthy groups of navigational links. `<nav>`元素用来在页面上标识 `<nav>`元素应该

通常情况下，包含在<nav>元素内的链接会链接到当前网站的其他页面或当前网站当前页面的某个部分。其他一次性链接不应当包含在`<nav>` 元素中，它们应该使用锚元素`<a>`

```
<nav>...</nav>
```




### Article 文章
`<article>`元素用来表示可以独立分发或者重复使用的一个独立的，自包含的内容片段，我们常常使用<article>元素来标识博客文章，新闻文章，用户提交内容等等。

When deciding whether to use the <article> element, we must determine if the content within the element could be replicated elsewhere without any confusion. If the content within the <article> element were removed from the context of the page and placed, for example, within an email or printed work, that content should still make sense.当我们在犹豫是否要使用<article>元素之前，我们先要确保该元素是否可以复制到页面的任何地方，且不引起任何混乱（迷惑）。如果<article>元素内的内容ongoing页面上下文中删除或替换了，例如放在邮件中或打印文件，内容仍然有意义。

```html
<article>...</article>
```

### Section 片段
`<section>`元素常常用来标识一个主题内容分组，通常会，但也不总是包含一个标题。The grouping of content within the `<section>` element may be generic in nature, but it’s useful to identify all of the content as related.
The `<section>` element is commonly used to break up and provide hierarchy to a page.

```html
<section>...</section>
```

> 使用`<article>` `<section>`还是`<div>`元素？
> 还是那句话根据语意来选择最适合的元素，在这里选择使用哪个元素取决于内容。
>
> <article><section>元素都用于文档结构和规划文档。 如果某组内容仅仅是用于样式，而对文档大纲没有价值，那就使用<div>

如果内容添加到文档提纲中，且可以独立分发或联合，使用`<article>`元素。

如果内容需要添加到文档提纲，且表示一个主题内容组，使用`<section>`元素。

### Aside
The `<aside>` element holds content, such as sidebars, inserts, or brief explanations, that is tangentially related to the content surrounding it.  `<aside>`元素用来包含诸如sidebars，输入框，或简单说明的内容，主要用于放在相关内容的周围，例如`<article>`元素可以用来表示和文章作者相关的内容。

凭直觉，我们会认为<aside>元素应该放在页面的左侧或右侧。但是我们必须记住的是，所有的结构元素，包括<aside>元素，都是块状元素，默认情况下都会在其嵌入的元素（也称为父元素）中新启用一行并占据一行的全部长度。

```html
<aside>...</aside>
```

我们将会在第五课中探讨如何改变元素的位置。

### Footer
`<footer>` 元素标识着页面、文章、片段或其他段的尾部，一般来说`<footer>`元素通常放在其父对象的最下面。Content within the `<footer>` element should be relative information and should not diverge from the document or section it is included within. 在`<footer>`元素中的内容应该和信息相关，而不要偏离其所在的文档或片段。
```html
<footer>...</footer>
```

在了解结构元素和文本元素之后，我们的HTML知识开始结合起来了，现在该回到我们的Styles Conference 网站看看我们是否可以弄出好一点的结构。


## 实践
---

目前我们的Styles Conference网站缺乏结构和内容，让我们来充实一下我们的网页。

1. 打开`index.html`，添加`<header>`元素，我们的`<header>`元素应该包含已存在的`<h1>`元素，同时也为`<h1>`元素内容添加一个标语元素`<h3>`

```html
<header>
  <h1>Styles Conference</h1>
  <h3>August 24&ndash;26th &mdash; Chicago, IL</h3>
</header>
```

2. 在`<header>`元素后面，使用`<section>`添加一组新的内容来介绍我们的会议，我们使用<h2>元素作为`<section>`的开始，并以已经存在的段落作为终结。

```html
<section>
  <h2>Dedicated to the Craft of Building Websites</h2>
  <p>Every year the brightest web designers and front-end developers descend on Chicago to discuss the latest technologies. Join us this August!</p>
</section>
```

3.  继介绍会议之后，我们添加一组新的内容用于放置演讲人员、计划表、会场这些页面。Following the introduction to our conference, let’s add another group of content that teases a few of the pages we’ll be adding, specifically the Speakers, Schedule, and Venue pages. Each of the pages we’re teasing should also reside within its own section and include supporting text.
我们将这些内容放到一个<section>元素中，每一个又单独的使用<section>包裹起来，总的来说，我们有三个<section>元素包含在一个<section>元素中

```html
<section>

  <section>
    <h5>Speakers</h5>
    <h3>World-Class Speakers</h3>
    <p>Joining us from all around the world are over twenty fantastic speakers, here to share their stories.</p>
  </section>

  ...

</section>
```

4.  最后，在页面的底部，通过`<footer>`元素添加版权信息。使用<small>元素来实现，其语意表示附属组件和小的打印内容，用来表示版权信息正合适。

通常情况下，在`<small>`元素内的内容会被渲染得很小，但由于我们使用了CSS重置，所以看起来不会有什么变化。

```html
<footer>
  <small>&copy; Styles Conference</small>
</footer>
```

现在来看看我们的页面：

Fig 2
Our home page after adding more content and structure


#### 特殊字符编码
上面的案例中，`<header>`中的 `<h3>`元素，以及`<footer>`中的 `<small>` 元素中有些很有意思的东西。

特殊字符包括各种标点符号，重音字符及标志，如果我们直接在HTML里输入，可能会被误解，因此需要编码

所有需要编码的字符都以&开始以;结束，中间是唯一的编码。

例如我们通过`resum&eacute;`来表示 “`resumé`” 。 在头部中我们编码了短横线和长横线，在脚部，我们编码了版权标识符，想知道更多的字符集编码，查看 Copy Paste Character(http://copypastecharacter.com/)


在我们的主页有点形状之后，让我们来学习如何创建超链接，那样我们就可以添加其他页面并编辑我们网站的其他部分了。

## 创建链接
---

除了文本外，互联网一个核心组件就是超链接，它提供了链接一个网页或资源到另一个网页或资源的能力。通过行内元素锚点`<a>`可以创建超链接，要从一个页面链接到另外一个页面，需要用到`href`，也就是`hyperlink reference`，其值表示链接目标。

如下，点击文本Shay，会跳转到http://shayhowe.com 网站:

```html
<a href="http://shayhowe.com">Shay</a>
```

> 使用锚元素包含块状元素
> 默认情况下，锚元素`<a>`是一行内元素，而行内元素是不可以包裹块状元素的。 然而根据HTML5介绍， 锚元素比较特殊，可以包裹块、行内或其他级别的元素。虽然打破了标准，但我们可以是页面中的一个块作为链接。

### 相对路径与绝对路径
最常见的两种链接类型是链接到统一网站的其他页面和链接到其他网站。将通过href属性值表示这些链接，也成为路径。

链接到相同网站的其他页面可以使用相对路径，也就是在href属性值中不包括域(`.com`, `.org`, `.edu` 等)，由于链接指向同一网站的其他页面，href属性值仅需要包含链接页面的文件名称例如about.html

对于位于不同文件夹的文件，其链接需要相应的调整，假设`about.html`文件位于Pages文件夹下，那么相对路径就是 `pages/about.html` 链接到其他网站则需要绝对路径，也就是href属性值需要包含全域名，假设链接到Google主页，其属性值是http://google.com

如下的代码分布展示了如何使用相对路径和绝对路径

```html
<!-- Relative Path -->
<a href="about.html">About</a>

<!-- Absolute Path -->
<a href="http://www.google.com/">Google</a>
```

### 链接到Email地址
会打开本地的Email客户端，不仅仅可以包含邮件地址，还可以包括邮件主题和正文内容。
创建Email链接的方法（https://yoast.com/dev-blog/guide-mailto-links/） 也就是href属性值为`mailto:hexcola@google.com` 如果还需要主题和正文内容，可以如下：
mailto:hexcola@google.com?subject=Reaching%20Out&body=How%20are%20you

### 打开新的窗口
默认情况下会在当前浏览器窗口打开新页面，想在新页面中打开，可以使用target属性，例如：
```html
<a href="http://shayhowe.com/" target="_blank">Shay Howe</a>
```

### 链接到页面的不同部分
常见的是，回到页面顶部等，先通过id来设置要回到的位置，然后在href属性值中指定，例如：
```html
<body id="top">
  ...
  <a href="#top">Back to top</a>
  ...
</body>
```


## 实践
---
是时候该将`Style Conference`从单页网站进化成多页网站了，所有的网页将会通过超链接链接起来。

1.  首先将`<header>`中的`Style Conference`元素链接到`index.html`页面，虽然我们在`index.html`页面中做这样的链接显得很多余，但是`header`会被复制到其他页面，在其他页面链接回来就显得很有意义。

```html
<h1>
  <a href="index.html">Styles Conference</a>
</h1>
```

2.  为了实现导航到各个不同的页面，我们需要添加导航菜单，在`<header>`元素中使用`<nav>` 元素。

```html
<header>

  ...

  <nav>
    <a href="index.html">Home</a>
    <a href="speakers.html">Speakers</a>
    <a href="schedule.html">Schedule</a>
    <a href="venue.html">Venue</a>
    <a href="register.html">Register</a>
  </nav>

</header>
```

3.  同时也将导航菜单添加到`Footer`

```html
<footer>

  ...

  <nav>
    <a href="index.html">Home</a>
    <a href="speakers.html">Speakers</a>
    <a href="schedule.html">Schedule</a>
    <a href="venue.html">Venue</a>
    <a href="register.html">Register</a>
  </nav>

</footer>
```

4.  在介绍会议的`<section>`元素中，我们需要添加一个链接到注册会议的链接。

```html
<section>

  ...

  <a href="register.html">Register Now</a>

</section>
```

5.  同时也不要忘了We can’t forget to add links to all of the sections teasing our other pages. Inside each section, let’s wrap both the `<h3>` and `<h5>` elements within an anchor element linking to the proper page. We’ll want to make sure we do this for every section accordingly.

```html
<section>

  <section>
    <a href="speakers.html">
      <h5>Speakers</h5>
      <h3>World-Class Speakers</h3>
    </a>
    <p>Joining us from all around the world are over twenty fantastic speakers, here to share their stories.</p>
  </section>

  ...

</section>
```

6.  现在我们需要创建几个页面，`speaker.html`, `schedule.html`, `venue.html`, `register.html`，这些文件和`index.html`处于同一个目录，为了确保我们的页面看起来一致，需要保证所有页面的结构相同以及和`index.html`页面相同的`<header>`和`<footer>`元素


Fig 2
Our home page after all of the different links and navigation have been added


## Demo和源码
* [Demo](http://learn.shayhowe.com/practice/getting-to-know-html/index.html)
* [源码](http://learn.shayhowe.com/practice/getting-to-know-html.zip)


## 总结
在本节内容所讨论的语意，对HTML的结构和意义至关重要。在之后我们会介绍新的元素，它们都有各自的语意，这些元素的意义给我们的内容提供了很多意义。

* 本节内容包含了如下：
* 什么是语意以及为什么很重要
* <div>和<span> 块状元素和行内元素的区别
* 什么文本的元素最适合表示元素内容
* HTML5结构化元素以及如何定义结构和组织页面内容
* 如何使用超链接

还需要学习很多内容，下一节我们讨论一下CSS

## 资源和链接
* [Semantic code: What? Why? How?](http://boagworld.com/dev/semantic-code-what-why-how/)via Boagworld
* [The i, b, em, & strong elements](http://html5doctor.com/i-b-em-strong-element/) via HTML5 Doctor
* [New Structural Elements in HTML5](http://dev.opera.com/articles/new-structural-elements-in-html5/)via Dev.Opera
* [The Full mailto Link Syntax](https://yoast.com/guide-mailto-links/) via Joost de Valk

## 课程链接
* [课程01：创建第一个网页](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_01_Building_Your_First_Web_Page.md)
* [课程03：了解CSS](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_03_Getting_to_Know_CSS.md)
