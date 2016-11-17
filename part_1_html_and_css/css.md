CSS是什么？
基本语法
在浏览器中是如何工作的
CSS发展历史
CSS当前状态
CSS Specifications
CSS相关资源

## CSS是什么？
可以认为HTML控制文档的结构和内容，CSS控制外观
Style sheets are collection of formatting rules

浏览器有默认样式，我们创建CSS就是替换默认的样式，由于存在默认的样式可能会导致我们的CSS效果在不同的浏览器里看起来不一样，这个时候我们可能会去找自己的CSS文件出什么问题，这个时候就要考虑CSS Reset

用户是可以控制文档内容显示效果，比如字体，页面大小，甚至完全禁用，为什么不呢？
有些设计师烂透了。

同时我们也要记住的一个核心就是，文档是用来沟通和传递信息的，CSS会提升体验，但仍旧需要以内容为主，所以这就需要我们站在用户的角度来思考如何更加合理的去设计页面，去写CSS

## CSS语法
CSS 由两部分组成：选择器和声明
### Selectors

### declaration
由大括号包含的一组规则，规则是由属性和值组成，并以`;`分隔
* property
* value

### 空白
选择器里的空白需要注意，但是声明部分空白不要紧

当然还有其他的一些重点，比如简写，伪元素，伪类 ，行内规则等等，但我们可以按照如下的几个点展开：
* 先集中精力搞定CSS语法的基本元素
* 浏览CSS Specifications
* 阅读别人的CSS

## 基本的选择器类型
* 元素选择器
* 类选择器
* ID选择器
### 混合选择器（Element-Specific Selectors） h2.subheading, div#sidebar
#### class和ID命名规则：
1. 不要使用空格和特殊字符
2. 区分大小写
3. 建立CSS标准(Establish standards for your CSS and stay consistent with them)
### 层级选择器 
Highly specific selectors that target elements based on their location within other elements 
`div p span {color:blue;}`
虽然层级没有限制，但超过3级效率就会很低，同时也不需要递减层级。

选择器组
允许让一组选择器共享格式
`h1,h2,.quote{font-weight: normal; color:blue;}`

## HTML中引用CSS的几种方式
1. 外部文件
2. 头部嵌套
3. 行内样式
使用规则：
* 大多数项目都使用外部CSS文件
* 嵌入式样式主要用于覆盖外部样式
* 一开始对项目样式有全局观