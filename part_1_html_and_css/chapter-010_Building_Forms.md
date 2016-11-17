title: 课程10：创建表单
date: 2016-04-08 00:00:03
tags: [html,css]
categories: HTML And CSS
---

HTML
  Initializing a Form
  Text Fields & Textareas
  Multiple Choice Inputs & Menus
  Form Buttons
  Other Inputs
  Organizing Form Elements
  Form & Input Attributes

Forms are an essential part of the Internet, as they provide a way for websites to capture information from users and to process requests, and they offer controls for nearly every imaginable use of an application. Through controls or fields, forms can request a small amount of information—often a search query or a username and password—or a large amount of information—perhaps shipping and billing information or an entire job application.

<!--more -->

表单在互联网中是非常重要的一部分，它们让网站可以捕获用户信息然后处理请求。 通过控件和域它们可以发布像搜索这样简单的请求或者如用户名密码，或者运输单、账单，或者工作信息等复杂请求。

为了获取用户输入，我们需要知道如何创建表单。在本课程中我们将讨论如何使用HTML来标记表单，哪种元素是用来捕获不同的数据的，以及如何通过CSS来设置表单样式。我们不会深入讨论表单中的信息是如何被网站后端处理的。表单的处理是更加高深的话题，不在本书的讨论范围之内，现在我们集中讨论表单的创建于样式。

## 初始化表单

我们使用 `<form>`元素像网页中添加表单。 `<form>`元素标记了页面控件的位置。此外它很像`<div>`元素，包裹了表单的所有的元素。

```html
<form action="/login" method="post">
  ...
</form>
```

有几个属性可以添加到`<form>`元素中，最常用的是`action` 和`method`属性。 `action`属性包含了用于处理该表单所包含的信息的服务端URL。`method`属性是浏览器用于提交表单数据的HTTP方法。Both of these <form> attributes pertain to submitting and processing data.

## 文本框 & 文本域

我们可以在表单中使用好几种元素来获取用户输入的文本信息。尤其是用于获取基于文本或字符串的文本框和文本域，这些数据包括文本内容，密码，电话号码或者其他信息。

### 文本框

用于获取用户文本的一个主要元素是`<input>`。`<input>`元素使用`type` 属性来定义该控件用于捕获什么信息。最常见的属性值是`text`，它用于捕获单行文本输入。
除了设置`type`属性外，我们也需要给`<input>`元素设置`name`属性。`name`属性用于作为控件的名称，以及将会和输入数据一起被传递到服务器。

```html
<input type="text" name="username">
```

`<input>`元素是自包含元素，也就是它仅使用一个标签，并不包裹其他内容。该元素的值尤其属性和对应的值提供。

最初只用两个基于文本类型的属性值：`text`和`password`（用于处理密码），但是HTML5带来了其他几种新的 `type`属性值。

这些值给控件提供了更加清晰的语义，同时也给用户体统了更好的控件。如果浏览器不能势必这些HTML5`type`属性值，将会使用`text`属性值作为备用。以下是行的HTML5输入类型列表。

* color
* date
* datetime
* email
* month
* number
* range
* search
* tel
* time
* url
* week

如下`<input>`元素显示如何使用HTML5中的一些`type`属性值；下图显示了这些不同的值在iOS中看起来的效果如何。注意不同的值提供了是怎么提供了不同的控件，这些所有的控件让用户输入更加简单。
```html
<input type="date" name="birthday">
<input type="time" name="game-time">
<input type="email" name="email-address">
<input type="url" name="website">
<input type="number" name="cost">
<input type="tel" name="phone-number">
```

iOS7 Date Control
Fig 10
iOS7 controls for an <input> element with a type attribute value of date
iOS7 Time Control
Fig 10
iOS7 controls for an <input> element with a type attribute value of time
iOS7 Email Control
Fig 10
iOS7 controls for an <input> element with a type attribute value of email
iOS7 URL Control
Fig 10
iOS7 controls for an <input> element with a type attribute value of url
iOS7 Number Control
Fig 10
iOS7 controls for an <input> element with a type attribute value of number
iOS7 Telephone Control
Fig 10
iOS7 controls for an <input> element with a type attribute value of tel

### 文本域

另外一个用于捕获基于文本数据元素是`<textarea>`， 和`<input>`元素不同的是，`<textarea>`元素可以接收多行文本，此外，`<textarea>`元素还有可以包裹空白文本的开始和闭合标签。由于`<textarea>`元素只接受一种类型的值，所以它并没有`type`
属性。但是 `name`属性依然使用。

```html
<textarea name="comment">Add your comment here</textarea>
```


The <textarea> element has two sizing attributes: cols for width in terms of the average character width and rows for height in terms of the number of lines of visible text. The size of a textarea, however, is more commonly identified using the width and height properties within CSS.

`<textarea>`元素有两个用于设置大小的属性：用于设置宽度的`cols`（字符的平均宽度）和 相对于可见文本的行数的设置高度的`rows`属性。

## 多选控件 & 菜单
除了基于文本的输入控件外，HTML还允许用户使用多选和下拉列表来选择数据。我们有好几种这样的表单控件元素，每种都有不同的优势。

### 单选按钮

单选按钮是可以让用户从简单选项列表中做出快速选择的的方法。单选按钮和多选项相反，它让用户一次只能选择一个选项。

要创建单选按钮，我们使用`<input>`元素，将`type`属性值设置为`radio` 每个单选按钮元素必须设置相同的`name`属性值用表示这些按钮属于同一组。

基于文本的控件，输入值由用户输入决定，而单选按钮中用户是从多选中做出选择，因此我们需要定义输入值。使用`value`属性，我们可以为每个`<input>`元素设置指定的值。

此外，我们可以使用布尔值`checked`为用户预选一个单选按钮。


```html
<input type="radio" name="day" value="Friday" checked> Friday
<input type="radio" name="day" value="Saturday"> Saturday
<input type="radio" name="day" value="Sunday"> Sunday
```


### 多选框

和单选按钮比较相似的是多选框，除了它们的`type`属性值外，它们使用相同的属性和模式，它们的区别是，多选框允许用户选择多个值，并将这些值绑定到一个控件名称上，但单选按钮只允许用户使用一个值。

```html
<input type="checkbox" name="day" value="Friday" checked> Friday
<input type="checkbox" name="day" value="Saturday"> Saturday
<input type="checkbox" name="day" value="Sunday"> Sunday
```


### 下拉列表
Drop-down lists are a perfect way to provide users with a long list of options in a practical manner. A long column of radio buttons next to a list of different options is not only visually unappealing, it’s daunting and difficult for users to comprehend, especially those on a mobile device. Drop-down lists, on the other hand, provide the perfect format for a long list of choices.
通过`<select>` 和`<option>`元素我们可以创建下拉列表，`<select>`元素会包含所有的菜单选项，且每个菜单选项都使用`<option>`元素来标记。

`name`属性位于`<select>`元素中，`value`属性位于嵌套在`<select>`元素中的`<option>`元素里。每个`<option>`元素的`value`属性用于对应`<select>`元素的`name`属性。

每个`<option>`元素包含了列表的每个选项的文本（对用户可见）。

和单选按钮、多选框的 `checked`布尔值类似，下拉列表可以使用`selected`布尔属性来为用户预选某个选项。



```html
<select name="day">
  <option value="Friday" selected>Friday</option>
  <option value="Saturday">Saturday</option>
  <option value="Sunday">Sunday</option>
</select>
```


### Multiple Selections 多选

当我们将`multiple`属性添加到`<select>`元素中，可以允许用户一次选择多个选项。此外，在`<option>`元素中可以使用多个`selected` 布尔值来预选多个选项。

`<select>`元素的尺寸可以使用CSS来控制，同时为了多个选项需要适当调整。 通知用户通过按下Shift键可以多选很有必要。

```html
<select name="day" multiple>
  <option value="Friday" selected>Friday</option>
  <option value="Saturday">Saturday</option>
  <option value="Sunday">Sunday</option>
</select>
```


## Form Buttons 表单按钮
After a user inputs the requested information, buttons allow the user to put that infor- mation into action. Most commonly, a submit input or submit button is used to process the data.

在用户输完请求信息后，按钮允许用户将

### Submit Input

Users click the submit button to process data after filling out a form. The submit button is created using the <input> element with a type attribute value of submit. The value attribute is used to specify the text that appears within the button.

```html
<input type="submit" name="submit" value="Send">
```


### Submit Button

As an <input> element, the submit button is self-contained and cannot wrap any other content. If more control over the structure and design of the input is desired—along with the ability to wrap other elements—the <button> element may be used.

The <button> element performs the same way as the <input> element with the type attribute value of submit; however, it includes opening and closing tags, which may wrap other elements. By default, the <button> element acts as if it has a type attribute value of submit, so the type attribute and value may be omitted from the <button> element if you wish.

Rather than using the value attribute to control the text within the submit button, the text that appears between the opening and closing tags of the <button> element will appear.

```html
<button name="submit">
  <strong>Send Us</strong> a Message
</button>
```


## Other Inputs
Besides the applications we’ve just discussed, the <input> element has a few other use cases. These include passing hidden data and attaching files during form processing.

### Hidden Input

Hidden inputs provide a way to pass data to the server without displaying it to users. Hidden inputs are typically used for tracking codes, keys, or other information that is not pertinent to the user but is helpful when processing the form. This information is not displayed on the page; however, it can be found by viewing the source code of a page. It should therefore not be used for sensitive or secure information.

To create a hidden input, you use the hidden value for the type attribute. Additionally, include the appropriate name and value attribute values.

```html
<input type="hidden" name="tracking-code" value="abc-123">
```

### File Input

To allow users to add a file to a form, much like attaching a file to an email, use the file value for the type attribute.

```html
<input type="file" name="file">
```


Unfortunately, styling an <input> element that has a type attribute value of file is a tough task with CSS. Each browser has its own default input style, and none provide much control to override the default styling. JavaScript and other solutions can be employed to allow for file input, but they are slightly more difficult to construct.

## Organizing Form Elements
Knowing how to capture data with inputs is half the battle. Organizing form elements and controls in a usable manner is the other half. When interacting with forms, users need to understand what is being asked of them and how to provide the requested information.

By using labels, fieldsets, and legends, we can better organize forms and guide users to properly complete them.

### Label

Labels provide captions or headings for form controls, unambiguously tying them together and creating an accessible form for all users and assistive technologies. Created using the <label> element, labels should include text that describes the inputs or controls they pertain to.

Labels may include a for attribute. The value of the for attribute should be the same as the value of the id attribute on the form control the label corresponds to. Matching up the for and id attribute values ties the two elements together, allowing users to click on the <label> element to bring focus to the proper form control.

```html
<label for="username">Username</label>
<input type="text" name="username" id="username">
```


If desired, the <label> element may wrap form controls, such as radio buttons or check boxes. Doing so allows omission of the for and id attributes.

```html
<label>
  <input type="radio" name="day" value="Friday" checked> Friday
</label>
<label>
  <input type="radio" name="day" value="Saturday"> Saturday
</label>
<label>
  <input type="radio" name="day" value="Sunday"> Sunday
</label>
```


### Fieldset

Fieldsets group form controls and labels into organized sections. Much like a <section> or other structural element, the <fieldset> is a block-level element that wraps related elements, specifically within a <form> element, for better organization. Fieldsets, by default, also include a border outline, which can be modified using CSS.

```html
<fieldset>
  <label>
    Username
    <input type="text" name="username">
  </label>
  <label>
    Password
    <input type="text" name="password">
  </label>
</fieldset>
```


### Legend

A legend provides a caption, or heading, for the <fieldset> element. The <legend> element wraps text describing the form controls that fall within the fieldset. The markup should include the <legend> element directly after the opening <fieldset> tag. On the page, the legend will appear within the top left part of the fieldset border.

```html
<fieldset>
  <legend>Login</legend>
  <label>
    Username
    <input type="text" name="username">
  </label>
  <label>
    Password
    <input type="text" name="password">
  </label>
</fieldset>
```


## Form & Input Attributes
To accommodate all of the different form, input, and control elements, there are a number of attributes and corresponding values. These attributes and values serve a handful of different functions, such as disabling controls and adding form validation. Described next are some of the more frequently used and helpful attributes.

### Disabled

The disabled Boolean attribute turns off an element or control so that it is not available for interaction or input. Elements that are disabled will not send any value to the server for form processing.

￼Applying the disabled Boolean attribute to a <fieldset> element will disable all of the form controls within the fieldset. If the type attribute has a hidden value, the hidden Boolean attribute is ignored.

```html
<label>
  Username
  <input type="text" name="username" disabled>
</label>
```


### Placeholder

The placeholder HTML5 attribute provides a hint or tip within the form control of an <input> or <textarea> element that disappears once the control is clicked in or gains focus. This is used to give users further information on how the form input should be filled in, for example, the email address format to use.

```html
<label>
  Email Address
  <input type="email" name="email-address" placeholder="name@domain.com">
</label>
```


The main difference between the placeholder and value attributes is that the value attribute value text stays in place when a control has focus unless a user manually deletes it. This is great for pre-populating data, such as personal information, for a user but not for providing suggestions.

### Required

The required HTML5 Boolean attribute enforces that an element or form control must contain a value upon being submitted to the server. Should an element or form control not have a value, an error message will be displayed requesting that the user complete the required field. Currently, error message styles are controlled by the browser and cannot be styled with CSS. Invalid elements and form controls, on the other hand, can be styled using the :optional and :required CSS pseudo-classes.

Validation also occurs specific to a control’s type. For example, an <input> element with a type attribute value of email will require not only that a value exist within the control, but also that it is a valid email address.

``` html
<label>
  Email Address
  <input type="email" name="email-address" required>
</label>
```


### Additional Attributes

Other form and form control attributes include, but are not limited to, the following. Please feel free to research these attributes as necessary.

* accept
* autocomplete
* autofocus
* formaction
* formenctype
* formmethod
* formnovalidate
* formtarget
* max
* maxlength
* min
* pattern
* readonly
* selection
* Direction
* step

## Login Form Example
The following is an example of a complete login form that includes several different elements and attributes to illustrate what we’ve covered so far. These elements are then styled using CSS.

HTML
```html
<form>
  <fieldset class="account-info">
    <label>
      Username
      <input type="text" name="username">
    </label>
    <label>
      Password
      <input type="password" name="password">
    </label>
  </fieldset>
  <fieldset class="account-action">
    <input class="btn" type="submit" name="submit" value="Login">
    <label>
      <input type="checkbox" name="remember"> Stay signed in
    </label>
  </fieldset>
</form>

```

CSS

```css
*,
*:before,
*:after {
   box-sizing: border-box;
}
form {
  border: 1px solid #c6c7cc;
  border-radius: 5px;
  font: 14px/1.4 "Helvetica Neue", Helvetica, Arial, sans-serif;
  overflow: hidden;
  width: 240px;
}
fieldset {
  border: 0;
  margin: 0;
  padding: 0;
}
input {
  border-radius: 5px;
  font: 14px/1.4 "Helvetica Neue", Helvetica, Arial, sans-serif;
  margin: 0;
}
.account-info {
  padding: 20px 20px 0 20px;
}
.account-info label {
  color: #395870;
  display: block;
  font-weight: bold;
  margin-bottom: 20px;
}
.account-info input {
  background: #fff;
  border: 1px solid #c6c7cc;
   box-shadow: inset 0 1px 1px rgba(0, 0, 0, .1);
  color: #636466;
  padding: 6px;
  margin-top: 6px;
  width: 100%;
}
.account-action {
  background: #f0f0f2;
  border-top: 1px solid #c6c7cc;
  padding: 20px;
}
.account-action .btn {
  background: linear-gradient(#49708f, #293f50);
  border: 0;
  color: #fff;
  cursor: pointer;
  font-weight: bold;
  float: left;
  padding: 8px 16px;
}
.account-action label {
  color: #7c7c80;
  font-size: 12px;
  float: left;
  margin: 10px 0 0 20px;
}

```


## In Practice
With an understanding of how to build forms in place, let’s create a registration page for our Styles Conference website so that we can begin to gather interest and sell tickets for the event.

Jumping into our register.html file, we’ll begin by following the same layout pattern we used on our Speakers and Venue pages. This includes adding a <section> element with a class attribute value of row just below the registration lead-in section and nesting a <div> element with a class attribute value of grid directly inside the <section> element.

Our code just below the lead-in section for the Register page should look like this:

```html
<section class="row">
  <div class="grid">
    ...
  </div>
</section>
```
As a refresher, the class attribute value of row adds a white background and provides some vertical padding, while the class attribute value of grid centers our content in the middle of the page and provides some horizontal padding.

Inside the <div> element with a class attribute value of grid we’re going to create two columns, one covering two-thirds of the page width and one covering one-third of the page width. The two-thirds column will be a <section> element on the left- hand side that tells users why they should register for our conference. The one-third column, then, will be a <form> element on the right-hand side providing a way for users to register for our conference.

We’ll add these two elements, and their corresponding col-2-3 and col-1-3 classes, directly inside the <div> element with a class attribute value of grid. Since both of these elements will be inline-block elements, we need to open a comment directly after the two-thirds column closing tag and then close that comment directly before the one-third column opening tag.

In all, our code should look like this:

```html
<section class="row">
  <div class="grid">

    <section class="col-2-3">
      ...
    </section><!--

    --><form class="col-1-3">
      ...
    </form>

  </div>
</section>
```
Now, inside our two-thirds column let’s add some details about our event and why it’s a good idea for aspiring designers and front-end developers to attend. We’ll do so using a handful of different heading levels (along with their pre-established styles), a paragraph, and an unordered list.

In our <section> element with a class attribute value of col-2-3, the code should look like this:

```html
<section class="col-2-3">

  <h2>Purchase a Conference Pass</h2>
  <h5>$99 per Pass</h5>

  <p>Purchase your Styles Conference pass using the form to the right. Multiple passes may be purchased within the same order, so feel free to bring a friend or two along. Once your order is finished we&#8217;ll follow up and provide a receipt for your purchase. See you soon!</p>

  <h4>Why Attend?</h4>

  <ul>
  <li>Over twenty world-class speakers</li>
    <li>One full day of workshops and two full days of presentations</li>
    <li>Hosted at The Chicago Theatre, a historical landmark</li>
    <li>August in Chicago is simply amazing</li>
  </ul>

</section>
```

Currently our unordered list doesn’t have any list item markers. All of the browser default styles have been turned off by the CSS reset we added all the way back in Lesson 1. Let’s create some custom styles specifically for this unordered list.

To do so, let’s add a class attribute value of why-attend to the unordered list.

```html
<ul class="why-attend">
    ...
</ul>
```
With a class available to add styles to, let’s create a new section for Register page styles at the bottom of our main.css file. Within this section let’s use the class to select the unordered list and add a list-style of square and some bottom and left margins.

The new section at the bottom of our main.css file should look like this:

```css
/*
  ========================================
  Register
  ========================================
*/

.why-attend {
  list-style: square;
  margin: 0 0 22px 30px;
}
```

The details section of our registration page is complete, so now it’s time to address our registration form. We’ll start by adding the action and method attributes to the <form> element. Since we haven’t set up our form processing, these attributes will simply serve as placeholders and will need to be revisited.

The code for our <form> element should look like this:

```html
<form class="col-1-3" action="#" method="post">
  ...
</form>
```
Next, inside the <form> element we’ll add a <fieldset> element. Inside the <fieldset> element we’ll add a series of <label> elements that wrap a given form control.

We want to collect a user’s name, email address, number of desired conference passes, and any potential comments. The name, email address, and number of conference passes are required fields, and we’ll want to make sure we use the appropriate elements and attributes for each form control.

With a mix of different input types, select menus, textareas, and attributes, the code for our form should look like the following:

```html
<form class="col-1-3" action="#" method="post">

  <fieldset>

    <label>
      Name
      <input type="text" name="name" placeholder="Full name" required>
    </label>

    <label>
      Email
      <input type="email" name="email" placeholder="Email address" required>
    </label>

    <label>
      Number of Passes
      <select name="quantity" required>
        <option value="1" selected>1</option>
        <option value="2">2</option>
        <option value="3">3</option>
        <option value="4">4</option>
        <option value="5">5</option>
      </select>
    </label>

    <label>
      Comments
      <textarea name="comments"></textarea>
    </label>

  </fieldset>

  <input type="submit" name="submit" value="Purchase">

</form>
```

Here we can see each form control nested within a <label> element. The Name form control uses an <input> element with a type attribute value of text, while the Email form control uses an <input> element with a type attribute value of email.

Both the Name and Email form controls include the required Boolean attribute and a placeholder attribute.

The Number of Passes form control uses the <select> element and nested <option> elements. The <select> element itself includes the required Boolean attribute, and the first <option> element includes the selected Boolean attribute.

The Comments form control uses the <textarea> element without any special modifications. And lastly, outside of the <fieldset> element is the submit form control, which is formed by an <input> element with a type attribute value of submit.

With the form in place, it’s time to add styles to it. We’ll begin with a few default styles on the <form> element itself and on the <input>, <select>, and <textarea> elements.

Within the register section of our main.css file we’ll want to add the following styles:

```html
form {
  margin-bottom: 22px;
}
input,
select,
textarea {
  font: 300 16px/22px "Lato", "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
}
```

We’ll start by placing a 22-pixel margin on the bottom of our form to help vertically space it apart from other elements. Then we’ll add some standard font-based styles—including weight, size, line-height, and family—for all of the <input>, <select>, and <textarea> elements.

By default, every browser has its own interpretation of how the styles for form controls should appear. With this in mind, we have repeated the font-based styles from our <body> element to ensure that our styles remain consistent.

Let’s add some styles to the elements within the <fieldset> element. Since we may add additional <fieldset> elements later on, let’s add a class attribute value of register-group to our existing <fieldset> element, and from there we can apply unique styles to the elements nested within it.

```html
<fieldset class="register-group">
  ...
</fieldset>
```
Once the register-group class attribute value is in place, we’ll add a few styles to the elements nested within the <fieldset> element. These styles will appear in our main.css file, below the existing form styles.

```css
.register-group label {
  color: #648880;
  cursor: pointer;
  font-weight: 400;
}
.register-group input,
.register-group select,
.register-group textarea {
  border: 1px solid #c6c9cc;
  border-radius: 5px;
  color: #888;
  display: block;
  margin: 5px 0 27px 0;
  padding: 5px 8px;
}
.register-group input,
.register-group textarea {
  width: 100%;
}
.register-group select {
  height: 34px;
  width: 60px;
}
.register-group textarea {
  height: 78px;
}
```
You’ll notice that most of these properties and values revolve around the box model, which we covered in Lesson 4. We’re primarily setting up the size of different form controls, ensuring that they are laid out appropriately. Aside from adding some box model styles, we’re adjusting the color and font-weight of a few elements.

So far, so good: our form is coming together quite nicely. The only remaining element yet to be styled is the submit button. As it’s a button, we actually have some existing styles we can apply here. If we think back to our home page, our hero section contained a button that received some styles by way of the btn class attribute value.

Let’s add this class attribute value, btn, along with a new class attribute value of btn-default to our submit button. Specifically we’ll use the class name of btn-default since this button is appearing on a white background and will be the default style for buttons moving forward.

```html
<input class="btn btn-default" type="submit" name="submit" value="Purchase">
```
Now our submit button has some shared styles with the button on the home page. We’ll use the btn-default class attribute value to then apply some new styles to our submit button specifically.

Going back to the buttons section of our main.css file, let’s add the following:

```css
.btn-default {
  border: 0;
  background: #648880;
  padding: 11px 30px;
  font-size: 14px;
}
.btn-default:hover {
  background: #77a198;
}
```
These new styles, which define the size and background of our submit button, are then combined with the existing btn class styles to create the final presentation of our submit button.

Our Register page is finished, and attendees can now begin to reserve their tickets.

Styles Conference website
Fig 10
Our registration page, which includes a form

## Demo & Source Code

Below you may view the Styles Conference website in its current state, as well as download the source code for the website in its current state.

View the Styles Conference Website or Download the Source Code (Zip file)

## Summary
Forms play a large role in how users interact with, provide information to, and take action on websites. We’ve taken all the right steps to learn not only how to mark up forms but also how to style them.

To quickly recap, within this lesson we discussed the following:

How to initialize a form
Ways to obtain text-based information from users
Different elements and methods for creating multiple choice options and menus
Which elements and attributes are best used to submit a form’s data for processing
How best to organize forms and give form controls structure and meaning
A handful of attributes that help collect more qualified data
Our understanding of HTML and CSS is progressing quite nicely, and we only have one more component to learn: tables. In the next chapter, we’ll take a look at how to organize and present data with tables.

Resources & Links
Forms via HTML Dog Form Element via Mozilla Developer Network Input Element via Mozilla Developer Network A Form of Madness via Dive Into HTML5



## 课程链接
* [课程09：添加多媒体](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_09_Adding_Media.md)
* [课程11：通过表格组织数据](https://github.com/hexcola/Learn_to_Code_HTML_And_CSS_zh/blob/master/Fundamentals/docs/Lesson_11_Organizing_Data_with_Tables.md)
