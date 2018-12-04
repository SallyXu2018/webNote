# BOM：浏览器对象模型 

## BOM的概念

BOM(Browser Object Model) 是指浏览器对象模型，浏览器对象模型提供了独立于内容的、可以与浏览器窗口进行互动的对象结构。BOM由多个对象组成，其中代表浏览器窗口的Window对象是BOM的顶层对象，其他对象都是该对象的子对象。

## BOM的顶级对象window

window是浏览器的顶级对象，当调用window下的属性和方法时，可以省略window
注意：window下一个特殊的属性 window.name

## 对话框

- alert()
- prompt()
- confirm()

注意：对话框时系统自带的，无法更改样式，所以一般不用于页面设计。多用于测试页面。

## 页面加载事件

- onload

```js
window.onload = function () {
  // 当页面加载完成执行
  // 当页面完全加载所有内容（包括图像、脚本文件、CSS 文件等）执行
}
```

- onunload

```js
window.onunload = function () {
  // 当用户退出页面时执行
}
```

## Location对象

### location的属性

```js
            console.log(window.location);
            //地址栏上#后面的内容
            console.log(window.location.hash);
            //主机号及端口名
            console.log(window.location.host);
            //主机名
            console.log(window.location.hostname);
            //文件的路径---相对路径
            console.log(window.location.pathname);
            //端口号
            console.log(window.location.port);
            //协议
            console.log(window.location.protocol);
            //搜索的内容
            console.log(window.location.search);
```

### location的方法

```js
        onload=function(){
        	document.getElementById("btn").onclick=function(){
        		//设置跳转的页面地址的
        		location.href="http://www.baidu.com";//属性------------->一定要记住
        		location.assign("http://www.baidu.com")//方法
        		//刷新
        		location.reload();
        		//在当前页面直接替换地址，没有历史记录
        		location.replace("http://www.baidu.com")
        	}
        }
```

## history对象

### history对象的方法

- history.forward（）；
- history.back（）；
- history.go（）；

注意，没啥用处，相当于浏览器的前进和后退

## navigator对象

### navigator对象的属性

```js
//可以判断浏览器的类型
console.log(window.navigator.userAgent);
//判断浏览器所在的系统平台类型
console.log(window.navigator.platform);
```

## BOM中有两个定时器（）计时器

### .setInterval（fn,number）；

参数1：函数
参数2：时间--毫秒-----1000毫秒=1秒
执行过程：页面加载完毕后，过了1秒，执行一次函数的代码，又过了一秒，继续执行函数
返回值：就是定时器的Id值

```js
//案例1：让两张图片在同一个div里随机摇晃
var timeID="";
        my$("btn1").onclick=function () {
            timeID=setInterval(function () {
                //随机数
                var x=parseInt(Math.random()*100+1);//random()----0-1
                var y=parseInt(Math.random()*100+1);
                my$("dv").style.left=x+"px";//记得加px
                my$("dv").style.top=y+"px";
            },500)
        };
        my$("btn2").onclick=function () {
            clearInterval(timeID);
        }
```

```js
//案例2：一闪一闪亮晶晶
<input type="button" value="一闪一闪亮晶晶" id="btn">
<div id="dv" class="dvv"></div>
<script src="../../js/common.js"></script>
<script>
    my$("btn").onclick=function () {
        setInterval(function () {
           my$("dv").innerHTML="<span>☆</span>";
            var x=parseInt(Math.random()*500+1);//random()----0-1
            var y=parseInt(Math.random()*500+1);
            my$("dv").firstElementChild.style.left=x+"px";
            my$("dv").firstElementChild.style.top=y+"px";
        },10)
    }
```
