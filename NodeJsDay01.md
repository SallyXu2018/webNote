

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

## 2.1 hello world

### 2.1.1 解析执行JavaScript

1.创建编写 JavaScript脚本文件

2.打开终端，定位到脚本文件所属目录

3.输入`node 文件名`执行对应的文件

注意：文件名不要使用`node.js`来命名，也就是说除了`node`这个名字随便起，而且最好也不要使用中文

### 2.1.2 读写文件

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

### 2.1.3 http

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

### 3.4 用户自定义模块

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

### 3.4 第三方模块



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
