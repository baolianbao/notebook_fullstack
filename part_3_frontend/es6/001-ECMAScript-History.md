# ECMAScipt 历史

## ECMA、ECMA International与ISO
Ecma International是一家国际性会员制度的信息和电信标准组织。1994年之前，名为欧洲计算机制造商协会（European Computer Manufacturers Association）。因为计算机的国际化，组织的标准牵涉到很多其他国家，因此组织决定改名表明其国际性。现名称已不属于首字母缩略字。
组织在1961年的日内瓦建立为了标准化欧洲的计算机系统。在欧洲制造、销售或开发计算机和电信系统的公司都可以申请成为会员。

Ecma International的任务包括与有关组织合作开发通信技术和消费电子标准、鼓励准确的标准落实、和标准文件与相关技术报告的出版。四十年来，Ecma建立了很多信息和电信技术标准。组织出版了370标准和90技术报告，大约三分之二被[国际标准化组织（ISO）](https://zh.wikipedia.org/wiki/%E5%9C%8B%E9%9A%9B%E6%A8%99%E6%BA%96%E5%8C%96%E7%B5%84%E7%B9%94)批准为国际标准。
与国家政府标准机构不同，Ecma国际是企业会员制的组织。组织的标准化过程比较商业化，自称这种营运方式减少官僚追求效果。

## ECMAScipt语言标准
ECMAScipt语言标准也就是[ECMA-262](https://www.ecma-international.org/publications/standards/Ecma-262.htm)，是基于JavaScript来制定的。 这也是为什么一会儿听到JavaScript一会儿听到ECMAScript的原因。

所谓标准，只是提供理想的指导和参考，实现和支持的环境却是错综复杂。
简单表达：ECMAScript是期望，JavaScript是这种期望的一种实现，还有其他的实现，例如ActionScript。

## ECMAScript发展历程
[Netscape](https://en.wikipedia.org/wiki/Netscape_Communications_Corporation)的[Brendan Eich](https://en.wikipedia.org/wiki/Brendan_Eich)早期创造了一门脚本语言，一开始叫Mocha，后来又叫LiveScript，最后在1995年称之为JavaScript。
然后在1996年3月发布了支持JavaScript的[Netscape Navigator](https://en.wikipedia.org/wiki/Netscape_Navigator) 2.0。

作为在客户端获得成功的脚本语言，微软为了捍卫浏览器市场，也创建了一个比较类似的语言名叫[JScript](https://en.wikipedia.org/wiki/JScript)。 

1996年，Netscape将JavaScript提交给ECMA International用来标准化和规范工作，也就是ECMA-262了，第一版本的ECMA-262（也就是ES1）在1997年6月份的ECMA大会通过，之后又不断发布了几个标准，至于为什么叫ECMAScript就有点像Netscape和微软打架争名字，然后折衷叫ECMAScript。
然而开发者任然习惯叫JavaScript。

> 注意：JavaScript和JScript都致力于兼容ECMAScript，同时也提供了ECMAScript标准中没有提到的一些特性。

### 版本
|版本   |发布日期    |更新内容   |
|---    |---        |---       |
|1      | 1997.6    |第一版     |
|2      | 1998.6    |Editorial changes to keep the specification fully aligned with ISO/IEC 16262 international standard|
|3      | 1999.12   |新增正则表达式，更好的字符串处理，新的流程控制语句，try/catch异常处理，error定义以及其他提升|
|4      | 取消      |Fourth Edition was abandoned, due to political differences concerning language complexity. Many features proposed for the Fourth Edition have been completely dropped; some are proposed for ECMAScript Harmony.|
|5      | 2009.12   |Adds "strict mode," a subset intended to provide more thorough error checking and avoid error-prone constructs. Clarifies many ambiguities in the 3rd edition specification, and accommodates behaviour of real-world implementations that differed consistently from that specification. Adds some new features, such as getters and setters, library support for JSON, and more complete reflection on object properties.[10]|
|5.1    | 2011.6    |This edition 5.1 of the ECMAScript Standard is fully aligned with third edition of the international standard ISO/IEC 16262:2011.|
|6      | 2015.6    | The Sixth Edition, known as ES6 or ECMAScript 2015,[11] adds significant new syntax for writing complex applications, including classes and modules, but defines them semantically in the same terms as ECMAScript 5 strict mode. Other new features include iterators and for/of loops, Python-style generators and generator expressions, arrow functions, binary data, typed arrays, collections (maps, sets and weak maps), promises, number and math enhancements, reflection, and proxies (metaprogramming for virtual objects and wrappers). As the first "ECMAScript Harmony" specification, it is also known as "ES6 Harmony."|
|7      | 2016.6    | The Seventh Edition intended to continue the themes of language reform, code isolation, control of effects and library/tool enabling from ES6, includes two new features: the exponentiation operator (**) and Array.prototype.includes.|


从上面可以看出的几个信息就是：
1. 我们有ES1，ES2，ES3， ES5， ES6(ES2015)，ES7 ，但就是没有ES4。
2. 鉴于环境的滞后性，目前我们主要专注于ES3，ES5，ES6，查看编译器(Babel/TypeScript等)，桌面浏览器，服务端，移动端等等环境对ES的支持情况：
* http://kangax.github.io/compat-table/es6/
* http://node.green/
总体上来说对于ES5支持程度非常高，对ES6支持的工作也在进展中。


## 下一步
基于上面的了解，就会有如下的问题：
1. ES5，ES6标准里具体的内容是什么？
* [ECMA-262 5.1 Edition](http://www.ecma-international.org/ecma-262/5.1/)
* [ECMA-262 6.0 Edition](http://www.ecma-international.org/ecma-262/6.0/)
> 注意ES6是我们习惯性的叫法，ECMA已经通过了命名方式是按年来的，所以叫ES2015更加合适。

2. 既然ES5支持程度这么高，我就用它就好了，会有哪些缺点？
Perhaps the most difficult problem that ES5 poses for us is the difficulty in identifying issues at development time. Tooling for ES5 is lacking as it is complicated, at best, for a tool to decipher how to inspect ES5 for concerns. We’d like to know what properties an object in another file contains, what an invalid parameter to a function may be, or let us know when we use a variable in an improper scope. ES5 makes these things difficult on developers and on tooling.

3. ES6/ES2015相比于ES5有哪些亮点？
[ECMAScript 6 features](https://github.com/lukehoban/es6features)

需要强调的是[Node.js6基本完全支持ES6了](https://nodejs.org/en/docs/es6/)
Node 4.x是LTS版本，根据他们的规则，偶数版本主要用于提高稳定性和安全性，奇数版本(例如5.x)主要用于添加新的特性，可以看看他们官网的指导：https://nodejs.org/en/blog/community/node-v5/


4. 如果我想用ES6中的特性怎么办？
transpilers 

关于浏览器支持可以使用[Babel](https://babeljs.io/)
而且前面提到的开发者在使用JavaScript常见的问题就是查找错误，TypeScript是一个好的选择。
> The value in TypeScript is not in the writing less code. The value of TypeScript is in writing safer code.

那么TypeScript能为ES015提供什么？主要集中在是三个方面：
1. Types
2. Interfaces
3. ES2016的特性，例如Annotation/Decorators 和 async/await.

Types and interfaces help provide the tooling it needs to identify problems early as we type them.
With these features our editors don’t have to guess whether we used a function properly or not. The information is readily available for the tool to raise a red flag to us so we can fix he issues right away. In some cases, these tools can also help recommend and refactor for us!
TypeScript promises to be forward thinking. It helps bring the agreed upon features in the future ECMAScript spec to us today. For example features like decorators (used in Angular 2) and async/await (a popular technique to make async programming easier in C#). Decorators are available now in TypeScript while async/await is coming soon in v 2.0 according to the TypeScript roadmap.

TypeScript和JavaScript有差别吗？
> TypeScript is a typed superset of JavaScript that compiles to plain JavaScript.



5. 到底如何使用这些Transpilers呢？

配合一些工具例如 gulp, grunt webpack systemJs等等来调用Babel和TypeScript进行转换，一些IDE甚至直接支持。