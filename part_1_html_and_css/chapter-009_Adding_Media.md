title:  课程09：添加多媒体
date: 2016-04-08 00:00:04
tags: [html,css]
categories: HTML And CSS
---

## 概述

如果网页都是纯文本，那多单调，HTML提供了一系列嵌入多媒体文件的方法，包括图片，音轨，视频，以及如何嵌套其他网页等等。

* 添加图片
* 添加音频
* 添加视频
* 添加嵌入式框架
* Figures & Captions

<!--more -->
## 添加图片
---
我们使用行内元素`<img>`用来添加图片，必须设置它的`src`和`alt`(alternative text)属性。
* `src`属性是用于指定图片位置
* `alt`属性用于描述图片内容，它由搜索引擎查找， 且当图片找不到时，属性值的文本就会显示。  The alt attribute value is picked up by search engines and assistive technologies to help convey the purpose of an image.

```html
<img src="dog.jpg" alt="A black, brown, and white dog wearing a kerchief">
```

![](Fig 09.01.png)
Fig 9
The alternate text, “A black, brown, and white dog wearing a kerchief,” shown in place of a missing image

> 支持的图片格式
> 图片有很多种格式，且不同的浏览器有支持和不支持的图片格式。大部分浏览器都支持`gif`, `jpg`，`png`图片，使用得比较广泛的格式是`jpg` 和`png` The jpg format provides quality images with high color counts while maintaining a decent file size, ideal for faster load times. The png format is great for images with transparencies or low color counts.
通常我们们会将jpg图片用于照片，png图片用于图标或背景。


### 修改图片尺寸
在网页加载之前，就必须告诉浏览器图片的尺寸。这样浏览器就可以为图片保留空间同时加快渲染速度。有好几种方式来设置图片的尺寸。一种是直接使用用`<img>` 元素的`width` 和`height`属性。 也可以使用CSS样式中的`width` 和`height` 属性， 当两个同时使用得时候，CSS会优先使用。

单独设置图片的宽高，图片会根据宽高比例相应缩放。当然也可以同时设置宽高，只不过有时会使图片拉伸。

```css
img {
  height: 200px;
  width: 200px;
}
```
尽管在HTML中直接使用`width` 和`height`属性为图片的默认尺寸提供了语义价值，但用于管理多个相同尺寸的图片就很困难。这这样的情况下，比较常见的是使用CSS来设置图片的大小。

### 图片定位
我们有很多种方式来设置图片的位置，默认情况下图片元素是行内元素，但我们可以通过CSS指定为`float`或`display`的值以及盒模型的一些属性，包括`padding` `border` `margin`。

#### 行内图片定位
默认情况下`<img>` 元素是行内元素，不使用样式的话，文本会直接包围图片，且当前的行高会和图片的高度一样，这就导致了行和行之间产生了间距。

```html
<p>Gatsby is a black, brown, and white hound mix puppy who loves howling at fire trucks and collecting belly rubs. <img src="dog.jpg" alt="A black, brown, and white dog wearing a kerchief"> Although he spends most of his time sleeping he is also quick to chase any birds who enter his vision.</p>
```

直接插入图片不修改样式的情况比较少。更多的情况是图片作为块元素显示，或者浮动到网页的一侧。

#### 块图片定位
在CSS中设置`display`属性值为`block`会强制将图片元素修改为块元素，这样就会占据新的一行。

```css
img {
  display: block;
}
```

#### 图片左对齐或右对齐
大多数情况下，图片以`inline` `block` 或者`inline-block`的方式显示都不太理想。我们更多希望的是图片元素居于其父元素的左侧或者右侧，其他所有元素围绕着它。我们可以通过`float`属性设置为`left`或`right`实现。

还记得我们在第5课里所提到的，`float`属性的最初目标就是用于设置图片左对齐还是右对齐的，现在我们就将它用于原始目标。

浮动元素只是开始，因为这样其他内容会直接和它接触，为了给图片周围流出空白，我们需要使用margin属性，此外我们也可以使用padding， border 和 background属性等等。

```css
img {
  background: #eaeaed;
  border: 1px solid #9799a7;
  float: right;
  margin: 8px 0 0 20px;
  padding: 4px;
}
```

> 什么使用使用图片元素？什么时候使用背景图片？
> 有两种方法向图片中添加图片，一种是本课所提到的使用`<img>` 元素，另外一种就是在上一节课中所提到的使用`background` 或`background-image`属性，两种情况都可以，但事实上它们有各自的应用场景。
> `<img>`往往用于承载语义以及和网页的内容相关。
> `<background>` 或`<background-image>` 往往倾向于将图片用于设计或网页的用户界面，而且和网页的内容无关。

## 实践
---
Now that we know how to add and position images on a page, let’s take a look at our Styles Conference website and see where we can add a few images.

1. Let’s begin by adding some images to our home page. Specifically, we’ll add an image within each of the teaser sections promoting a few of our pages.

Before we jump into the code, though, let’s create a new folder named “images” within our “assets” folder. Then, within the “images” folder, let’s create another folder named “home” specifically for our home page images. Within the “home” folder we’ll add three images: speakers.jpg, schedule.jpg, and venue.jpg. (For reference, these images may be downloaded within a zip file.)

Then, inside our index.html file, each teaser section has an <a> element wrapping both an <h3> and an <h5> element. Let’s move the <h5> element above the <a> element and replace it with an <img> element. The src attribute value for each <img> element will correspond to the folder structure and filename we set up, and the alt attribute value will describe the contents of each image.

The HTML for our first teaser, for the Speakers page, will look like this:
```html
<section class="teaser col-1-3">
  <h5>Speakers</h5>
  <a href="speakers.html">
    <img src="assets/images/home/speakers.jpg" alt="Professional Speaker">
    <h3>World-Class Speakers</h3>
  </a>
  <p>Joining us from all around the world are over twenty fantastic speakers, here to share their stories.</p>
</section>
```
Let’s continue this pattern for both the Schedule and Venue page teasers, too.

2. Now that we’ve added a few images to our home page, we’ll need to clean up their styles a bit and make sure they properly fit into the layout of our page.

Since images are inline-level elements by default, let’s change our images within the teaser sections to block-level elements. Let’s also set their maximum width to 100% to ensure they don’t exceed the width of their respective columns. Changing this width value is important as it allows our images to adjust with the width of the columns as necessary.

Lastly, let’s round the corners of the images slightly and apply 22 pixels of bottom margin to the images, providing a little breathing room.

Once we add these new styles to our existing home page styles (using the teaser class as a qualifying selector for the <img> elements), our CSS will look like this:

```css
.teaser img {
  border-radius: 5px;
  display: block;
  margin-bottom: 22px;
  max-width: 100%
}
```
3. Next up, let’s add images of all of the speakers to the Speakers page. We’ll begin by creating a “speakers” folder within our “images” folder and placing images of all of the speakers there.

Within the speakers.html file, let’s add an <img> element within each of the speaker information <aside> elements. Let’s place each <img> element inside the <div> element with the class attribute value of speaker-info, just above the <ul> element.

The src attribute value of each image will correspond to the “speakers” folder we set up and the speaker’s name; the alt attribute value will be the speaker’s name.

The <aside> element for myself, as a speaker, will look like this:
```html
<aside class="col-1-3">
  <div class="speaker-info">

    <img src="assets/images/speakers/shay-howe.jpg" alt="Shay Howe">

    <ul>
      <li><a href="https://twitter.com/shayhowe">@shayhowe</a></li>
      <li><a href="http://learn.shayhowe.com/">learn.shayhowe.com</a></li>
    </ul>

  </div>
</aside>
```
This same pattern for adding an image should then be applied to all other speakers.
4. As we did with the images on our home page, we’ll want to apply some styles to the images on the Speakers page.

Let’s begin by applying the border-radius property with a value of 50%, turning our images into circles. From there, let’s set a fixed height of 130 pixels to each image and set them to be vertically aligned to the top of the line they reside within.

With the height and vertical alignment in place, let’s apply vertical margins to the images. Using a negative 66-pixel margin on the top of the images, we’ll pull them slightly out of the <aside> element and make them vertically centered with the top border of the <div> element with a class attribute value of speaker-info. Then, applying a 22-pixel margin on the bottom of the image provides space between the image and the <ul> element below it.

When we add these new styles to our existing Speakers page styles (using the speaker-info class as a qualifying selector for the <img> elements), our CSS will look like this:

```css
.speaker-info img {
  border-radius: 50%;
  height: 130px;
  margin: -66px 0 22px 0;
  vertical-align: top;
}
```

5. Since we are using an aggressive negative margin on the <img> element within the <div> element with a class attribute value of speaker-info, we need to remove the padding on the top of that <div> element.

Previously we were using the padding property with a value of 22px 0, thus placing 22 pixels of padding on the top and bottom and 0 pixels of padding on the left and right of the <div> element. Let’s swap this property and value out for the padding-bottom property, as that’s the only padding we need to identify, and use a value of 22 pixels.

The new speaker-info class rule set looks like this:

```css
.speaker-info {
  border: 1px solid #dfe2e5;
  border-radius: 5px;
  margin-top: 88px;
  padding-bottom: 22px;
  text-align: center;
}
```
Now both our home and Speaker pages are looking pretty sharp.
![](Fig09.02.png)
Fig 9
Our Styles Conference home page after adding images to each section that teases another page

![](Fig09.03.png)

## 添加音频
---
HTML5通过`<audio>`[元素](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio)提供了快速而简单方法用于给网站添加[音频文件](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_HTML5_audio_and_video)，和`<img>`元素一样，也通过`src`属性来指定文件资源，不同于`<img>`元素，`<audio>`元素需要开口和闭口标签，我们会在接下来讨论。

```html
<audio src="jazz.ogg"></audio>
```

### 音频属性
除了`src`元素外，常用的属性还包括`autoplay`， `controls`， `loop`，以及`preload`。
`autoplay`， `controls`，`loop`属性都是布尔属性，作为布尔值，它们不需要状态值，当且仅当它们出现于`<audio>`元素中的时候，就会设置为`true`，`<audio>`元素会更加值进行设置。

默认情况下`<audio>` 元素不在页面显示，如果`autoplay`属性出现在`<audio>`元素中，页面中将什么都不会出现，但音频文件会在页面加载时自动播放。

```html
<audio src="jazz.ogg" autoplay></audio>
```
如果要想在页面中显示`<audio>`元素，`controls`布尔值是必须的。

```html
<audio src="jazz.ogg" controls></audio>
```

当展示`<audio>`元素时，`loop`布尔属性会让音频循环播放。

最后，关于`preload`属性，它用于表示该音频文件信息是否在音频播放之前加载，它接收三个值`none` `auto`和`metadata`。
* `none`将不预加载关于音频文件的任何信息。
* `auto`将加载关于音频文件的所有信息
* `metadata`处于`none`和`auto`值之间，会加载关于音频文件的元数据，包括如音频长度，但不是全部信息。

当`preload`属性未出现在`<audio>`元素中是，关于音频的所有信息都会加载，正如将其值设置为`auto`一样。当音频文件对网页内容不是很重要的时候，将`preload`属性设置为`metadata`或`none`会节省带宽并让网页加载更快。

### 备用音频以及多资源文件
目前为止，不同的浏览器支持不同的音频文件，三大主流的文件格式是`ogg` `mp3`和`wav` 为了能得到最好的支持，我们需要在`<audio>`元素中加载几个不同的备份音频文件。

要实现这样的功能，首先得从`<audio>`中移除`src`属性，取而代之的使用`<source>`元素，其中包含`src`属性。每一个文件格式使用一个设置了`src`属性值的`<source>`元素，同时在`<source>`属性使用`type`帮助浏览器识别音频的类型，当浏览器能识别一种文件格式的时候，就会忽略其他的音频。

但由于该属性是在HTML5中介绍的，一些浏览器可能不支持`<audio>`元素，在这种情况下，我们提供一个链接用于下载音频文件。
```html
<audio controls>
  <source src="jazz.ogg" type="audio/ogg">
  <source src="jazz.mp3" type="audio/mpeg">
  <source src="jazz.wav" type="audio/wav">
  Please <a href="jazz.mp3" download>download</a> the audio file.
</audio>
```

除了`<audio>`元素外，HTML5还支持`<video>`元素，它和`<audio>`元素用很多共通的属性。

## 添加视频
---
[在HTML5中添加视频](http://dev.opera.com/articles/introduction-html5-video/) 和添加音频文件非常相似。 我们也使用`src` `autoplay` `controls` `loop` `preload`属性和备用视频。

在`<audio>`元素中如果`controls`属性没有设置，音频不会显示，而在视频中，如果`controls`属性没有显示，则视频会显示。 With the <audio> element, if the controls Boolean attribute isn’t specified the audio clip isn’t displayed. With videos, if the controls Boolean attribute is not specified the video will display. However, it is fairly difficult to view unless the autoplay Boolean attribute is also applied. In general, the best practice here is to include the controls Boolean attribute unless there is a good reason not to allow users to start, stop, or replay the video.

由于视频在页面中会占据一些空间，我们往往需要在CSS中指定它的`width`和`height`属性值。 这样会保证视频不会太大，并保持在网页之中。此外，和图片一样指定尺寸后，会使浏览器渲染视频更快，且会分配恰当的空间用于输出视频。
```html
<video src="earth.ogv" controls></video>
```

> 自定义音频和视频的控制条
> 默认情况下`<audio>` `<video>`元素的控制条是由浏览器决定的，根据网站的设计，也许会有指定控制条的样式的需求。如果是这个情况，那么可以创建一个自定义的播放器，但需要些JavaScript。
> 此外，如果自定义的播放器使用了`<img>`元素作为控制器，`alt`属性值value of the alt attribute should explictly state that the image is a control and requires the proper interaction to work.

### `Poster` 属性
对于`<video>`还有另外一个属性`poster`，该属性可以通过使用URL来指定一个图片，用于一段视频的显示图。

```html
<video src="earth.ogv" controls poster="earth-video-screenshot.jpg"></video>
```

### 备用视频
和`<audio>`元素一样，备用视频也是必须的，HTML标记格式是一样的。
```html
<video controls>
  <source src="earth.ogv" type="video/ogg">
  <source src="earth.mp4" type="video/mp4">
  Please <a href="earth.mp4" download>download</a> the video.
</video>
```

还有一个备用选项是使用文本嵌入YouTube或Vimeo视频，这些视频网站允许我们上传视频，提供标准的视频播放器，并且让我们通过行内框架嵌入视频。

> HTML5 音频和视频文件格式
> 在浏览器支持`<audio>` 和`<video>`元素的同时也对文件的格式有妖气，每个浏览器都有自己[首选](https://developer.mozilla.org/en-US/docs/HTML/Supported_media_formats)的音频和视频格式。

## 添加行内框架
另外一种向网页中添加内容的方式就是嵌套其他的HTML网页内容到当前网页，可以通过`<iframe>`元素来实现。Another way to add content to a page is to embed another HTML page within the current page. This is done using an inline frame, or <iframe> element. The <iframe> element accepts the URL of another HTML page within the src attribute value; this causes the content from the embedded HTML page to be displayed on the current page. The value of the src attribute may be a URL relative to the page the <iframe> element appears on or an absolute URL for an entirely external page.

Many pages use the <iframe> element to embed media onto a page from an external website such as Google Maps, YouTube, and others.

```html
<iframe src="https://www.google.com/maps/embed?..."></iframe>
```
The <iframe> element has a few default styles, including an inset border and a width and height. These styles can be adjusted using the frameborder, width, and height HTML attributes or by using the border, width, and height CSS properties.

### 无缝行内框架
Pages referenced within the src attribute of an <iframe> element play by their own rules, as they do not inherit any styles or behaviors from the page they are referenced on. Any styles applied to a page that includes an <iframe> element will not be inherited by the page referenced within the <iframe> element. Additionally, links within the page referenced within the <iframe> element will open inside that frame, leaving the page that contains the <iframe> element unchanged.

There will be times when we’ll want to change these behaviors, and the seamless Boolean attribute will allow us to do just that. When present on the <iframe> element, the seamless Boolean attribute allows styles from the page that includes an <iframe> element to be inherited by the page referenced within the <iframe> element. Additionally, the seamless Boolean attribute allows links clicked on a page referenced within an <iframe> element to be opened within the same window as the original page that includes the <iframe> element.

```html
<iframe src="contact.html" seamless></iframe>
```
The seamless Boolean attribute is a new attribute introduced in HTML5. Although the browser support for this attribute is growing, it will not work within older browsers. It’s advisable to test the seamless Boolean attribute before using it.

## 实践
Inline frames provide a great way to add dynamic content to a page. Let’s give this a shot by updating our Venue page with some maps.
1. Before adding any maps or inline frames, let’s first prepare our Venue page for a two-column grid. Below the leading section of the page we’ll add a <section> element with the class attribute value of row to identify a new section of the page, and we’ll include some general styles, such as a white background and some vertical padding.

Directly inside this <section> element let’s add a <div> element with the class attribute value of grid. The class of grid centers our content on the page and prepares for the one-third and two-thirds columns to follow.

So far the main section of our venue.html file looks like this:
```html
<section class="row">
  <div class="grid">
    ...
  </div>
</section>
```
2. Within the <div> element with the class attribute value of grid we’ll have two new sections, one for the conference venue and one for the conference hotel. Let’s add two new <section> elements and give each of these <section> elements a unique class that corresponds to its content. We’ll use these classes to add margins to the bottom of each section.

Our HTML should now look like this:
```html
<section class="row">
  <div class="grid">

    <section class="venue-theatre">
      ...
    </section>

    <section class="venue-hotel">
      ...
    </section>

  </div>
</section>
```

3. Now that we have a few classes to work with, let’s create a new section within our main.css file for Venue page styles. We’ll add a 66-pixel margin to the bottom of the <section> element with the class attribute value of venue-theatre to insert some space between it and the <section> element below it.

Then, we’ll add a 22-pixel margin to the bottom of the <section> element with the class attribute value of venue-hotel to provide some space between it and the <footer> element below it.

The new venue section within the main.css file looks like the following:
```css
/*
  ========================================
  Venue
  ========================================
*/

.venue-theatre {
  margin-bottom: 66px;
}
.venue-hotel {
  margin-bottom: 22px;
}
```

The <section> element with the class attribute value of venue-hotel has a smaller bottom margin than the <section> element with the class attribute value of venue-theatre because it sits next to the padding from the bottom of the <section> element with the class attribute of row. Adding that margin and padding together gives us the same value as the bottom margin on the <section> element with the class attribute value of venue-theatre.

4. Now it’s time to create the two columns within each of the new <section> elements. We’ll start by adding a <div> element with a class attribute value of col-1-3 to establish a one-third column. After it we’ll add an <iframe> element with a class attribute value of col-2-3 to establish a two-thirds column.

Keeping in mind that the column classes make both the <div> and <iframe> elements inline-block elements, we need to remove the empty space that will appear between them. To do so we’ll open an HTML comment directly after the closing <div> tag, and we’ll close the HTML comment immediately before the opening <iframe> tag.

In all, our HTML for the columns looks like this:
```html
<section class="row">
  <div class="grid">

    <section class="venue-theatre">

      <div class="col-1-3"></div><!--

      --><iframe class="col-2-3"></iframe>

    </section>

    <section class="venue-hotel">

      <div class="col-1-3"></div><!--
      --><iframe class="col-2-3"></iframe>

    </section>

  </div>
</section>
```
5. Within each of the <div> elements with a class attribute value of col-1-3 let’s add the venue’s name within an <h2> element, followed by two <p> elements. In the first <p> element let’s include the venue’s address, and in the second <p> element let’s include the venue’s website (within an anchor link) and phone number.

Within each of the paragraphs, let’s use the line-break element, <br>, to place breaks within the address and in between the website and phone number.

For the <section> element with the class attribute value of venue-theatre, the HTML looks like this:
```html
<section class="venue-theatre">

  <div class="col-1-3">
    <h2>Chicago Theatre</h2>
    <p>175 N State St <br> Chicago, IL 60601</p>
    <p><a href="http://www.thechicagotheatre.com/">thechicagotheatre.com</a> <br> (312) 462-6300</p>
  </div><!--

  --><iframe class="col-2-3"></iframe>

</section>
```
The same pattern shown here for the theatre should also be applied to the hotel (using, of course, the proper address, website, and phone number).

We can search for these addresses in Google Maps. Once we locate an address
6. We can search for these addresses in Google Maps. Once we locate an address and create a customized map, we have the ability to embed that map into our page. Following the instructions on Google Maps for how to share and embed a map will provide us with the HTML for an <iframe> element.

Let’s copy the HTML—<iframe> element, src attribute, and all—onto our page where our existing <iframe> element resides. We’ll do this for each location, using two different <iframe> elements.

In copying over the <iframe> element from Google Maps we need to make sure we preserve the class attribute and value, col-2-3, from our existing <iframe> element. We also need to be careful not to harm the HTML comment that closes directly before our opening <iframe> tag.

Looking directly at the <section> element with the class attribute value of venue-theatre again, the HTML looks like this:
```html
<section class="venue-theatre">

  <div class="col-1-3">
    <h2>Chicago Theatre</h2>
    <p>175 N State St <br> Chicago, IL 60601</p>
    <p><a href="http://www.thechicagotheatre.com/">thechicagotheatre.com</a> <br> (312) 462-6300</p>
  </div><!--

  --><iframe class="col-2-3" src="https://www.google.com/maps/embed?pb=!1m5!3m3!1m2!1s0x880e2ca55810a493%3A0x4700ddf60fcbfad6!2schicago+theatre!5e0!3m2!1sen!2sus!4v1388701393606"></iframe>

</section>
```

7. Lastly, we’ll want to make sure that both <iframe> elements that reference Google Maps share the same height. To do this, we’ll create a new class, venue-map, and apply it to each of the <iframe> elements alongside the existing col-2-3 class attribute value.

The HTML for the <section> element with the class attribute value of venue-theatre now looks like this:
```html
<section class="venue-theatre">

  <div class="col-1-3">
    <h2>Chicago Theatre</h2>
    <p>175 N State St <br> Chicago, IL 60601</p>
    <p><a href="http://www.thechicagotheatre.com/">thechicagotheatre.com</a> <br> (312) 462-6300</p>
  </div><!--

  --><iframe class="venue-map col-2-3" src="https://www.google.com/maps/embed?pb=!1m5!3m3!1m2!1s0x880e2ca55810a493%3A0x4700ddf60fcbfad6!2schicago+theatre!5e0!3m2!1sen!2sus!4v1388701393606"></iframe>

</section>
```
Once the venue-map class is applied to each <iframe> element, let’s create the venue-map class rule set within our main.css file. It includes the height property with a value of 264 pixels.

The venue-map class rule set looks like this:
```css
.venue-map {
  height: 264px;
}
```
We now have a Venue page, complete with maps for the different locations of our conference.
![](Fig09.04.png)
Fig 9
Our Styles Conference Venue page, which now includes inline frames

## Demo和源码
* [Demo](http://learn.shayhowe.com/practice/adding-media/index.html)
* [源码](http://learn.shayhowe.com/practice/adding-media.zip)


## Semantically Identifying Figures & Captions
With HTML5 also came the introduction of the <figure> and <figcaption> elements. These elements were created to semantically mark up self-contained content or media, commonly with a caption. Before HTML5 this was frequently done using an ordered list. While an ordered list worked, the markup was not semantically correct.

### Figure
The <figure> block-level element is used to identify and wrap self-contained content, often in the form of media. It may surround images, audio clips, videos, blocks of code, diagrams, illustrations, or other self-contained media. More than one item of self-contained content, such as multiple images or videos, may be contained within the <figure> element at a time. If the <figure> element is moved from the main portion of a page to another location (for example, the bottom of the page), it should not disrupt the content or legibility of the page.

```html
<figure>
  <img src="dog.jpg" alt="A black, brown, and white dog wearing a kerchief">
</figure>
```

### Figure Caption
To add a caption or legend to the <figure> element, the <figcaption> element is used. The <figcaption> may appear at the top of, bottom of, or anywhere within the <figure> element; however, it may only appear once. When it’s used, the <figcaption> element will serve as the caption for all content within the <figure> element.

Additionally, the <figcaption> element may replace an <img> element’s alt attribute if the content of the <figcaption> element provides a useful description of the visual content of the image.

```html
<figure>
  <img src="dog.jpg">
  <figcaption>A beautiful black, brown, and white hound dog wearing kerchief.</figcaption>
</figure>
```

Not all forms of media need to be included within a <figure> element or include a <figcaption> element; only those that are self-contained and belong together as a group.


## 总结
除了文本内容外，多媒体内容在网站中占比很大。在网站中使用图片，音频，视频在最近几年暴增，也没有停缓的趋势。现在我们知道了在设计中如何使用这些多媒体，以及如何使用它们来丰富我们网站的内容。

回顾一下：
* 向网页中添加图片，音频，视频，内框架的最好的方式。
* 在不同的情况下对图片进行定位。
* 在老版本的浏览器中提供备用的音频和视频。
* 音频和视频中的常用属性
* 无缝属性让我们可以将内框架表现如同是当前网站的一部分
* 语义化标记自包含内容，包括多媒体文件。

我们已经到学习HTML与CSS的冲刺阶段了，仅仅剩下几个组件需要介绍了，接下来我们将讨论表单。


## 资源与链接
* [Using HTML5 audio and video](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_HTML5_audio_and_video) via Mozilla Developer Network
* [Audio HTML5 Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio) via Mozilla Developer Network
* [Introduction to HTML5 Video](http://dev.opera.com/articles/introduction-html5-video/) via Dev.Opera
* [The figure & figcaption elements](http://html5doctor.com/the-figure-figcaption-elements/) via HTML5 Doctor

## 课程链接
* [课程08：创建列表](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_08_Creating_Lists.md)
* [课程10：创建表单](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_10_Building_Forms.md)
