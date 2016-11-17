### 使用flash插件
首先，需要安装：
```bash
npm i flash
```

使用

```js
app.use(require('flash')());

```

之后，我们就可以在Request中访问flash对象了：

```js
app.get('/', function(req,res){
	res.render('index.html', {username: req.session.username});
	req.session.flash.splice(0,1);
});

app.post('/', function(req, res){
	var old_name = req.session.username;
	var username = req.body.username;

	if (old_name !== username){
		req.flash('info', 'Welcome '+ username);
	}

	req.session.username = username;
	res.redirect('/');
});
```

接着我们需要在模板里能够显示该信息：

{% for message in flash %}
    {{ message.message }}
{% endfor %}

话说，这个并不好使……因为它再的信息被读取后并未清空，信息会一直贮存在session中（req.session.flash）, 所以才使用：

```js
req.session.flash.splice(0,1);
```
来手动清空，当这样做并方便，需要优化，例如在`for message in flash`中将`flash`换成一个方法，每次执行都会剔除已经读出的消息。

## Essentials
npm i express -g

express --version

locally
npm install express --save


app.js

```
var express = require('express');
var app = express();

app.get('/', function(req, res) {
    res.send('Hello Express');
});

var server = app.listen(3000, function(){
    console.log('Listening on port 3000');
});

```

## Create Routes
get
无参数
app.get('/aboutme', function(req, res) {
    res.send('@hexcola');
})

有参数
app.get('/who/:name?', function(req, res){
    var name = req.params.name;
    res.send(name + ' was here');
});

app.get('/who/:name?/:title?', function(req, res){
    var name = req.params.name;
    var title = req.params.title;
    res.send(name + ' was here');
});

完全匹配
app.get('*', function(req, res){
    res.send('bad route');
})


## Using Template
what you want ? Jade or EJS?
npm install ejs --save

```
app.set('view engine', 'ejs');
```

we will create a folder named views, and we crate a file name default.ejs

```
app.get('/', function(req, res){
    // it will search views folder, and find the default.ejs file  
    res.render('default');
});
```

btw, if you don't want templates stay in the views folder, you can set anything you want , just doing by this:

```
app.set('views', __dirname + '/whateveryouwant');
```
then, your template file should be in the whateveryouwant folder.

### Render template with data
res.render('default', {title: 'Home'});

in the default.ejs file
<%= title %>

some other same shit:
for loop, conditions

在概念上，我们可以认为template就是View，而数据就是Model，这样处理起来，是不是就很好理解？

### template partials
在views文件夹内我们创建一个partials的文件夹，然后在里面创建一个page的文件夹，然后在里面创建head.ejs, footer.ejs

那么在其他需要引用的页面：
<% include partials/page/head.ejs %>
基本概念就是打散页面，让其原子化

### Using locals
locals变量可以在不同路由，不同视图页面都能共享变量
app.locals.title  = 'whatever you want?'
获取方式和渲染模板时候传递参数的方式是一样的：
<%= title %>



## Modularizing our Routes
随着项目体积增大，或者出于组织方式，我们有时候需要将路由放到不同的文件中，例如常规的项目和验证路由，我们就可以分开。

创建routes文件夹
var routes = require('./routes);

那么原来在app.js 下的路由：
```
app.get('/', function(req, res) {
    res.render('template');
});

app.get('/about', function(req, res){
    res.render('template');
});
```
就可以换成在routes文件夹下创建index.js文件中：
```
exports.index = function(req, res){
    res.render('template');
}

exports.about= function(req, res){
    res.render('template');
}
```

同时，在app.js中，我们需要修改代码为：
app.get('/', routes.index);
app.get('/about', routes.about);


## Structuring Our Content
### 使用express generator
`sudo npm i -g express-generator`

进入我们的项目，
`express - e project`
e 表示我们将使用ejs视图引擎

使用generator很简单，但有了前面的基础，一起看起来顺理成章了。


在views文件夹内我们创建一个partials的文件夹，然后在里面创建一个content的文件夹
views
    |__ content
        |__ socialmedia.ejs
        |__ somethingelse.ejs
        |__ 
        |__ ...
    |__ templates
        |__ header.ejs
        |__ footer.ejs
        |__ head.ejs
        |__ jsdefault.ejs
        |__ ...
    |__ err.ejs
    |__ index.ejs

JSON Online Editor

## Importing data
对于Node.js来说，可以直接像模块一样直接导入文件。
var data = require('./data.josn')
这将导入数据作为一个对象，存储在data中，当然我们也可以这样：
app.local.data = require('./data.json');
这样我们所有的页面都可以访问。


访问数据的方式：
1. 通过app.locals
2. 通过路由传递


Font Awesome

What's Next

Recommond books
Node for Front-End Developers
Learning Node
Node.js in Action



[Proposed Keystone Package Architecture](https://github.com/keystonejs/keystone/issues/912)


[省市区三级联动](https://github.com/fengyuanchen/distpicker)


[Bootstrap Collapse Panel](http://www.w3schools.com/Bootstrap/bootstrap_collapse.asp)

```html
<div class="panel-group">
  <div class="panel panel-default">
    <div class="panel-heading">
      <h4 class="panel-title">
        <a data-toggle="collapse" href="#collapse1">Collapsible panel</a>
      </h4>
    </div>
    <div id="collapse1" class="panel-collapse collapse">
      <div class="panel-body">Panel Body</div>
      <div class="panel-footer">Panel Footer</div>
    </div>
  </div>
</div>
```

## Mongo数据库快捷操作
```bash
$ mongo
# 查看所有的数据库
> show dbs 

# 使用指定的数据库
> use huaguoshan

# 查看当前数据库里有哪些集合
> show collections
```

#### 插入文档
```bash
> db.roles.insert({name:'Admin'})
> db.roles.insert({name:'Manager'})
# 批量插入
> db.roles.insert([{name:'Officer'}, {name:'Owner'}, {name: 'User'}])


> db.users.insert({username:'hexcola', role_id: ObjectId(57fa5ebfb92494fb110d2790)})

```

#### 查询
```bash
> db.find()
```

#### 删除

```bash
# 删除数据库
> db.dropDatabase()

# 删除集合
> db.collections.drop()

# 删除文档
> db.collections.remove({username: 'hexcola'})
```

## 关于passport.js的flash操作最好的实践方式
http://stackoverflow.com/questions/26403853/node-authentification-with-passport-js-how-to-flash-a-message-if-a-field-is-miss
查看那个使用了nunjucks的答案！
passReqToCallback 设置为true之后还需要为回调方法添加req参数！！
http://walidhosseini.com/journal/2014/10/18/passport-local-strategy-auth.html

它的答案里的的bootstrap的[alert](http://v4-alpha.getbootstrap.com/components/alerts/)不会自动消失，可以使用下面的答案来完成：
http://stackoverflow.com/questions/23101966/bootstrap-alert-auto-close
推荐答案

```js
$(".alert").fadeTo(2000, 500).slideUp(500, function(){
    $(".alert").alert('close');
});
```

# 关于passport登录成功后重定向的问题：
并没有什么好的思路：


```js
app.get('/login', function(req, res, next) {
  passport.authenticate('local', function(err, user, info) {
    if (err) { return next(err); }
    if (!user) { return res.redirect('/login'); }
    req.logIn(user, function(err) {
      if (err) { return next(err); }
      return res.redirect('/users/' + user.username);
    });
  })(req, res, next);
});
```

不过可以通过如下几个方式来获取上一个请求的URL：
res.redirect('back');
下面这个方案仅仅时候Express 4.X
req.get('Referrer')


## 假如用于提交表单的按钮不在form里，怎么使用jQuery来提交表单呢？

```js
// https://api.jquery.com/submit/
// http://stackoverflow.com/questions/1960240/jquery-ajax-submit-form
$("#doCreate").click( function(){
    $('#theForm').submit();}
);

var frm = $('#theForm');
frm.submit(function (ev) {
    $.ajax({
        type: frm.attr('method'),
        url: frm.attr('action'),
        data: frm.serialize(),
        success: function (data) {
        }
    });

    ev.preventDefault();
});
```

## Bootstrap + jQuery比较好用的日期选择器
租房项目需要使用到日期范围，这里推荐使用 [Datepicker](http://eonasdan.github.io/bootstrap-datetimepicker/)

## Express中使用Mongoose如何导出Schema
要完成这个，首先得明白以下两种方法的区别

```js
var UserSchema = mongoose.Schema({
    name: String
})

module.exports = mongoose.model('User', UserSchema);
```
versus this method:

```js
var UserSchema = mongoose.Schema({
    name: String
})

mongoose.model('User', UserSchema);
```

http://stackoverflow.com/questions/15462635/why-use-model-export-in-separate-model-files

然后我们通过

```js
var KeyValue = require('./share/keyvalue')
// 然后通过 KeyValue.schema 来获取Schema，没错，那个是小写。
```

当然也可以参考： http://stackoverflow.com/questions/8730255/how-to-get-schema-of-mongoose-database-which-defined-in-another-model


## 在项目中会遇到比较复杂的表单，尤其是一些动态的字段，这里就涉及到两个问题
1. 如何添加动态的字段？
2. 在提交表单的时候如何以数组的方式提交呢？
参考链接：
如何添加动态字段：
http://bootsnipp.com/snippets/featured/dynamic-form-fields-add-amp-remove
http://formvalidation.io/examples/adding-dynamic-field/
对于第二个formvalidation里的方法比较好用。
示例如下：

```html
<div class="panel panel-default">
    <div class="panel-heading">
        <h4 class="panel-title">
            <a data-toggle="collapse" href="#meter">仪表数据</a>
            <button type="button" class="btn btn-default addButton_meter"><i class="fa fa-plus"></i></button>
        </h4>
    </div>
    <div id="meter" class="panel-collapse collapse">
        <div class="panel-body">
            <!-- Add dynamic field-->
            <div class="form-group hide" id="meterTemplate">
                <div class="row">
                    <div class="col-xs-2">
                        <input  class="form-control" placeholder="仪表名称" type="text" name="name">
                    </div>
                    <div class="col-xs-3">
                        <input  class="form-control" placeholder="仪表编号" type="text" name="meterId">
                    </div>
                    <div class="col-xs-2">
                        <input  class="form-control" placeholder="单价" type="text" name="measureObjPrice">
                    </div>
                    <div class="col-xs-2">
                        <input  class="form-control" placeholder="观察日期" type="text" name="measureDate">
                    </div>
                    <div class="col-xs-2">
                        <input  class="form-control" placeholder="观察结果" type="text" name="measureValue">
                    </div>

                    <div class="col-xs-1">
                        <button type="button" class="btn btn-default removeButton_meter"><i class="fa fa-minus"></i></button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

```js
    $(document).ready(function(){
        /**
        * Meters Dynamic fields
        **/
        addDynamicFields('.addButton_meter',
        '.removeButton_meter',
        '#meterTemplate',
        'meter',
        ['name', 'meterId', 'measureObjPrice', 'measureDate', 'measureValue'],
        '.form-group');

        /**
        * Fees Dynamic fields
        */
        addDynamicFields('.addButton_fee',
        '.removeButton_fee',
        '#feeTemplate',
        'fee',
        ['key', 'value'],
        '.form-group');
        
    });

    /*
    * addButton {String}
    * removeButton {String}
    * template {String}
    * targetObj {String}
    * fields {Array[String]}
    * parentsClass {String}
    */
    function addDynamicFields(addButton, removeButton, templateId, targetObj, fields, parentsClass){
        index = 0;

        $(addButton).click(function(e){
            e.preventDefault();
            var $template = $(templateId),
                $clone = $template
                            .clone()
                            .removeClass('hide')
                            .removeAttr('id')
                            .insertBefore($template);
                
                fields.forEach(function(field){
                    $clone.find('[name="'+field+'"]').attr('name', targetObj+'['+index+']['+field+']').end();
                });

                index ++;
                
                $(removeButton).click(function(e){
                    e.preventDefault();
                    var $row = $(this).parents(parentsClass);
                    $row.remove();
                })
        })
    }


```

同样在实例中也看到了该如何提交同一类字段的方式，参考： 
http://codereview.stackexchange.com/questions/94493/submit-an-array-as-html-form-value-using-javascript
http://stackoverflow.com/questions/34313657/html-form-post-an-array-of-objects
也就是：

```html
<form id="form">
    <input type="text" name="group_name">

    <div id="dynamic_form">
        <input type="text" name="members[0][name]">
        <input type="text" name="members[0][date]">

        <input type="text" name="members[1][name]">
        <input type="text" name="members[1][date]">

        <input type="text" name="members[2][name]">
        <input type="text" name="members[2][date]">
    </div>
</form>
```

```js
{
  "group_name": "SomeGroup",
  "members": [
    {
      "name": "Alice",
      "date": "01/01/2015"
    },
    {
      "name": "Bob",
      "date": "02/01/2015"
    },
    {
      "name": "Carol",
      "date": "03/01/2015"
    },
  ]
}
```

需要注意的是，这里的索引不一定要按照步长为1，之间不连续也是可以的，只要确保不用一样的就可以了，如果一样的就是表示多维数组了。

另外，如果用members[0].name members[0].date则会将它们按照数组排放，结果如下：

```js
['Alice', 'Bob', 'Carol'], ["01/01/2015","02/01/2015", "03/01/2015"]
```
这个在数据分析里应该有很大的价值。


## Mongoose如何populate子文档里的引用？
http://stackoverflow.com/questions/33273682/mongodb-multiple-populate-subdocuments-not-being-returned
[How to populate a sub-document in mongoose after creating it?](http://stackoverflow.com/questions/13026486/how-to-populate-a-sub-document-in-mongoose-after-creating-it)
```js
.populate('user_id').populate('comment.commentor_id')
```
How to populate a sub-document in mongoose after creating it? 回答了具体的内容。

## Bootstrap 提示消息总数
可以使用badge
[How to make a total count of messages / alerts indicator in Bootstrap?](http://stackoverflow.com/questions/18471141/how-to-make-a-total-count-of-messages-alerts-indicator-in-bootstrap)

## Nunjucks如何格式化Date数据类型
默认当我们从数据库中读取出来的Date数据类型通过Nunjucks渲染出来的格式：`Wed Nov 01 2017 09:21:00 GMT+0800 (China Standard Time) ` 而这往往不太理想，但Nunjucks又没有提供特定功能的过滤器，所以，我们可以使用如下的插件：
* [nunjucks-date](https://www.npmjs.com/package/nunjucks-date)
* [nunjucks-date-filter](https://www.npmjs.com/package/nunjucks-date-filter)
他们使用的方式基本相同，唯一的要注意的就是关于如何获取Nunjucks的环境的问题：

```js
var env = new nunjucks.Environment();
```
在Express.js中是获取不到的，参考：[Custom filters for Nunjucks in Browser](http://stackoverflow.com/questions/21062613/custom-filters-for-nunjucks-in-browser) ，
当我们通过`nunjucks.configured`的时候就会返回`env`对象了，所以代码如下：

```js
var nunjucks = require('nunjucks');
var nunjucksDate = require('nunjucks-date');

//.....
app.set('view engine', 'nunjucks');
nunjucksDate.setDefaultFormat('YYYY-MM-DD');
var env = nunjucks.configure(config.root + '/app/views', {
    autoescape: true,
    express: app
});

nunjucksDate.install(env, 'date');
```
那样我们在nunjucks中就可以直接使用`date`作为过滤器了，当然也可以修改为其他的格式，例如 `date('YYYY')`


## 如何上传文件到服务器（1） - 简单功能
自己写当然可以，不过我们可以使用一些插件来简化问题。
推荐组合：
客户端: [`blueimp-file-upload`](https://bower.io/search/) 搜索`blueimp`
服务端：[`jquery-file-upload-middleware`](https://github.com/aguidrevitch/jquery-file-upload-middleware)

最基本的运用方式：
服务端：

```js
var upload = require('jquery-file-upload-middleware');

  // configure upload middleware
  upload.configure({
      uploadDir: config.root + '/public/uploads',
      uploadUrl: '/uploads',
      imageVersions: {
          thumbnail: {
              width: 80,
              height: 80
          }
      }
  });
  
  // To prevent access to /upload except for post(for security)
  /// Redirect all to home except post 
  app.get('/upload', function( req, res ){
      res.redirect('/');
  });
  
  app.put('/upload', function( req, res ){
      res.redirect('/');
  });
  
  app.delete('/upload', function( req, res ){
      res.redirect('/');
  });
  
  app.use('/upload', function(req, res, next){
      upload.fileHandler({
          uploadDir: function () {
              return config.root + '/public/uploads/'
          },
          uploadUrl: function () {
              return '/uploads'
          }
      })(req, res, next);
  });
```

客户端，最简单的方式：
1. 先安装插件
2. 引用：

```html
<input id="fileupload" type="file" name="files[]" data-url="/upload" multiple>

<script src="/components/blueimp-file-upload/js/vendor/jquery.ui.widget.js"></script>
<script src="/components/blueimp-file-upload/js/jquery.fileupload.js"></script>
<script>$('#fileupload').fileupload({ dataType: 'json' })</script> 
```

## 如何上传文件到服务器（2）- 使用ImageMagicK生成Thumbnail
要根据图片生成预览图，也就是要对图片进行处理，生成新的图片，这里有几个要点：
1. 项目安装:[imagemagick](https://www.npmjs.com/package/imagemagick)，它其实一个wrapper用于调用系统工具(childprocess)的。
2. 系统安装[imagemagick](http://www.imagemagick.org/script/index.php)，第一步安装的wrapper需要有实际的工具去执行，那就需要安装该软件了，如果是在Windows下，记得一定要安装dll版本，例如ImageMagick-7.0.2-6-Q16-x64-dll.exe，而不要选择类似于ImageMagick-7.0.2-6-Q16-x64-static.exe的Static版本
这是因为dll版本会包含原来的一些老的命令行工具，例如：`identify`，`convert`等等， `static`版本的也可以，只不过需要通过`magick.exe identify`的方式来进行，而这和Unix、Linux平台下的ImageMagick方式不一样就会导致找不到工具。

参考：[Cannot create thumbnails](https://github.com/aguidrevitch/jquery-file-upload-middleware/issues/34)

### 可能会出现的错误

1. 为什么我使用了blueimg-jquery-file-upload和jquery-file-upload-expressjs，并没有生成`thumbnail`？
    - 查看配置是否正确

        ```js
            upload.configure({
            uploadDir: __dirname + '/public/uploads',
            uploadUrl: '/uploads',
            imageVersions: {
                thumbnail: {
                    width: 80,
                    height: 80
                }
            }
        });
        ```
    一定要有·thumbnail·的配置，否则就不会生成。

    - 查看imagemageick是否能正确运行，因为即使不能正确运行，也不会直接给出提示信息
        查看方式，按照[imagemagick](https://www.npmjs.com/package/imagemagick)的代码运行，看看是否成功即可，如果运行失败且不是因为文件找不到的原因，那就是`imagemagick`的环境不正确了。

2. 如果系统没有正确安装[imagemagick](http://www.imagemagick.org/script/index.php)，有可能出现哪些错误？
    没有在Mac或其他*nix平台测试，但在Windows平台下，会发生类似于`Error: spawn ENOENT` 错误。


## 关于地图
http://lbs.amap.com/api/lightmap/guide/point/





##
visual studio code live reload： http://stackoverflow.com/questions/30039512/how-to-view-my-html-code-in-browser-with-visual-studio-code

如何使用bower_component
http://stackoverflow.com/questions/18333310/express-js-routing-for-bower-components

cookie and session http://wiki.jikexueyuan.com/project/node-lessons/cookie-session.html

Middleware check if user authenticated : https://scotch.io/tutorials/route-middleware-to-check-if-a-user-is-authenticated-in-node-js

如何在nunjucks模板里访问各种session信息？
https://segmentfault.com/q/1010000003993234/a-1020000003993306
http://jaspreetchahal.org/expressjs-exposing-variables-and-session-to-jade-templates/
res.locals
例如 res.locals.user -> {{ user }}
关于SerializeUser和DeserializeUser的实践
http://stackoverflow.com/questions/10164312/node-js-express-js-passport-js-stay-authenticated-between-server-restart

Github Login https://www.jokecamp.com/tutorial-passportjs-authentication-in-nodejs/

路由保护
https://github.com/jaredhanson/passport/blob/a892b9dc54dce34b7170ad5d73d8ccfba87f4fcf/lib/passport/http/request.js#L74