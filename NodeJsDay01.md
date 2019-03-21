https://nodejs.org/en/

# 1. Node.js介绍

## 1.1 Node.js是什么

- Node.js is a JavaScript runtime built on Chrome‘s V8 JavaScript engine
  - Node.js不是一门语言
  - Node.js不是库、不是框架
  - Node.js是一个JavaScript运行时环境
  - 简单来讲就是Node.js可以解析和执行JavaScript代码
  - 以前只有浏览器可以解析执行JavaScript代码
  - 也就是说现在的JavaScript可以完全脱离浏览器来运行，一切都归于Node.js
- 浏览器中的 JavaScript
  - EcmaScript
    - 基本的语法
    - if
    - var 
    - function
    - Object
    - Array
  - BOM
  - DOM
- Node.js中的JavaScript
  - 没有**BOM、DOM**
  - EcmaScript
  - 在Node这个JavaScript执行环境中为JavaScript提供了一些服务器级别的操作API
    - 例如文件读写
    - 网络服务的构建
    - 网络通信
    - http服务
    - 等处理。。。
- 构建与Chrome 的 V8 引擎之上
  - 代码只是具有特定格式的字符串而已
  - 引擎可以认识他，引擎可以帮你去解析和执行
  - Google Chrome的V8引擎是目前公认的解析执行JavaScript代码最快的
  - Node.js 的作者把Google Chrome 中的 V8 引擎移植了出来，开发了一个独立的JavaScript运行时环境
- Node.js  uses an event-driven ,non-blocking I/O model that makes it lightweight and efficient
  - event-driven事件驱动
  - non-blocking I/O model 非阻塞IO模型（异步）
  - lightweight and efficient 轻量和高效
  - 随着课程慢慢学习就会明白什么是事件驱动和非阻塞IO模型
- Node.js' package ecosystem ,npm,is the largest ecosystem of open source libraries in the world 
  - npm是世界上最大的开源库生态系统
  - 绝大多数的JavaScript相关的包都存放在npm上，这样做的目的是为了让开发人员方便的去下载使用
  - `npm install jquery`

## 1.2 Node.js 能做什么

- web服务器后台
- 命令行工具
  - npm（node）
  - git（c语音）
  - hexo（node）
- 对于前端开发工程师来说，接触最多的是命令行工具
  - 自己写的很少，主要是是用别人第三方开发的
  - webpack
  - gulp
  - npm

## 1.3 预备知识

- html
- css
- JavaScript
- 简单的命令行操作
  - cd
  - dir 列出目录
  - ls 列出目录
  - mkdir
  - rm 删除文件
- 具有服务端开发经验更佳

## 1.4 参考资料

- JavaScript标准参考教程（alpha）:https://wangdoc.com/javascript/

1.5 课程内容

- B/S编程模型
  - Browser-Server
  - back-end
  - 任何服务端这种BS编程模型都是一样的，和语言无关 
  - Node只是作为我们学习BS编程模型的一个工具而已
- 模块化编程
  - RequireJS
  - SeaJS
  - `@import（’文件路径‘）`
  - 以前认知的JavaScript只能通过`script`标签来加载
  - 在node中可以向`@import()`一样来引用加载JavaScript脚本文件 
- Node常用的API
- 异步编程
  - 回调函数
  - promise
  - async
  - generator
- Express Web开发框架
- EcamScript 6
  - 他只是一个新的语法而已
- 。。。
- 学习node不仅会帮助大家打开服务端黑盒子，同时会帮助你学会以后的前端高级内容
  - Vue.js
  - React.js
  - angular.js



# 2. 起步 

## 2.1 解析执行JavaScript

1.创建编写 JavaScript脚本文件

2.打开终端，定位到脚本文件所属目录

3.输入`node 文件名`执行对应的文件

注意：文件名不要使用`node.js`来命名，也就是说除了`node`这个名字随便起，而且最好也不要使用中文

## 2.2 读写文件

文件的读取

```js
//浏览器中的JavaScript是没有文件操作的能力的
//但是node中的JavaScript具有文件操作的能力

//fs是file-system的简写，就是文件系统的意思
//在node中如果想要进行文件操作，就必须引入fs这个核心模块
//在fs这个核心模块中，就提供了所有的文件操作相关的API
//例如：fs.readFile就是用来读取文件的
//1.使用require方法加载fs核心模块
var fs=require('fs');
//2.读取文件
//第一个参数就是要读取的文件路径
//第二个参数是一个回调函数
//error
//  如果读取失败，error就是错误对象
//  如果读取成功，error就是null
//data
//  如果读取失败，data就是错误对象
//  如果读取成功，error就是读取到的数据

//成功
//  data是数据  error是null
//失败
//  data是undefined没有数据 error是错误对象
fs.readFile('./data/a.txt',function (error,data) {
    //<Buffer 68 65 6c 6c 6f 20 6e 6f 64 65 2e 6a 73>
    //文件中存储的其实都是二进制数据 0 1
    //这里为什么看不到0和1呢？原因是二进制转成十六进制了
    //但是无论是二进制还是十六进制，人类都不认识
    //所以我们可以通过tostring方法把其转为我们认识的字符

    // console.log(error);//一个对象
    // console.log(data);//undefined

    //在这里就可以通过error来确认是否有错误发生
    if(error){
        console.log('读取文件失败了');

    }else {
        console.log(data.toString())
    }
    //
});
```

文件的写入

```js
var fs =require('fs');
//第一个参数：文件的路径
//第二个参数：文件内容
//第三个函数：回调函数
//成功
//  文件写入成功
//  error是null
//失败
//  文件写入失败
//  error是一个错误对象
fs.writeFile('./data/hello>.md','大家好，给大家介绍一下，我是node.js',function (error) {
    if(error){
        console.log('文件写入失败')
    }else {
        console.log('文件写入成功');
    }
});
```

## 2.3 http

很傻的服务

```js
//接下来，我们要干一件使用node很有成就感的一件事
//你可以使用node非常轻松构建一个web服务器
//在node中专门提供了一个核心模块：http
//http这个模块的职责就是帮你创建编写服务器的

//1.加载http核心模块
var http=require('http');
//2.使用http.createSever()方法创建一个web服务器
//返回一个server实例
var server=http.createServer();
//3.服务器要干嘛
//提供服务：对数据的服务
    //发请求
    //接受请求
    //处理请求
    //给个反馈（发送响应）
    //注册request请求事件
    //当客户端请求过来，就会自动触发服务器的request请求事件，然后执行第二个参数：回调处理函数
server.on('request',function () {
    console.log('收到客户端请求了')
});
//4.绑定端口号，启动服务器
server.listen(3000,function () {
    console.log('服务器启动成功了，可以通过服务器http://127.0.0.1:3000/来进行访问')
});
```

很傻的服务升级有响应

```js
var http=require('http');
var server=http.createServer();
//request请求事件处理函数，需要接受两个参数
//request 请求对象
    //请求对象可以用来获取客户端的一些请求信息，例如请求路径
//response 响应对象
    //响应对象可以用来给客户端发送响应消息
server.on('request',function (request,response) {
    console.log('收到客户端请求了,请求路径是：'+request.url);
    //    http://127.0.0.1:3000/   请求路径：/
    //    http://127.0.0.1:3000/a   请求路径：/a
    //    http://127.0.0.1:3000/foo/b   请求路径：/foo/b

    //response对象有一个方法：write可以用来给客户端发送响应数据
    //write可以使用多次，但是最后一定要用end来结束响应，否则客户端会一直等待
     response.write('hello0');
     response.write('hello1');
    //告诉客户端，我的话说完了，你可以呈递给用户啦
     response.end();
});
server.listen(3000,function () {
    console.log('服务器启动成功了，可以通过服务器http://127.0.0.1:3000/来进行访问')
});
```

根据不同而路径发送不同的响应

```js
var http=require('http');
//1. 创建server
var server=http.createServer();
//2. 监听request请求事件，设置请求处理函数
server.on('request',function (req,res) {
    // console.log('收到请求了，请求路径是：'+req.url);
    //直接end的同时发送请求
    // res.end('hello world');

    //1.获取请求路径
    //  req.url获取到的是端口号之后的那一段路径
    //2.判断路径处理响应
    var url=req.url;
    // if(url==='/'){
    //     res.end('index page')
    // }else if (url==='/login'){
    //     res.end('login page')
    // }else {
    //     res.end('404 not found')
    // }
    if(url==='/products'){
        var products=[
            {
                name:'apple1',
                price:999
            },
            {
                name:'apple2',
                price:9999
            },
            {
                name:'apple3',
                price:9
            }
        ];
        //响应内容只能是二进制数据或者字符串
        //数字 对象 数组 布尔值都不可以
        res.end(JSON.stringify(products));
    }
});
//3. 绑定端口号，启动服务
server.listen(3000,function () {
    console.log('服务器启动成功，可以访问了')
});
```

# 3. node中的js

## 3.1 EcmaScript

- 没有DOM、BOM

## 3.2 模块系统

- 在 Node 中没有全局作用域的概念
- 在 Node 中，只能通过 require 方法来加载执行多个 JavaScript 脚本文件
- require 加载只能是执行其中的代码，文件与文件之间由于是模块作用域，所以不会有污染的问题
  - 模块完全是封闭的
  - 外部无法访问内部
  - 内部也无法访问外部
- 模块作用域固然带来了一些好处，可以加载执行多个文件，可以完全避免变量命名冲突污染的问题
- 但是某些情况下，模块与模块是需要进行通信的
- 在每个模块中，都提供了一个对象：`exports`
- 该对象默认是一个空对象
- 你要做的就是把需要被外部访问使用的成员手动的挂载到 `exports` 接口对象中
- 然后谁来 `require` 这个模块，谁就可以得到模块内部的 `exports` 接口对象
- 还有其它的一些规则，具体后面讲，以及如何在项目中去使用这种编程方式，会通过后面的案例来处理

格式：

a.js文件内容

```js
var bexports=require('./b');
console.log(bexports.foo);
console.log(bexports.add(10,20));
```

b.js文件内容

```js
var foo='bbb';
exports.foo='hello';
exports.add=function (a,b) {
    return a+b
};
```

### 

## 3.3核心模块

node为JavaScript提供了很多服务器级别的API，这些API绝大多数都被包装到了一个具名的核心模块中了。例如：

- 文件操作的`fs`核心模块
- http服务构建的`http`模块
- `path`路径操作模块
- `os`操作系统信息模块
- 等等。。。

以后只要碰到是核心模块，要想马上使用它，就必须require它

```js
//用来获取机器信息的
var os=require('os');
//获取当前机器的CPU信息
console.log(os.cpus());
//memory 内存
console.log(os.totalmem());

//用来操作路径的
var path=require('path');
//extname extension name
console.log(path.extname('c:/a/b/c/d/hello.txt'));
```

## 3.4 用户自定义模块

- require

require方法有两个作用

```
1.加载文件模块并执行里面的代码
2.拿到被加载文件模块导出的接口对象
```

- exports

```
在每个文件模块中都提供了一个对象：exports
exports默认是一个空对象
你要做的就是把所有需要外部访问的成员挂载到这个exports对象中
```

## 3.5 第三方模块



# 4. web服务器开发

## 4.1 IP地址和端口号

- IP地址用来定位计算机
- 端口号用来定位具体的应用程序
- 一切需要联网通信的软件都会占用一个端口号
- 端口号的范围是从0-65536之间
- 在计算机中有一些默认的端口号，最好不要去使用
  - 例如http服务的80
- 我们在开发过程中使用一些简单好记的就可以了，例如3000、5000等没什么含义
- 可以同时开启多个服务，但一定要确保不同服务占用的端口号不一致

## 4.2 Content-Type

- 服务器最好把每次响应的数据是什么内容类型都告诉客户端，而且要正确的告诉
- 不同的资源对应的 Content-Type 是不一样，具体参照：http://tool.oschina.net/commons
- 对于文本类型的数据，最好都加上编码，目的是为了防止中文解析乱码问题

## 4.3 通过网络发送文件

- 发送的并不是文件，本质上来讲发送是文件的内容
- 当浏览器收到服务器响应内容之后，就会根据你的 Content-Type 进行对应的解析处理

例1：

```js
var http = require('http');
var server = http.createServer();
server.on('request',function (req,res) {
    //在服务器默认发送数据，其实是utf8编码的内容
    //但是浏览器不知道你是utf8编码的内容
    //浏览器在不知道服务器响应内容的编码的情况下会按照当前操作系统的默认编码区解析
    //中文操作系统默认的是gbk
    //解决方法：正确的高速浏览器我发送的内容是什么编码的
    //在http协议中，Content-Type就是用来告诉对方我发给你的是什么数据类型的
    // res.setHeader('Content-Type','text/plain;charset=utf-8');
    // res.end('hello 世界');

    var url=req.url;
    if(url==='/plain'){
        //text/plain就是普通文本
        res.setHeader('Content-Type','text/plain;charset=utf-8');
        res.end('hello 世界')
    }else if(url=='/html'){
        //如果你发送的是html格式的是字符串，则也要告诉浏览器我给你的是text/html格式的内容
        res.setHeader('Content-Type','text/html;charset=utf-8');
        res.end('<p>hello html<a href="">点我</a></p>');
    }
});
server.listen(3000,function () {
   console.log('server is running...')
});
```

例2：

```js
//1.结合fs发送文件中的数据
//2.Content-Type
//http://tool.oschina.net/commons
//Content-Type不同的资源对应的是不一样的
//图片不需要指定编码
//一般只为字
var http = 一般只为字符数据才('http');
var fs=require('fs');
var server = http.createServer();
server.on('request',function (req,res) {
     //    /  index.html
    var url=req.url;
    if(url==='/'){
        //我们要发送的是文件中的内容
        fs.readFile('./resource/index.html',function (err,data) {
           if(err){
               res.setHeader('Content-Type','text/plain;charset=utf-8');
               res.end('文件读取失败，请稍后重试！')
           }else {
               //data默认是二进制数据，可以通过.toString
       //res.end()支持两种数据类型，一种是二进制，一种是字符串
               res.setHeader('Content-Type','text/html;charset=utf-8');
               res.end(data);
           }
        });
    }else if(url==='/dog'){
        //url：统一资源定位符
        //一个url最终是要对应到一个资源的
        fs.readFile('./resource/dog2.jpg',function (err,data) {
            if(err){
                res.setHeader('Content-Type','text/plain;charset=utf-8');
                res.end('文件读取失败，请稍后重试！')
            }else {
                //data默认是二进制数据，可以通过.toString
                //res.end()支持两种数据类型，一种是二进制，一种是字符串
                //图片就不需要指定编码了
                res.setHeader('Content-Type','image/jpeg');
                res.end(data);
            }
        });
    }
});
server.listen(3000,function () {
    console.log('server is running...')
});
```

## 4.4 请求对象 Request

## 4.5 响应对象 Response

## 4.6 在Node中使用模板引擎

## 4.7 统一处理静态资源

## 4.8 服务端渲染



# 5. 案例：留言本

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>留言本</title>
  <!-- 
    浏览器收到 HTML 响应内容之后，就要开始从上到下依次解析，
    当在解析的过程中，如果发现：
      link
      script
      img
      iframe
      video
      audio
    等带有 src 或者 href（link） 属性标签（具有外链的资源）的时候，浏览器会自动对这些资源发起新的请求。
   -->
   <!-- 
      注意：在服务端中，文件中的路径就不要去写相对路径了。
      因为这个时候所有的资源都是通过 url 标识来获取的
      我的服务器开放了 /public/ 目录
      所以这里的请求路径都写成：/public/xxx
      / 在这里就是 url 根路径的意思。
      浏览器在真正发请求的时候会最终把 http://127.0.0.1:3000 拼上

      不要再想文件路径了，把所有的路径都想象成 url 地址
    -->
  <link rel="stylesheet" href="/public/lib/bootstrap/dist/css/bootstrap.css">
</head>

<body>
  <div class="header container">
    <div class="page-header">
      <h1>Example page header <small>Subtext for header</small></h1>
      <a class="btn btn-success" href="/post">发表留言</a>
    </div>
  </div>
  <div class="comments container">
    <ul class="list-group">
      {{each comments}}
      <li class="list-group-item">{{ $value.name }}说：{{ $value.message }} <span class="pull-right">{{ $value.dateTime }}</span></li>
      {{/each}}
    </ul>
  </div>
</body>
</html>
```

post.html

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <link rel="stylesheet" href="/public/lib/bootstrap/dist/css/bootstrap.css">
</head>

<body>
  <div class="header container">
    <div class="page-header">
      <h1><a href="/">首页</a> <small>发表评论</small></h1>
    </div>
  </div>
  <div class="comments container">
    <!-- 
      以前表单是如何提交的？
      表单中需要提交的表单控件元素必须具有 name 属性
      表单提交分为：
        1. 默认的提交行为
        2. 表单异步提交

        action 就是表单提交的地址，说白了就是请求的 url 地址
        method 请求方法
            get
            post
     -->
    <form action="/pinglun" method="get">
      <div class="form-group">
        <label for="input_name">你的大名</label>
        <!--required minlength=   maxlength=这是简单的验证-->
        <input type="text" class="form-control" required minlength="2" maxlength="10"
               id="input_name" name="name" placeholder="请写入你的姓名">
      </div>
      <div class="form-group">
        <label for="textarea_message">留言内容</label>
        <textarea class="form-control" name="message" id="textarea_message" cols="30" rows="10"
                  required minlength="5" maxlength="20"></textarea>
      </div>
      <button type="submit" class="btn btn-default">发表</button>
    </form>
  </div>
</body>

</html>
```

app.js

```js
//app application 应用程序
//把当前模块所有依赖项都声明在文件模块最上面
//为了让目录结构保持统一清晰，所以我们约定，把所有的HTML文件都放到views文件夹中
//我们为了方便统一处理这些静态资源，所以我们约定把所有的静态资源都存放在public目录中
//那些资源能被用户访问，哪些资源不能被用户访问，我们现在可以通过代码来进行非常灵活的控制
//  /  index.html
//  public 整个public目录中的资源都被允许访问
var http=require('http');
var fs=require('fs');
var template=require('art-template');
var url=require('url');

//  /pinglun?name=对鸡内金&message=得金龟
//对于这种表单提交的请求路径，由于其中具有用户动态填写的内容
//所以你不可能通过去判断完整的URL路径来处理这个请求
//结论：对于我们来讲，其实只需要判定，如果你的请求路径是/pinglun的时候，那我就认为你提交表单的请求过来了
var comments=[
    {
        name:'萨利1',
        massage:'今天天气不错',
        dateTime:'2018-11-25'
    },
    {
        name:'萨利2',
        massage:'今天天气不错',
        dateTime:'2018-11-25'
    },
    {
        name:'萨利3',
        massage:'今天天气不错',
        dateTime:'2018-11-25'
    }
];

http
    .createServer(function (req,res) {
        // 使用url.parse方法将路径解析为一个方便操作的对象
        // 第二个参数为true表示直接将查询字符串转为一个对象（通过query属性来访问）
        var parseObj=url.parse(req.url,true);
        //单独获取不包含查询字符串的的路径部分（该路径不包含？之后的内容）
        var pathname=parseObj.pathname;
        //var url=req.url;
        if(pathname==='/'){
            fs.readFile('./views/index.html',function (err,data) {
                if(err){
                    return res.end('404 not found .')
                }
                var htmlStr=template.render(data.toString(),{
                    comments:comments
                });
                res.end(htmlStr)
            })
        }else if (pathname==='/post'){
            fs.readFile('./views/post.html',function (err,data) {
                if(err){
                    return res.end('404 not found')
                }
                res.end(data)
            })
        } else if(pathname.indexOf('/public/')===0){
            //   /public/css/main.css
            //   /public/js/main.js
            //   /public/lib/jquery.js
            //统一处理
            //  如果路径以/public/开头的，则我认为你要获取public中的某个资源
            //  所以我们就直接可以把请求路径当做文件路径来直接获取
            fs.readFile('.'+pathname,function (err,data) {
                if(err){
                    return res.end('404 not found .')
                }
                res.end(data)
            })
        }else if(pathname==='/pinglun'){
            //注意：这个时候无论/pinglun?xxx之后是什么，我的pathname是不包含？之后的那个路径
            //一次请求对应一次响应，响应结束这次请求也就结束了
            //res.end(JSON.stringify(parseObj.query));

            //我们已经使用URL模块的parse方法把请求路径中的查询字符串给解析成一个对象了
            //所以 接下来要做的
            //      1.获取表单提交的数据parseObj.query
            //      2.将当前时间日期添加到数据对象中，然后存储到数组中
            //      3.让用户重定向跳转到首页 /
            //          当用户重新请求/的时候，我数组中的数据已经发生变化了，所以用户看到的页面也就变了
            var comment=parseObj.query;
            comment.dataTime='2017-11-10 12:11:11';
            comments.unshift(comment);
            //服务端这个时候已经把数据存储好了，接下来就是让用户重新请求/首页，就可以看到最新的留言内容了

            //如何通过服务器让客户端重定向？
            //1.状态码设置为302临时重定向
            //      statusCode
            //2.在响应头中通过location告诉客户端往哪儿重定向
            //      setHeader
            //如果客户端发现收到服务器响应的状态码是302就会自动去响应头中找location，然后对该地址发送新的请求
            //所以你就能看到客户端自动跳转了
            res.writeHead(302,{'Location':'/'});
            res.end();
        }else {
            //其他的都处理成404
            fs.readFile('./views/404.html',function (err,data) {
                if(err){
                    return res.end('404 not found')
                }
                res.end(data)
            })
        }
})
    .listen(3000,function () {
        console.log('server is running')
    });
```





# 6. Node中的模块系统 

使用node编写应用程序时主要就是在使用：

- EcmaScript语言
  - 和浏览器哦不一样，在node中没有bom和dom
- 核心模块
  - 文件操作的fs
  - http服务的http
  - URL路径操作模块
  - path路径处理模块
  - os操作系统信息
- 第三方模块
  - art-template（不许通过npm下载才可以使用）
- 自己写的模块

## 什么是模块化

- 文件作用域
- 通信规则
  - 加载 require
  - 倒出 

## CommonJS模块规范

在node中的JavaScript还有一个重要的概念，模块系统

- 模块作用域
- 使用require方法来加载模块
- 使用exports接口对象来导出模块中的成员

### 加载 `require`

语法

```JavaScript
var 自定义变量名=require('模块')
```

两个作用：

- 执行被加载模块中的代码
- 得到被加载模块中的`exports`倒出接口对象

#### require方法加载规则

- 优先从缓存加载
- 判断模块标识

```JavaScript
// 如果是非路径形式的模块标识
// 路径形式的模块：
//  ./ 当前目录，不可省略
//  ../ 上一级目录，不可省略
//  /xxx 几乎不用
//  d:/a/foo.js 几乎不用
//  首位的 / 在这里表示的是当前文件模块所属磁盘根路径
//  .js 后缀名可以省略
// require('./foo.js')

// 核心模块的本质也是文件
// 核心模块文件已经被编译到了二进制文件中了，我们只需要按照名字来加载就可以了
// require('fs')
// require('http')

// 第三方模块
// 凡是第三方模块都必须通过 npm 来下载
// 使用的时候就可以通过 require('包名') 的方式来进行加载才可以使用
// 不可能有任何一个第三方包和核心模块的名字是一样的
// 既不是核心模块、也不是路径形式的模块
//    先找到当前文件所处目录中的 node_modules 目录
//    node_modules/art-template
//    node_modules/art-template/package.json 文件
//    node_modules/art-template/package.json 文件中的 main 属性
//    main 属性中就记录了 art-template 的入口模块
//    然后加载使用这个第三方包
//    实际上最终加载的还是文件

//    如果 package.json 文件不存在或者 main 指定的入口模块是也没有
//    则 node 会自动找该目录下的 index.js
//    也就是说 index.js 会作为一个默认备选项
//    
//    如果以上所有任何一个条件都不成立，则会进入上一级目录中的 node_modules 目录查找
//    如果上一级还没有，则继续往上上一级查找
//    。。。
//    如果直到当前磁盘根目录还找不到，最后报错：
//      can not find module xxx
// var template = require('art-template')
```

### 倒出 `exports`

- node中是模块作用域，默认文件所有成员只在当前文件模块中有效
- 对于希望可以被其他模块访问的成员，我们就需要把这些公开的成员都挂载到`exports`接口对象中就可以了

#### 导出多个成员（必须在对象中）

```javascript
exports.a=123;
exports.b='hello';
exports.c=function(){
    console.log('ccc');
}
exports.d={
    foo='bar'
}
```

倒出多个成员也可以这么写：

```javascript
module.exports={
    foo:'bar',
    add:function(){
        
    }
}
```

#### 导出单个成员（拿到的是函数、字符串）

```javascript
module.exports='hello';
```

以下情况会覆盖

```javascript
module.exports='hello';
//以这个为准，后者会覆盖前者
module.exports =function(x,y){
    return x+y;
}
```



#### 原理解析

exports和`module.exports`的一个引用

```javascript
console.log(exports===module.exports)//ture
exports.foo='bar';
//等价于
module.exports.foo='bar'
```

#### exports 和 module.exports 的区别

- 每个模块中都有一个 module 对象
- module 对象中有一个 exports 对象
- 我们可以把需要导出的成员都挂载到 module.exports 接口对象中
- 也就是：`moudle.exports.xxx = xxx` 的方式
- 但是每次都 `moudle.exports.xxx = xxx` 很麻烦，点儿的太多了
- 所以 Node 为了你方便，同时在每一个模块中都提供了一个成员叫：`exports`
- `exports === module.exports` 结果为  `true`s
- 所以对于：`moudle.exports.xxx = xxx` 的方式 完全可以：`expots.xxx = xxx`
- 当一个模块需要导出单个成员的时候，这个时候必须使用：`module.exports = xxx` 的方式
- 不要使用 `exports = xxx` 不管用
- 因为每个模块最终向外 `return` 的是 `module.exports`
- 而 `exports` 只是 `module.exports` 的一个引用
- 所以即便你为 `exports = xx` 重新赋值，也不会影响 `module.exports`
- 但是有一种赋值方式比较特殊：`exports = module.exports` 这个用来重新建立引用关系的
- 之所以让大家明白这个道理，是希望可以更灵活的去用它

### 补充  

#### jQuery 的 each 和 原生的 JavaScript 方法 forEach

- EcmaScript 5 提供的
  - 不兼容 IE 8
- jQuery 的 each 由 jQuery 这个第三方库提供
  - jQuery 2 以下的版本是兼容 IE 8 的
  - 它的 each 方法主要用来遍历 jQuery 实例对象（伪数组）
  - 同时它也可以作为低版本浏览器中 forEach 替代品
  - jQuery 的实例对象不能使用 forEach 方法，如果想要使用必须转为数组才可以使用
  - `[].slice.call(jQuery实例对象)`

#### 301 和 302 状态码区别

- 301 永久重定向，浏览器会记住
- 302 临时重定向



加载规则以及加载机制

循环加载

#### 文件操作路径和模块路径

文件操作路径：

```javascript
// 在文件操作的相对路径中
//    ./data/a.txt 相对于当前目录
//    data/a.txt   相对于当前目录
//    /data/a.txt  绝对路径，当前文件模块所处磁盘根目录
//    c:/xx/xx...  绝对路径
// fs.readFile('./data/a.txt', function (err, data) {
//   if (err) {
//     console.log(err)
//     return console.log('读取失败')
//   }
//   console.log(data.toString())
// })

```

模块操作路径：

```javascript
// 在模块加载中，如果忽略了.，择业时磁盘根路径
 require('/data/foo.js')

//相对路径
require('./data/foo.js')('hello')

//模块加载的路径中的相对路径中不能省略./
```

#### 修改完代码自动重启

使用一个第三方命名行工具，`nodemon`来帮我们解决频繁修改代码重启服务器问题

`nodemon`是一个基于node.js开发的一个第三方命令行工具，我们使用的话死后要独立安装

```shell
npm install --global nodemon
```

安装完毕之后，使用：

```shell
nodemon app.js
```

只要是通过`nodemon app.js`启动服务，他会监视文件的变化，当文件发生变化时，自动帮你重启服务器



## npm

- node package manager

### npm网站

http://www.npmjs.com

### npm命令行工具

只要安装了node就已经安装了npm

可以再命令行中输入`npm --version`查看npm版本

升级npm版本`npm install --global npm`命令

### 常用命令

- npm init
  - npm init -y可以跳过向导，快速生成
- npm install
  - 一次性把dependencies选项中的依赖项全部安装
  - npm i 
- npm install 包名
  - 只下载
  - npm i 包名
- npm insatall --save 包名
  - 下载并且保存依赖项（package.json文件中的dependencies选项
  - npm i -S 包名
- npm uninstall 包名
  - 只删除，如果有依赖项依然保存
  - npm un 包名
- npm uninstall --save 包名
  - 删除的同时也会把依赖信息也去除
  - npm un -S 包名
- npm help
  - 查看使用帮助
- npm 命令 --help
  - 查看指定命令的使用帮助

### 解决npm被墙问题

npm存储包文件的服务器在国外，有时候会被墙，速度很慢。

http://npm.taobao.org

安装淘宝的cnpm，在任意目录下都可执行命令行`npm install --global cnpm`

```shell
#这里还是使用国外的npm服务器
npm install jquery
#这里使用的是淘宝的npm
cnpm install jquery
```

如果不想安装`cnpm`又想使用淘宝的服务器下载：

```shell
npm install jquery --registry=https://registry.npm.taobao.org
```

但是每次手动打参数很麻烦，所以可以把这个选项加入到配置文件中

```shell
npm config set registry https://registry.npm.taobao.org

#查看npm配置信息
npm config list
```

只要经过了上面命令的配置，则以后所有的`npm stall`都会默认通过淘宝服务器下载

## package.json

我们建议每个项目都有一个`package.json`文件（包描述文件，就像产品的说明书一样），给人踏实的感觉。

这个文件可以通过`npm init`的方式来自动初始化出来

然后下载第三方包的时候，如`npm install --save art-template`中有--save，则在`package.json`自动生成引用的具体文件



对于我们目前来讲最有用的是`dependencies`选项，可以用来帮助我们保存第三方包的依赖信息

如果你的`node_modules`删除了也不担心，我们只需要：`npm install`就会自动把`package.json`中的`dependencies`中所有的依赖项都下载回来

- 建议每个项目根目录下都有一个`package.json`文件
- 建议执行`npm install`包名的时候都是加上`--save`这个选项，目的使用来保存依赖信息

# 9.express

- http://expressjs.com

## 安装

```shell
npm install --save express
```

## hello world

```javascript
var express = require('express')
var app = express()
app.get('/',(req,res)=>res.send('hello world !!'))
app.listen(3000,()=>console.log('running'))
```

## 基本路由

get：

```JavaScript
app.get('/',function(req,res){
    res.send('hello world')
})
```

post：

```javascript
app.post('/',function(req,res){
    res.send('got a post request')
})
```



## 静态服务

```javascript
//  /public资源
app.use(express.static('public'))
//  /files资源
app.use(express.static('files'))//直接访问里面的资源

//  /public/xxx
app.use('/static',express.static('public'))

//  /static/xxx
app.use('/static',express.static('public'))//取别名，通过别名访问

app.use('/static',express.static(path.join(__dirname,'public')))
```





## 整体感知

```javascript
//0 安装 npm install --save express
//1 引包
var express =require('express')

//2 创建服务器应用
//		也就是原来的http.createServer
var app=express()

//在express重开发资源就是一个API的事
//公开制定目录
//只要这样做了，就可以直接通过/public/xx的方式来访问public中所有的资源了
app.use('/public/',express.static('./public/'))
app.use('/static/',express.static('./static/'))

//模板引擎，在express中也是一个API的事

//当服务器收到get请求/的时候，执行回调处理函数
app.get('/',function (req,res) {
	res.send('hello express!')
})

app.get('/about',function (req,res) {
	res.send('你好我是about!')
})

//相当于server.listen
app.listen(3000,function(){
	console.log('app is running at port 3000')
})
```

## 在express中配置使用`art-template`模板引擎

- [art-template-github仓库](https://github.com/aui/art-template)
- [art-template官方文档](https://aui.github.io/art-template/)

安装

```shell
npm install --save art-template
npm install --save express-art-template
```

配置

```javascript
//第一个参数：表示当渲染以.art结尾的文件的时候，使用art-template模板引擎
app.engine('html', require('express-art-template'));
```

使用

```javascript
app.get('/',function (req,res) {
    //express默认会去项目中的views目录查找该模板文件
    res.render('index.html')
});
```

如果希望修改默认的`views`视图渲染目录，可以

```javascript
//views不可以更改
app.set('views',render函数的默认路径)
```



## 在express获取表单get请求参数

express内置了一个API，可以直接通过`req.query`来获取

```javascript
req.query
```



## 在express获取表单post请求体数据

在express中没有内置获取表单post请求体的API，这里我们需要使用第三方包：`body-parser`

安装

```shell
npm install --save body-parser
```

配置

```javascript
var express =require('express')
//引包
var bodyParser=require('body-parser')

var app=express()
//配置body-parser
//只要加入这个配置，则在req请求对象上会多出来一个属性
//也就是说你可以直接通过req.body来获取表单post请求体数据
app.use(bodyParser.urlencoded({extended:false}))

app.use(bodyParser.json())
```

使用

```javascript
app.use(function(req,res){
    res.setHeader('Content-Type','text/plain')
    res.write('you posted :\n')
    //通过req.body来获取表单post请求体数据
    res,end(JSON.stringify(req.body	,null,2))
})
```



## crud案例

### 模块化思想

模块如何划分

- 模块职责要单一

### 起步

- 初始化
- 安装模块
- 模板处理

### 路由设计

| 请求方法 | 请求路径         | get 参数 | post 参数                      | 备注             |
| -------- | ---------------- | -------- | ------------------------------ | ---------------- |
| GET      | /studens         |          |                                | 渲染首页         |
| GET      | /students/new    |          |                                | 渲染添加学生页面 |
| POST     | /studens/new     |          | name、age、gender、hobbies     | 处理添加学生请求 |
| GET      | /students/edit   | id       |                                | 渲染编辑页面     |
| POST     | /studens/edit    |          | id、name、age、gender、hobbies | 处理编辑请求     |
| GET      | /students/delete | id       |                                | 处理删除请求     |

### 提取路由模块

router.js

```javascript
/**
 * router.js路由模块
 * 职责
 *  处理路由
 *  根据不同的请求方法+请求路径设置具体的处理函数
 */


var fs=require('fs');
//express提供了一种更好的方式
//专门用来包装路由的
var express=require('express');

//1.创建一个路由器
var router=express.Router();
//2.把路由都挂载到router路由容器中
router.get('/students',function (req,res) {

});
router.get('/students/new',function (req,res) {
    
});
router.post('/students/new',function (req,res) {
  
});
router.get('/students/edit',function (req,res) {

});
router.post('/students/edit',function (req,res) {

});
router.get('/students/delete',function (req,res) {

});
//3.把router倒出
module.exports=router;
```

app.js

```javascript
var router=require('./router');

//把路由容器挂载到app服务中
app.use(router);
```

### 设计操作数据的API文件模块

```javascript
/**
 * student.js
 * 数据操作文件模块
 * 职责：操作文件中的数据，只处理数据，不关心业务
 */

/**
 * 获取所有的学生列表
 * return []
 */
exports.find=function () {
    
};

/**
 * 添加保存学生
 */
exports.save=function () {

};

/**
 * 更新学生
 */
exports.update=function () {

};

/**
 * 删除学生
 */
exports.delete=function () {

};
```

### 自己编写的步骤

- 处理模板
- 开放静态资源
- 配置模板引擎
- 简单路由：/students渲染静态页出来
- 路由设计
- 提取路由模块
- 由于接下来一系列的业务操作，都需要处理文件数据，所以要封装student.js
- 先写好students.js文件结构
  - 查询所有学生列表的API find
  - findByid
  - save
  - updateById
  - deleteById
- 实现具体功能
  - 通过路由收到请求
  - 接收请求中的数据（get、post）
    - req.query
    - req.body
  - 调用数据操作API处理数据
  - 根据操作结果给客户端发送响应
    - res.render
    - res.redirict
- 业务功能顺序
  - 列表
  - 添加
  - 编辑
  - 删除



web开发框架

高度封装了http模块

更加专注于业务，而非底层细节

知其所以然

# 10.增删改查

使用文件来保存数据（锻炼异步代码）

# 11.MongoDB

所有代码都分装好了
