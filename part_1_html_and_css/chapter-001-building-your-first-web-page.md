title: 课程01：创建你的第一个网页
date: 2016-04-08 00:00:12
tags: [html,css]
categories: HTML And CSS
---

在互联网发明之前，网站是不存在的，书籍，印在纸上的文件是我们的主要信息源头，It took a considerable amount of effort—and reading—to track down the exact piece of information you were after.

如今你可以打开浏览器，选择你常用的搜索引擎来搜索信息，任何可以想象到的信息在指尖下。And chances are someone somewhere has built a website with your exact search in mind.

本书将向你介绍如何使用两大主流计算机语言HTML和CSS来建立你自己的网站。

在开始我们如何使用HTML和CSS来建立网站之前，明白两种语言的语法、术语之间的区别是非常重要的。

<!-- more -->

## HTML和CSS是什么？

HTML HyperText Markup Language gives content structure and meaning by defining that content as, for example, headings, paragraphs, or images. 通过如标题、段落、图像等方式定义内容来赋予给定内容的结构和含义。

CSS 或者 Cascading Style Sheets 用来表示内容外观的展示语言，如字体、颜色等等。

HTML和CSS这两种语言应该是相互独立的。HTML内不应该出现CSS语言，反之亦然。规则是：HTML用于展示内容，CSS用于展示内容的外观。

在了解HTML和CSS的区别后，我们更深入的了解HTML

## 了解常见的HTML术语

开始学习HTML你会遇到一些新的也挺奇怪的——术语。随着时间你会逐渐了解更多，但有三个HTML术语在开始学习之前你就必须掌握。

### Elements
元素是用于定义页面内对象（标题、段落、图片）结构和内容的标识符，有常用的 多层级的标题元素（通过`<h1>` 到 `<h6>`标识）、段落元素（通过`<p>`），当然还包括`<a>` `<div>` `<strong>` `<em>`元素等等

元素通过小于号和大于号表示中间是元素名称，因此一个元素看起来如下：
`<a>`

### Tags
The use of less-than and greater-than angle brackets surrounding an element creates what is known as a tag. Tags most commonly occur in pairs of opening and closing tags.

一个开口标签表示元素的开始， It consists of a less-than sign followed by an element’s name, and then ends with a greater-than sign; for example, <div>.
一个闭合标签表示元素的结束，It consists of a less-than sign followed by a forward slash and the element’s name, and then ends with a greater-than sign; for example, </div>.

在开口标签和闭合标签中的内容称为元素内容，例如一个超链接，会有一个开口标签`<a>` 和一个闭合标签`</a>`，它们中间的内容是超链接的内容。那么超链接的标签看起来如下：
```html
<a>...</a>
```

### Attributes
Attributes are properties used to provide additional information about an element. （Attributes和 properties的区别http://jquery-howto.blogspot.com/2011/06/html-difference-between-attribute-and.html， 简而言之， attributes 值是固定的HTML属性值， properties是DOM中可以修改的属性值）常见的属性有id属性用来标识当前的元素，class属性用来对元素分组，src属性为嵌入的元素指定源文件，href 属性提供了超链接。

Attributes在开口标签中定义，放在元素名称的后面，一般属性包括属性名称和值，这些舒心的格式是通过一个属性名称 + 等于号 + 括号括起来的值。例如`<a>` 元素包含了一个href属性看起来如下：
```html
<a href="http://shayhowe.com/">Shay Howe</a>
```

上述代码会在网页上显示Shay Home的文本，当用户点击文本的时候会跳转到 XX 链接。锚元素是通过一个开口标签<a> 和一个闭合标签</a> 包含了文本，并且超链接属性 The anchor element is declared with the opening `<a>` and closing `</a>`tags encompassing the text, and the hyperlink reference attribute and value are declared with href="http://shayhowe.com" in the opening tag.

![HTML术语](https://raw.githubusercontent.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/master/Fundamentals/images/Fig01.01.png)

图1.01 HTML syntax outline including an element, attribute, and tag

现在你已经知道了HTML elements, tags, 和 attributes是什么了，let’s take a look at putting together our first web page. 如果看起来都是新的，不要担心，我们会一步一步解析。

## 设置HTML文档结构

HTML文档就是纯文本文件保存为.html文件而不是.txt文件后缀。 开始写HTML，你首先需要一个你熟悉使用纯文本编辑器，不幸的是，不包括Microsoft Word或Pages那些富文本编辑器。 有两个比较流行的用来写HTML和CSS的纯文本编辑器是Dreamweaver和Sublime Text。 其他类似的编辑器如Windows上的Notepad++ 和Mac上的TextWrangler都是可以的。

所有的HTML文档都有要气的结构，包含如下的定义和元素：
`<!DOCTYPE html>` `<html>` `<head>` `<body>`
文档类型声明或者 `<!DOCTYPE html>` 告诉Web浏览器当前使用的是哪个版本的HTML，它必须放在HTML的最顶端。 因为我们将使用最新的版本的HTML，我们的文档类型声明简单就是`<!DOCTYPE html>` 在文档类型声明之后就是`<html>`元素用来表示文档开始。

在`<html>`元素内部，`<head>`元素表示文档的顶部，包括一些元数据（metadata， 附带页面的相关信息） `<head>`元素内部的内容并不直接显示在网页上，它会包含文档的标题（会现实在浏览器窗口的标题栏上），外部文件的链接，或者其他的有用元数据。

网页里所有可见的内容都会在`<body>`元素内， 一个典型的HTML文件结构看起来如下：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Hello World</title>
  </head>
  <body>
    <h1>Hello World</h1>
    <p>This is a web page.</p>
  </body>
</html>
```

以上的代码展示了文档由文档类型 `<!DOCTYPE html>` 声明开始，接下来紧跟 `<html>` 元素，在 `<html>` 元素中包含了`<head>` 和 `<body>` 元素。`<head>` 元素包含了通过 `<meta charset=”utf-8”>` 标签指定了字符集编码已经 `<title>` 指定了文档的标题。`<body>` 元素包含了通过 `<h1>` 元素指定的标题以及通过 `<p>` 指定的段落。因为标题和段落嵌套在 `<body>`元素中，那么他们在网页中都是可见的。

当一个元素方到另外一个元素内部，也称为嵌套，用原来表示文档结构组织和结构清晰When an element is placed inside of another element, also known as nested, it is a good idea to indent that element to keep the document structure well organized and legible.
在上面的代码中，`<head>` 和 `<body>` 标签嵌套并缩进在 `<html>` 元素里。In the previous code, both the `<head>` and `<body>` elements were nested—and indented—inside the `<html>` element. The pattern of indenting for elements continues as new elements are added inside the `<head>` and `<body>` elements.

> 自闭合元素
>
> 在之前的示例中，<meta>元素只有一个标签，没有闭合标签，不要担心，这是故意的。不是所有的元素都包含开口元素和闭合元素，Some elements simply receive their content or behavior from attributes within a single tag. The <meta> element is one of these elements. The content of the previous <meta> element is assigned with the use of the charset attribute and value. Other common selfclosing elements include

* `<br>`
* `<embed>`
* `<hr>`
* `<img>`
* `<input>`
* `<link>`
* `<meta>`
* `<param>`
* `<source>`
* `<wbr>`

上面展示的结构，使用了 `<!DOCTYPE hmtl>` 作为文档类型并且使用了 `<html>` `<head>` 和 `<body>` 元素，很常见，

> 代码验证
> 在写代码的时候不管我们多么小心，我们都会犯错误，幸运的是，当我们写HTML和CSS的时候我们有验证程序来检测我们的代码。The W3C has built both HTML and CSS validators that will scan code for mistakes. Validating our code not only helps it render properly across all browsers, but also helps teach us the best practices for writing code.

## 实践
---
作为一个Web设计人员和前端开发人员we have the luxury of attending a number of great conferences dedicated to our craft. 我们将组织一个我们自己的会议， 样式会议，并建立为之一个网站。开始吧！

1.	打开我们的文本编辑器，创一个新的文件命名为index.html， 保存到一个我们不会忘记的地方。我将在我的桌面创建一个文件夹命名为”style-conference” 用来保存该文件。
2.	在index.html文件中，我们在其中添加文档结构，包括<!DOCTYPE html>文件类型和 `<html>` `<head>` 和 `<body>` 元素

```html
<!DOCTYPE html>
<html lang="en">
  <head>
  </head>
  <body>
  </body>
</html>
```

3.	在 `<head>` 元素中，我们添加 `<meta>` 和 `<title>` 元素，`<meta>` 元素应该包括恰当的 `charset` 属性和值，`<title>` 元素应该包含网页的标题，我们这里命名为 **Style Conference**

```html
<head>
  <meta charset="utf-8">
  <title>Styles Conference</title>
</head>
```
4.	在 `<body>` 元素中，我们添加 `<h1>` 和 `<p>` 元素，`<h1>` 元素应该包含我们希望包含的标题，我们还使用 “Styles Conference”，使用 `<p>`元素包含一个简单的段落用于介绍我们的会议。

```html
<body>
  <h1>Styles Conference</h1>
  <p>Every year the brightest web designers and front-end developers descend on Chicago to discuss the latest technologies. Join us this August!</p>
</body>
```

5.	先在看看我们做的怎么样！找到我们的index.html文件，用浏览器打开该文件。
![index.html](https://raw.githubusercontent.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/master/Fundamentals/images/Fig01.02.png)

图1.02 Our first steps into building our Styles Conference website

现在我们切换一下我们的装备，看看CSS，记住：HTML定义网页的内容和结构，CSS用来定义网页的视觉风格和外观。

## 了解常见的CSS术语

除了HTML术语外，有几个常见的CSS术语你需要熟悉。这些术语包括选择器(selectors)， 属性(properties) 和值(values)，和HTML中的术语一样，使用CSS越多，你会对这些术语越熟悉。

### 选择器Selectors
一个添加到网页的元素可以通过CSS来改变样式，
As elements are added to a web page, they may be styled using CSS. A selector designates exactly which element or elements within our HTML to target and apply styles (such as color, size, and position) to. Selectors may include a combination of different qualifiers to select unique elements, all depending on how specific we wish to be. For example, we may want to select every paragraph on a page, or we may want to select only one specific paragraph on a page.
例如，我们想选择网页中的每一个段落，或者我们想选择页面中的某一个段落。

选择器一般指向一个属性值，比如id或class的值，或者指向元素的类型，比如 `<h1>` ， `<p>` 等

在CSS中，选择器后面跟的是花括号 `{}`， 其中包括的样式会被应用到所选择的元素。如下的选择器针对所有的 `<p>` 元素。

```css
p { ... }
```

### 属性 Properties
一旦选择一个元素后，属性决定了什么样的样式会运用到该元素。 属性名称在选择器之后，花括号内部，冒号之前，有许多属性我们可以使用，比如background, color, font-size, height已经width等等，此外新的属性不断增加。 在如下的代码中，我们定义了 `<p>` 元素内的color和font-size属性

``` css
p {
  color: ...;
  font-size: ...;
}
```

### 值 Values
现在我们已经通过一个选择器选择了一个元素，并通过属性来确定我们将应用什么样式。 现在我们可以通过值来确定属性的行为了。 值可以通过文本表示，放在冒号和分号之间，以下是我们选择了所有的 `<p>` 元素，并设置了`color` 属性，值为 `orange`， `font-size`属性，值为16pixels.

``` css
p {
  color: orange;
  font-size: 16px;
}
```

回顾一下，在CSS中我们的规则是，先从选择器开始，后面跟上花括号，在花括号中定义属性和值对，每个声明都通过属性开始，跟上冒号，然后是值，然后是分号
It is a common practice to indent property and value pairs within the curly brackets. As with HTML, these indentations help keep our code organized and legible.
在花括号内缩进属性和值对是常见的做法，正如HTML中，这些缩进可以显得代码有组织，并且清晰可读。

![CSS术语](https://raw.githubusercontent.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/master/Fundamentals/images/Fig01.03.png)

图 1.03 CSS语法CSS syntax outline including a selector, properties, and values

掌握了一些常见术语和CSS的通用语法是个不错的开始，但在深入之前我们还要学点更多的东西，我们需要知道CSS的选择器是怎样工作的？

## 使用Selectors
---
选择器，正如上文提到的，标识哪个HTML元素改变样式。It is important to fully understand how to use selectors and how they can be leveraged. The first step is to become familiar with the different types of selectors. We’ll start with the most common selectors: type, class, and ID selectors. 充分了解如何使用选择器以及它们可以怎样使用非常重要。 第一步是先熟悉有哪几类的选择器，我们从常见的选择器开始，它们分别是类型，分类，Id选择器

### 类型选择器 Type
类型选择器通过它们的元素类型来指向元素，例如我们想指向所有的块元素`<div>` 我们会使用div类型选择器。 如下的代码展示了一个div元素选择器已经其对应指向的HTML
CSS

```css
div { ... }
```

HTML
```html
<div>...</div>          
<div>...</div>
```

### 类选择器Class
类选择器允许我们通过HTML元素的class属性值来选择HTML元素。 由于类选择器选择一组特定的元素而不是一种类型的所有元素，类选择器比类型选择器更具有针对性。

一旦我们在多个HTML元素中使用了相同的class属性值，类选择器允许我们给不同的HTML元素运用相同的样式。

在CSS中， 类由前置的点号 . 表示后面跟上类的属性值。如下代码中的类选择器选择所有包含类属性值为awesome的所有HTML元素，包括div元素和段落元素
CSS

```css
.awesome { ... }
```

HTML

```html
<div class="awesome">...</div>
<p class="awesome">...</p>
```

### ID选择器
ID选择器比类选择器更加精准，它们只指向一个HTML元素。 和类选择器使用HTML元素的class属性值做为选择器一样，ID选择器使用元素的ID属性值作为选择器

无论是什么类型的元素，ID属性值在一个页面只能出现一次，If used they should be reserved for significant elements.

在CSS中，ID选择器由前置的# 跟上ID属性值。如下代码中的ID选择器只会选择ID属性值为shayhowe的HTML元素

CSS

```css
#shayhowe { ... }
```

HTML
```html
<div id="shayhowe">...</div>
```

### 其他选择器
选择器是非常强大的，上面所示的选择器是我们常用到的。这些选择器也仅仅是开始。此外有许多更高级的选择器（http://learn.shayhowe.com/advanced-html-css/complex-selectors/）当你对以上的选择器使用自如了，可以尝试看看这些高级的选择器。


## 引用CSS
---
为了能使我们的CSS和HTML能交流，我们需要在HTML文件中引用CSS文件。 引用CSS最好的方式是将我们所有的样式放到一个外部的样式表中，The best practice for referencing our CSS is to include all of our styles in a single external style sheet, which is referenced from within the `<head>` element of our HTML document.  使用一个外部的样式表可以让我们在整个网站中使用并高效修改

> 添加CSS的其他方式
>
> Other options for referencing CSS include using internal and inline styles. You may come across these options in the wild, but they are generally frowned upon, as they make updating websites cumbersome and unwieldy.

创建CSS样式表，使用纯文本编辑器新建一个空白文件，保存为.css后缀， CSS文件应保存在HTML文件所在的相同目录或者子目录。
在HTML文档中的`<head>`元素中，`<link>`元素用来定义HTML文件和CSS文件之间的关系，因为我们连接到CSS，我们使用rel属性值为stylesheet来指定它们的关系，此外，href(hyperlink reference)属性用来表示CSS文件的位置或路径。Within the `<head>` element of the HTML document, the `<link>` element is used to define the relationship between the HTML file and the CSS file. Because we are linking to CSS, we use the rel attribute with a value of stylesheet to specify their relationship. Furthermore, the href (or hyperlink reference) attribute is used to identify the location, or path, of the CSS file.

如下示例：

```html
<head>
  <link rel="stylesheet" href="main.css">
</head>
```

为了能使CSS正常渲染，href属性值所表示的路径必须指定为我们保存的CSS文件。在如上的案例中，`main.css` 文件保存在和HTML相同的位置，也称为根目录

如果我们的CSS文件放在子目录，`href` 属性值需要相应变化。假设我们将文件放到一个名为 `sytlesheets` 的文件夹中，那么 `href` 的属性值就是 `stylesheets/main.css`。

现在我们嗯的页面开始慢慢的有生气了，我们还没有深入CSS太多，但你可能已经意识到尽管我们还没有定义CSS，一些HTML元素已经有默认的样式。这是由于浏览器应用了其偏好的一些CSS样式，幸运的是，我们可以简单的重写这些样式，接下来我们就使用CSS重置（初始化）来实现。

##使用CSS重置
---
每个Web浏览器对于不同的HTML元素都有其默认的样式。Google Chrome浏览器和IE浏览器如恶化渲染标题、段落、列表等等也许是不同的。 为了包装不同浏览器之间的兼容，CSS重置就广为使用。

CSS重置将每个HTML元素赋予预设的样式，并为所有的浏览器设置为统一的。 这些重置一般包括移除任何sizing, margins, paddings或其他样式并调整这些值。 由于CSS样式自上而下解析，我们的重置文件必须放到样式表的最上方。Doing so ensures that those styles are read first and that all of the different web browsers are working from a common baseline.这样做可以确保所有的样式被先读取，然后所有的Web浏览器的起点都相同。

我们有很多的重置方案以供选择，它们各有所长，最广为使用的是 Eric Meyer’s rest （http://meyerweb.com/eric/tools/css/reset/） which has been adapted to include styles for the new HTML5 elements. 可以适用HTML5元素。

如果你喜欢探索，还有Nicolas Gallagher创建的Normaize.css（http://necolas.github.io/normalize.css/）  Normalize.css focuses not on using a hard reset for all common elements, but instead on setting common styles for these elements. It requires a stronger understanding of CSS, as well as awareness of what you’d like your styles to be.

> 跨浏览器兼容和测试
> 正如之前所提到的，不同的浏览器以不同的方式来渲染HTML元素， 虽然不要求网站在所有的浏览器中看起来完全一样，但至少得非常接近，
>
> As previously mentioned, different browsers render elements in different ways. It’s important to recognize the value in cross-browser compatibility and testing. Websites don’t need to look exactly the same in every browser, but they should be close. Which browsers you wish to support, and to what degree, is a decision you will need to make based on what is best for your website.
In all there are a handful of（少量的） things to be on the lookout for when writing CSS. The good news is that anything is possible, and with a little patience we’ll figure it all out.

## 实践
---
回到我们的conference website，看看我们是否可以添加一点CSS
1.	在styles-conference文件夹中，我们创建一个文件夹名称为assets，用来保存网站所有的文件，比如样式表，图片，视频等等，在该文件夹中，对于我们的样式表，我们再添加一个文件夹，命名stylesheets
2.	使用纯文本编辑器创建一个main.css文件保存到stylesheets文件夹中
3.	在浏览器中打开我们的index.html，我们可以看到 `<h1>` 和 `<p>` 元素都有默认的CSS样式，具体来说，它们有不同的字体大小和间距。 使用Eric Meyer的重置，我们可以调节这些样式，让其处于同一个起点。去Eric的网站复制其重置，粘贴到我们的main.css文件的顶部。

```css
/* http://meyerweb.com/eric/tools/css/reset/ 2. v2.0 | 20110126
  License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed,
figure, figcaption, footer, header, hgroup,
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure,
footer, header, hgroup, menu, nav, section {
  display: block;
}
body {
  line-height: 1;
}
ol, ul {
  list-style: none;
}
blockquote, q {
  quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
  content: '';
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
```

4.	随着我们往CSS文件中添加内容，让我们把它和index.html文件连接起来，打开index.html文件，在<head>元素中，`<title>` 元素后添加 `<link>` 元素。
5.	因为我们将在 `<link>` 元素汇总引用样式表，那么来添加一个关系属性，`rel` 指定值为 `stylesheet`
6.	我们还需要包含一个超链接引用，使用 `href` 属性，连接到 `main.css` 文件，记住，我们的 `main.css` 文件保存在 `assets` 文件夹下的 `stylesheets` 文件夹。因此 `href` 属性值为 `assets/stylesheets/main.css`

```html
<head>
  <meta charset="utf-8">
  <title>Styles Conference</title>
  <link rel="stylesheet" href="assets/stylesheets/main.css">
</head>
```

该看看我们的成果了，在浏览器中打开index.html文件。

![CSS重置效果](https://raw.githubusercontent.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/master/Fundamentals/images/Fig01.04.png)

图 1.04 Our Styles Conference website with a CSS reset

## Demo和源代码

下面的连接你可以查看Style Conference网站的当前状态，也可以下载当前状态的源代码
* [Demo](http://learn.shayhowe.com/practice/building-your-first-web-page/index.html)
* [源代码](http://learn.shayhowe.com/practice/building-your-first-web-page.zip)

## 总结

目前来说，不错！在本课中我们已经走了很大一步了。
回头看看，你已经知道了HTML和CSS的基础，通过继续努力，你花些时间来写HTML和CSSS，你将会更加熟悉两门语言。

总结一下，目前我们所覆盖的内容：
*	HTML和CSS的区别
*	熟悉HTML元素、标签和属性
*	设置网页结构
*	熟悉CSS选择器、属性和值
*	使用CSS选择器
*	在HTML中引用CSS
*	CSS重置

现在我们更加详细的了解下HTML并学点语意方面的知识。

## 资源与链接
---
* [Common HTML terms](http://www.scriptingmaster.com/html/HTML-terms-glossary.asp) via Scripting Master
* [CSS Terms & Definitions](http://www.impressivewebs.com/css-terms-definitions/) via Impressive Webs
* [CSS Tools: Reset CSS](http://meyerweb.com/eric/tools/css/reset/) via Eric Meyer
* [Normalize.css](http://necolas.github.io/normalize.css/) via Nicolas Gallagher
* [An Intro to HTML & CSS](http://www.shayhowe.com/web-design/intro-to-html-css/) via Shay Howe

## 课程链接

* [课程02：了解HTML](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_02_Getting_to_Know_HTML.md)
