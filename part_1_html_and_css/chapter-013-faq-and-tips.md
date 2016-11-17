title: CSS Div左侧固定宽度，右侧填充
date: 2016-04-16 00:20:08
tags: [html,css]
categories: HTML And CSS Tips
---

```html
<div class="container">
    <div class="right">
        right content fixed width
    </div>
    <div class="left">
        left content flexible width
    </div>
</div>
```

```css
.container {
   height: auto;
   overflow: hidden;
}

.right {
    width: 180px;
    float: right;
    background: #aafed6;
}

.left {
    float: none; /* not needed, just for clarification */
    background: #e8f6fe;
    /* the next props are meant to keep this block independent from the other floated one */
    width: auto;
    overflow: hidden;
}​​
```

http://stackoverflow.com/questions/5195836/2-column-div-layout-right-column-with-fixed-width-left-fluid