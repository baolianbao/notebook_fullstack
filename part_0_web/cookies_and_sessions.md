# HTTP Cookies 和 HTTP Session

## HTTP cookies
HTTP cookies，通常又称作"cookies"，已经存在了很长时间，但是仍旧没有被予以充分的理解。首要的问题是存在了诸多误区，认为cookies是后门程序或病毒，或压根不知道它是如何工作的。第二个问题是对于cookies缺少一个一致性的接口。尽管存在着这些问题，cookies仍旧在web开发中起着如此重要的作用，以至于如果cookie在没有可替代品出现的情况下消失，我们许多喜欢的Web应用将变得毫无用处。

### cookies的起源
早期Web开发面临的最大问题之一是如何管理状态。简言之，服务器端没有办法知道两个请求是否来自于同一个浏览器。那时的办法是在请求的页面中插入一个token，并且在下一次请求中将这个token返回（至服务器）。这就需要在form中插入一个包含token的隐藏表单域，或着在URL的qurey字符串中传递该token。这两种办法都强调手工操作并且极易出错。

[Lou Montulli](https://en.wikipedia.org/wiki/Lou_Montulli),那时是网景通讯的一个雇员，被认为在1994年将[“magic cookies”](https://en.wikipedia.org/wiki/Magic_cookie)的概念应用到了web通讯中。他意图解决的是web中的购物车，现在所有购物网站都依赖购物车。他的最早的[说明文档](https://curl.haxx.se/rfc/cookie_spec.html)提供了一些cookies工作原理的基本信息该文档在[RFC2109](https://tools.ietf.org/html/rfc2109)中被规范化（这是所有浏览器实现cookies的参考依据），并且最终逐步形成了[REF2965](https://tools.ietf.org/html/rfc2965).Montulli最终也被授予了关于[cookies的美国专利](http://v3.espacenet.com/publicationDetails/biblio?CC=US&NR=5774670&KC=&FT=E)。网景浏览器在它的第一个版本中就开始支持cookies，并且当前所有web浏览器都支持cookies。

### cookie是什么？
坦白的说，一个cookie就是存储在用户主机浏览器中的一小段文本文件。Cookies是纯文本形式，它们不包含任何可执行代码。一个Web页面或服务器告之浏览器来将这些信息存储并且基于一系列规则在之后的每个请求中都将该信息返回至服务器。Web服务器之后可以利用这些信息来标识用户。多数需要登录的站点通常会在你的认证信息通过后来设置一个cookie，之后只要这个cookie存在并且合法，你就可以自由的浏览这个站点的所有部分。再次，cookie只是包含了数据，就其本身而言并不有害。

Cookie总是保存在客户端中，按在客户端中的存储位置，可分为内存Cookie和硬盘Cookie。内存Cookie由浏览器维护，保存在内存中，浏览器关闭后就消失了，其存在时间是短暂的。硬盘Cookie保存在硬盘里，有一个过期时间，除非用户手工清理或到了过期时间，硬盘Cookie不会被删除，其存在时间是长期的。所以，按存在时间，可分为非持久Cookie和持久Cookie。

#### 1.cookie的属性
一般cookie所具有的属性，包括：

* Domain：域，表示当前cookie所属于哪个域或子域下面。
此处需要额外注意的是，在C#中，如果一个cookie不设置对应的Domain，那么在CookieContainer.Add(cookies)的时候，会死掉。对于服务器返回的Set-Cookie中，如果没有指定Domain的值，那么其Domain的值是默认为当前所提交的http的请求所对应的主域名的。比如访问 http://www.example.com，返回一个cookie，没有指名domain值，那么其为值为默认的www.example.com。

* Path：表示cookie的所属路径。
Expire time/Max-age：表示了cookie的有效期。expire的值，是一个时间，过了这个时间，该cookie就失效了。或者是用max-age指定当前cookie是在多长时间之后而失效。如果服务器返回的一个cookie，没有指定其expire time，那么表明此cookie有效期只是当前的session，即是session cookie，当前session会话结束后，就过期了。对应的，当关闭（浏览器中）该页面的时候，此cookie就应该被浏览器所删除了。

* secure：表示该cookie只能用https传输。一般用于包含认证信息的cookie，要求传输此cookie的时候，必须用https传输。
* httponly：表示此cookie必须用于http或https传输。这意味着，浏览器脚本，比如javascript中，是不允许访问操作此cookie的。


#### 2.服务器发送cookie给客户端
从服务器端，发送cookie给客户端，是对应的Set-Cookie。包括了对应的cookie的名称，值，以及各个属性。
例如：
Set-Cookie: lu=Rg3vHJZnehYLjVg7qi3bZjzg; Expires=Tue, 15 Jan 2013 21:47:38 GMT; Path=/; Domain=.169it.com; HttpOnly
Set-Cookie: made_write_conn=1295214458; Path=/; Domain=.169it.com
Set-Cookie: reg_fb_gate=deleted; Expires=Thu, 01 Jan 1970 00:00:01 GMT; Path=/; Domain=.169it.com; HttpOnly


#### 3.从客户端把cookie发送到服务器
从客户端发送cookie给服务器的时候，是不发送cookie的各个属性的，而只是发送对应的名称和值。
例如：
GET /spec.html HTTP/1.1
Host: www.example.org
Cookie: name=value; name2=value2
Accept: */*


#### 4.关于修改，设置cookie
除了服务器发送给客户端（浏览器）的时候，通过Set-Cookie，创建或更新对应的cookie之外，还可以通过浏览器内置的一些脚本，比如javascript，去设置对应的cookie，对应实现是操作js中的document.cookie。


#### 5.Cookie的缺陷
(1)cookie会被附加在每个HTTP请求中，所以无形中增加了流量。
(2)由于在HTTP请求中的cookie是明文传递的，所以安全性成问题。（除非用HTTPS)
(3)Cookie的大小限制在4KB左右。对于复杂的存储需求来说是不够用的。



## HTTP Serssion
 session在web开发中是一个非常重要的概念，这个概念很抽象，很难定义，也是最让人迷惑的一个名词，也是最多被滥用的名字之一，在不同的场合，session一次的含义也很不相同。这里只探讨HTTP Session。
 
为了说明问题，这里基于Java Servlet理解Session的概念与原理，这里所说Servlet已经涵盖了JSP技术，因为JSP最终也会被编译为Servlet，两者有着相同的本质。
 
在Java中，HTTP的Session对象用javax.servlet.http.HttpSession来表示。
 
### 概念
Session代表服务器与浏览器的一次会话过程，这个过程是连续的，也可以时断时续的。在Servlet中，session指的是HttpSession类的对象，这个概念到此结束了，也许会很模糊，但只有看完本文，才能真正有个深刻理解。
 
### Session创建的时间是：
一个常见的误解是以为session在有客户端访问时就被创建，然而事实是直到某server端程序调用 HttpServletRequest.getSession(true)这样的语句时才被创建，注意如果JSP没有显示的使用 <% @page session="false"%> 关闭session，则JSP文件在编译成Servlet时将会自动加上这样一条语句 HttpSession session = HttpServletRequest.getSession(true);这也是JSP中隐含的 session对象的来历。
由于session会消耗内存资源，因此，如果不打算使用session，应该在所有的JSP中关闭它。
 
引申：
1）、访问*.html的静态资源因为不会被编译为Servlet，也就不涉及session的问题。
2）、当JSP页面没有显式禁止session的时候，在打开浏览器第一次请求该jsp的时候，服务器会自动为其创建一个session，并赋予其一个sessionID，发送给客户端的浏览器。以后客户端接着请求本应用中其他资源的时候，会自动在请求头上添加：
Cookie:JSESSIONID=客户端第一次拿到的session ID
这样，服务器端在接到请求时候，就会收到session ID，并根据ID在内存中找到之前创建的session对象，提供给请求使用。这也是session使用的基本原理----搞不懂这个，就永远不明白session的原理。
下面是两次请求同一个jsp，请求头信息：

通过图可以清晰发现，第二次请求的时候，已经添加session ID的信息。
 
### Session删除的时间是：
1）Session超时：超时指的是连续一定时间服务器没有收到该Session所对应客户端的请求，并且这个时间超过了服务器设置的Session超时的最大时间。
2）程序调用HttpSession.invalidate()
3）服务器关闭或服务停止
 
### session存放在哪里：服务器端的内存中。不过session可以通过特殊的方式做持久化管理。
 
### session的id是从哪里来的
sessionID是如何使用的：当客户端第一次请求session对象时候，服务器会为客户端创建一个session，并将通过特殊算法算出一个session的ID，用来标识该session对象，当浏览器下次（session继续有效时）请求别的资源的时候，浏览器会偷偷地将sessionID放置到请求头中，服务器接收到请求后就得到该请求的sessionID，服务器找到该id的session返还给请求者（Servlet）使用。一个会话只能有一个session对象，对session来说是只认id不认人。
 
### session会因为浏览器的关闭而删除吗？
不会，session只会通过上面提到的方式去关闭。
 
### 同一客户端机器多次请求同一个资源，session一样吗？
一般来说，每次请求都会新创建一个session。

 
其实，这个也不一定的，总结下：对于多标签的浏览器（比如360浏览器）来说，在一个浏览器窗口中，多个标签同时访问一个页面，session是一个。对于多个浏览器窗口之间，同时或者相隔很短时间访问一个页面，session是多个的，和浏览器的进程有关。对于一个同一个浏览器窗口，直接录入url访问同一应用的不同资源，session是一样的。
 
### session是一个容器，可以存放会话过程中的任何对象。
 
### session因为请求（request对象）而产生，同一个会话中多个request共享了一session对象，可以直接从请求中获取到session对象。
 
### 其实，session的创建和使用总在服务端，而浏览器从来都没得到过session对象。
但浏览器可以请求Servlet（jsp也是Servlet）来获取session的信息。客户端浏览器真正紧紧拿到的是session ID，而这个对于浏览器操作的人来说，是不可见的，并且用户也无需关心自己处于哪个会话过程中。

## 参考
* [Cookie/Session机制详解](http://blog.csdn.net/fangaoxin/article/details/6952954)
* [Http协议中Cookie详细介绍](http://www.jianshu.com/p/8731e8d62b3d / http://www.169it.com/article/3217120921.html)
* [深入理解HTTP Session](http://lavasoft.blog.51cto.com/62575/275589/)