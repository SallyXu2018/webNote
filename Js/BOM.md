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

## 定时器（计时器）

### window.setInterval（fn,time）；

参数1：函数
参数2：时间--毫秒-----1000毫秒=1秒
执行过程：页面加载完毕后，过了1秒，执行一次函数的代码，又过了一秒，继续执行函数
返回值：就是定时器的Id值

注意：用window.clearInterval（id）;来取消定时器。

```js
//案例1：让两张图片在同一个div里随机摇晃
var timeID="";
        my$("btn1").onclick=function () {
            timeID=window.setInterval(function () {
                //随机数
                var x=parseInt(Math.random()*100+1);//random()----0-1
                var y=parseInt(Math.random()*100+1);
                my$("dv").style.left=x+"px";//记得加px
                my$("dv").style.top=y+"px";
            },500)
        };
        my$("btn2").onclick=function () {
            window.clearInterval(timeID);
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

### window.setTimeout（fn,time）；

参数1：函数
参数2：时间--毫秒-----1000毫秒=1秒

注意：该定时器只执行一次，执行一次后便没有用了。但是定时器仍旧在内存中，需要用window.clearTimeOut（id）来清理内存。



## 三个大的系列:

## offset系列

作用：获取元素的相关的样式属性的值

元素的样式属性是无法直接通过：对象.style.属性在季节来获取的（样式在style属性中设置）

- offsetWidth:获取元素的宽（有边框）
- offsetHeight:获取元素的高（有边框）
- offsetLeft:获取元素距离左边位置的值
- offsetTop:获取元素距离上面位置的值

注意：

1没有脱离文档流:offsetLeft、offsetTop父级元素margin+父级元素padding+父级元素的border+自己的margin
2脱离文档流了：offsetLeft、offsetTop主要是自己的left和自己的margin

## scroll系列

- scrollWidth:元素中内容的实际的高度（没有边框）
- scrollHight:元素中内容的实际的宽度（没有边框），如果没有内容或内容不足就是元素的高
- scrollTop:向上卷曲出去的距离
- scrollLeft:向左卷曲出去的距离

```js
function getScroll() {
    //直接返回一个对象
    return{
        left:window.pageXOffset||document.documentElement.scrollLeft||document.body.scrollLeft,
        top:window.pageYOffset||document.documentElement.scrollTop||document.body.scrollTop||0
    };
}
//测试
//onscroll方法，元素的滚动事件
window.onscroll=function (ev) {
    console.log("向左卷曲"+getScroll().left+"-------------向上卷曲"+getScroll().top);

}
```

## client系列

clientWidth:可视区域的宽（没有边框），变宽内部的宽度

clientHeight:可视区域的高（没有边框），变宽内部的高度

clientLeft:左边框的宽度

clientTop:上边框的宽度

## 直接通过document获取元素

### 获取body

console.log(document.body);//获取的是元素--标签

### 获取title

console.log(document.title);//标签中的值

### 获取html

console.log(document.documentElement);

## 案例

### 匀速动画封装

设置任意一个元素移动到指定的位置

```js
function animate1(ele,target) {
    //先清理定时器
    clearInterval(ele.timeID);
    //为防止不断的重新开内存空间，直接使用元素的属性改变其指向来防止定时器不断加赠
    ele.timeID = setInterval(function () {
        //---1获取div的当前位置
        var current = ele.offsetLeft;
        //---2div每次移动多少像素
        var step = 8;
        step=target>current?step:-step;
        //--3每次移动后的距离
        current += step;
        //--5判断移动后的位置是否到达目标位置
        if (Math.abs(target-current)>Math.abs(step)) {
            //--4设置div的目标位置
            ele.style.left = current + "px";
        } else {
            clearInterval(ele.timeID);
            //若目标距离小于移动步数，直接到达目标位置
            ele.style.left = target + "px";
        }
    }, 10);
}
```

### 案例-----鼠标在页面中移动,图片跟着鼠标移动

```js
document.onmouseover=function (e) {
    //鼠标的移动的横纵坐标
    //可视区域的横坐标
    //可视区域的纵坐标
    my$("im").style.left=e.clientX+"px";
    my$("im").style.top=e.clientY+"px";
};
```

### 案例-----完整的轮播图

```js
/* 完整轮播图:
* 1. 根据ul中li个数(图片的个数)动态的创建li,并且加入到ol中,作为小按钮来使用
* 为每个ol中的li添加鼠标进入的事件,(添加事件之前,先把索引保存在每个li的自定义属性中),鼠标进入li的时候做排他功能(背景颜色),移动图片(图片整体移动,移动的ul,每次移动的是一个图片的宽度,图片的宽度就是向宽的宽度),调用的是动画函数,移动ul,移动的是索引值*图片的宽度,并且把索引值存储在一个全局变量中,pic
* 2. 创建li之后,1---设置ol中第一个li有默认的背景颜色,2---把ul中的第一个li克隆一下(无缝连接的效果)追加到ul中所有的li的最后面(无缝效果:页面中的第一个图片和最后一个图片是同一个图片)
*
* 3.左右焦点的div显示和隐藏
* 4.为左右按钮注册点击事件
*  每一次点击右边的按钮,先判断pic的值是不是ul中li的length-1(pic的值最大是5),此时设置pic的值为0,同时设置ul距离左边的left值为0(初始值),此时pic立刻加1,移动ul,用户看到的就是第二个图片
*  设置小按钮的背景颜色
*  左边按钮,需要判断pic值是不是0,如果是0此时pic=5,ul的left为5*图片的宽,立刻pic-1,然后ul移动一张图片,此时用户看到了第五个图片
*
*  5.自动播放在页面加载的时候,启动一个定时器,里面调用的就是右边按钮的点击事件的处理函数
*/
<script>
//获取所有的需要的元素
    var box=my$("box");
    var screen=box.children[0];
    var imgWidth=screen.offsetWidth;
    var ulobj=screen.children[0];
    var olobj=screen.children[1];
//实现12345鼠标经过动画
//声明全局变量，贯穿全部的位置变量
var pic=0;
    //------------------------在olobj中创建li标签，即12345小方快
    //循环遍历ulobj中的li标签（olobj中的li个数与ulobj中的img个数相同）
    for (var i=0;i<ulobj.children.length;i++){
        //创建li标签，追加到olobj中
        var liobj=document.createElement("li");
        olobj.appendChild(liobj);
        liobj.innerHTML=i+1;
        //*********为olobj中的li添加index新属性，为了方便图片滚动时的位置计算
        liobj.setAttribute("index",i);
        //--------------------为每一个olobj中的li标签注册鼠标经过事件
        liobj.onmouseover=function (ev) {
            //-------实现排他功能
            for(var i=0;i<olobj.children.length;i++){
                olobj.children[i].removeAttribute("class");
            }
            this.className="current";

            //-------实现鼠标经过图片滑动功能
            //pic就等于每个olobj的索引值
            pic=this.getAttribute("index");
            animate(ulobj,-pic*imgWidth);
        };
    }
        //默认1方块带有class标签
        olobj.children[0].className="current";
//实现鼠标经过box时的动画效果
        //--------------------------------------注册鼠标经过box的事件
        box.onmouseover=function(){
            my$("arr").style.display="block";
            clearInterval(timeID);
        };
        //--------------------------------------注册鼠标离开box的事件
        box.onmouseout=function () {
            my$("arr").style.display="none";
            timeID=setInterval(f1,1500);
        };
        //--------------------------------------注册鼠标点击右箭头事件
        //****************克隆ulobj中第一个图片放在ulobj的最后
        ulobj.appendChild(ulobj.children[0].cloneNode(true));
        my$("right").onclick=f1;
        function f1() {
// 如果点击到视觉效果最后一张图片时，其实是我们克隆的最后一张图片，再点击时，从最后一张快速跳到第一张进行动画
            if(pic==ulobj.children.length-1){
                pic=0;
                ulobj.style.left=0+"px";
            }
            pic++;
            animate(ulobj,-pic*imgWidth);
            //实现12345小方块的同步
            if(pic==ulobj.children.length-1){
                olobj.children[0].className="current";
                olobj.children[olobj.children.length-1].className="";
            }else {
                //排它功能
                for(var i=0;i<olobj.children.length;i++){
                    olobj.children[i].className="";
                }
                olobj.children[pic].className="current";
            }
        }
        //--------------------------------------注册鼠标点击左箭头事件
//如果点击到第一张图片的时候pic=0,图片立刻跳转到最后一张图片，在进行左滚动动画
        my$("left").onclick=function () {
            if(pic==0){
                pic=5;
                ulobj.style.left=-pic*imgWidth+"px";
            }
            pic--;
            animate(ulobj,-pic*imgWidth);
            //实现12345小方块的同步
            for(var i=0;i<olobj.children.length;i++){
                olobj.children[i].className="";
            }
            olobj.children[pic].className="current";
        };
//实现自动播放效果，其实就是定时器，不断重复右边箭头点击事件
    var timeID=setInterval(f1,1500);
</script>
```

### 案例-----图片跟着鼠标走

```js
//鼠标在页面中移动,图片跟着鼠标移动
document.onmouseover=function (ev) {
    //鼠标的移动的横纵坐标
    //可视区域的横坐标
    //可视区域的纵坐标
    my$("im").style.left=ev.clientX+"px";
    my$("im").style.top=ev.clientY+"px";
};
```

### 封装getscroll函数

```js
function getScroll() {
    return{
        left:window.pageXOffset||document.documentElement.scrollLeft||document.body.scrollLeft,
        top:window.pageYOffset||document.documentElement.scrollTop||document.body.scrollTop||0
    };
}
//测试
window.onscroll=function (ev) {
    console.log("向左卷曲"+getScroll().left+"-------------向上卷曲"+getScroll().top);

}
```

### 变速动画封装

设置任意一个元素移动到指定的位置

```js
function animate2(ele,target) {
    //清理定时器
    clearInterval(ele.timeID);
    ele.timeID=setInterval(function () {
        //获取当前的位置
        var current=ele.offsetLeft;
        //移动的步数
        var step=(target-current)/10;
        step=step>0?Math.ceil(step):Math.floor(step);
        current+=step;
        ele.style.left=current+"px";
        if(current==target){
            //清理定时器
            clearInterval(ele.timeID);
        }
        //测试代码
        console.log("目标位置："+target+",当前位置："+current+",每次移动步数："+step+" ")

    },20)
}
```

### 封装getStyle函数

```js
//获取任意一个元素的任意一个属性样式
function getStyle(ele,attr) {
    return window.getComputedStyle?window.getComputedStyle(ele,null)[attr]:ele.currentStyle[attr];
}
```

### 封装缓动动画增加任意一个属性

```js
//封装缓动动画增加任意一个属性
function animate3(ele,attr,target) {
    //清理定时器
    clearInterval(ele.timeID);
    ele.timeID=setInterval(function () {
        //获取当前的位置
        var current=parseInt(getStyle(ele,attr));
        //移动的步数
        var step=(target-current)/10;
        step=step>0?Math.ceil(step):Math.floor(step);
        current+=step;
        ele.style[attr]=current+"px";
        if(current==target){
            //清理定时器
            clearInterval(ele.timeID);
        }
        //测试代码
        //console.log("目标位置："+target+",当前位置："+current+",每次移动步数："+step+" ")

    },20)
}
```

### 封装缓动动画增加任意多个属性

```js
//封装缓动动画增加任意多个属性
function animate4(ele,json) {
    //清理定时器
    clearInterval(ele.timeID);
    ele.timeID=setInterval(function () {
        var flag=true;//默认 假设全部到达目标
        for(var attr in json){
            //获取当前的位置
            var current=parseInt(getStyle(ele,attr));
            //移动的步数
            var target=json[attr];
            var step=(target-current)/10;
            step=step>0?Math.ceil(step):Math.floor(step);
            current+=step;
            ele.style[attr]=current+"px";
            if(current!=target){
                flag=false;
            }
        }
        if(flag){
            //清理定时器
            clearInterval(ele.timeID);
        }

        //测试代码
        console.log("目标位置："+target+",当前位置："+current+",每次移动步数："+step+" ")
    },20)
}
```

### 封装缓动动画增加任意多个属性和回调函数

```js
//封装缓动动画增加任意多个属性和回调函数
function animate5(ele,json,fn) {
    //清理定时器
    clearInterval(ele.timeID);
    ele.timeID=setInterval(function () {
        var flag=true;//默认 假设全部到达目标
        for(var attr in json){
            //获取当前的位置
            var current=parseInt(getStyle(ele,attr));
            //移动的步数
            var target=json[attr];
            var step=(target-current)/10;
            step=step>0?Math.ceil(step):Math.floor(step);
            current+=step;
            ele.style[attr]=current+"px";
            if(current!=target){
                flag=false;
            }
        }
        if(flag){
            //清理定时器
            clearInterval(ele.timeID);
            if(fn){
                fn();
            }
        }
        //测试代码
        console.log("目标位置："+target+",当前位置："+current+",每次移动步数："+step+" ")
    },20)
}
```

### 封装缓动动画增加任意多个属性、回调函数、层级、透明度

```js
//封装缓动动画增加任意多个属性、回调函数、层级、透明度
function animate5(ele,json,fn) {
    //清理定时器
    clearInterval(ele.timeID);
    ele.timeID=setInterval(function () {
        var flag=true;//默认 假设全部到达目标
        for(var attr in json){
            //判断json中是否为opacity或者zindex属性
            if(attr=="opacity"){
                //获取当前的透明度，并且放大一百倍
                var current=getStyle(ele,attr)*100;
                //设置目标透明度，并且放大一百倍
                var target=json[attr]*100;
                var step=(target-current)/10;
                step=step>0?Math.ceil(step):Math.floor(step);
                current+=step;
                ele.style[attr]=current/100;
            }else if(attr=="zIndex"){
                this.style[attr]=json[attr];
            }else {
                //获取当前的位置
                var current=parseInt(getStyle(ele,attr));
                //移动的步数
                var target=json[attr];
                var step=(target-current)/10;
                step=step>0?Math.ceil(step):Math.floor(step);
                current+=step;
                ele.style[attr]=current+"px";
            }
            if(current!=target){
                flag=false;
            }
        }
        if(flag){
            //清理定时器
            clearInterval(ele.timeID);
            if(fn){
                fn();
            }
        }
        //测试代码
        console.log("目标位置："+target+",当前位置："+current+",每次移动步数："+step+" ")
    },20)
}
```

