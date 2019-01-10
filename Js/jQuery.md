# jQuery基本概念

> 学习目标：学会如何使用jQuery，掌握jQuery的常用api，能够使用jQuery实现常见的效果。



## 为什么要学习jQuery？

【01-让div显示与设置内容.html】

使用javascript开发过程中，有许多的缺点：

```javascript
1. 查找元素的方法太少，麻烦。
2. 遍历伪数组很麻烦，通常要嵌套一大堆的for循环。
3. 有兼容性问题。
4. 想要实现简单的动画效果，也很麻烦
5. 代码冗余。
```



## jQuery初体验

【02-让div显示与设置内容.html】

```javascript
$(document).ready(function () {
    $("#btn1").click(function () {
      	//隐式迭代：偷偷的遍历，在jQuery中，不需要手动写for循环了，会自动进行遍历。
        $("div").show(200);
    });

    $("#btn2").click(function () {
        $("div").text("我是内容");
    });
});
```



优点总结：

```javascript
1. 查找元素的方法多种多样，非常灵活
2. 拥有隐式迭代特性，因此不再需要手写for循环了。
3. 完全没有兼容性问题。
4. 实现动画非常简单，而且功能更加的强大。
5. 代码简单、粗暴。
```





## 什么是jQuery?

> jQuery的官网 [http://jquery.com/](http://jquery.com/) 
> jQuery就是一个js库，使用jQuery的话，会比使用JavaScript更简单。

js库：把一些常用到的方法写到一个单独的js文件，使用的时候直接去引用这js文件就可以了。（animate.js、common.js）



我们知道了，jQuery其实就是一个js文件，里面封装了一大堆的方法方便我们的开发，其实就是一个加强版的common.js，因此我们学习jQuery，其实就是学习jQuery这个js文件中封装的一大堆方法。



## jQuery的版本

> 官网下载地址：[http://jquery.com/download/](http://jquery.com/download/)
> jQuery版本有很多，分为1.x 2.x 3.x



大版本分类：

```javascript
1.x版本：能够兼容IE678浏览器
2.x版本：不兼容IE678浏览器
1.x和2.x版本jquery都不再更新版本了，现在只更新3.x版本。

3.x版本：不兼容IE678，更加的精简（在国内不流行，因为国内使用jQuery的主要目的就是兼容IE678）
```



关于压缩版和未压缩版

```javascript
jquery-1.12.4.min.js:压缩版本，适用于生产环境，因为文件比较小，去除了注释、换行、空格等东西，但是基本没有颗阅读性。
jquery-1.12.4.js:未压缩版本，适用于学习与开发环境，源码清晰，易阅读。
```



## jQuery的入口函数

使用jQuery的三个步骤：

```javascript
1. 引入jQuery文件
2. 入口函数
3. 功能实现
```



关于jQuery的入口函数：

```javascript
//第一种写法
$(document).ready(function() {
	
});
//第二种写法
$(function() {
	
});
```



jQuery入口函数与js入口函数的对比

js的入口函数执行要比jQuery的入口函数执行得晚一些

```javascript
1.	JavaScript的入口函数要等到页面中所有资源（包括图片、文件）加载完成才开始执行。
2.	jQuery的入口函数只会等待文档树加载完成就开始执行，并不会等待图片、文件的加载。
```



## jQuery对象与DOM对象的区别（重点）

```javascript
1. DOM对象：使用JavaScript中的方法获取页面中的元素返回的对象就是dom对象。
2. jQuery对象：jquery对象就是使用jquery的方法获取页面中的元素返回的对象就是jQuery对象。
3. jQuery对象其实就是DOM对象的包装集（包装了DOM对象的集合（伪数组））
4. DOM对象与jQuery对象的方法不能混用。
```



DOM对象转换成jQuery对象：【联想记忆：花钱】

```javascript
var $obj = $(domObj);
// $(document).ready(function(){});就是典型的DOM对象转jQuery对象

```



jQuery对象转换成DOM对象：

```javascript
var $li = $(“li”);
//第一种方法（推荐使用）
$li[0]
//第二种方法
$li.get(0)

```



【练习：隔行变色案例.html】



# 选择器

```js
$("s1,s2");//并集选择器

$("s1 s2");//后代选择器

$("s1>s2");//子代选择器

$("s1s2");//交集选择器
```

## 什么是jQuery选择器

jQuery选择器是jQuery为我们提供的一组方法，让我们更加方便的获取到页面中的元素。注意：jQuery选择器返回的是jQuery对象。

jQuery选择器有很多，基本兼容了CSS1到CSS3所有的选择器，并且jQuery还添加了很多更加复杂的选择器。【查看jQuery文档】

jQuery选择器虽然很多，但是选择器之间可以相互替代，就是说获取一个元素，你会有很多种方法获取到。所以我们平时真正能用到的只是少数的最常用的选择器。



## 基本选择器

| 名称       | 用法               | 描述                                 |
| ---------- | ------------------ | :----------------------------------- |
| ID选择器   | $(“#id”);          | 获取指定ID的元素                     |
| 类选择器   | $(“.class”);       | 获取同一类class的元素                |
| 标签选择器 | $(“div”);          | 获取同一类标签的所有元素             |
| 并集选择器 | $(“div,p,li”);     | 使用逗号分隔，只要符合条件之一就可。 |
| 交集选择器 | $(“div.redClass”); | 获取class为redClass的div元素         |

> 总结：跟css的选择器用法一模一样。



## 层级选择器

| 名称       | 用法        | 描述                                                        |
| ---------- | ----------- | :---------------------------------------------------------- |
| 子代选择器 | $(“ul>li”); | 使用>号，获取儿子层级的元素，注意，并不会获取孙子层级的元素 |
| 后代选择器 | $(“ul li”); | 使用空格，代表后代选择器，获取ul下的所有li元素，包括孙子等  |



> 跟CSS的选择器一模一样。

## 过滤选择器

> 这类选择器都带冒号:

| 名称         | 用法                               | 描述                                                        |
| ------------ | ---------------------------------- | :---------------------------------------------------------- |
| :eq（index） | $(“li:eq(2)”).css(“color”, ”red”); | 获取到的li元素中，选择索引号为2的元素，索引号index从0开始。 |
| :odd         | $(“li:odd”).css(“color”, ”red”);   | 获取到的li元素中，选择索引号为奇数的元素                    |
| :even        | $(“li:even”).css(“color”, ”red”);  | 获取到的li元素中，选择索引号为偶数的元素                    |

【案例：隔行变色】

## 筛选选择器(方法)

> 筛选选择器的功能与过滤选择器有点类似，但是用法不一样，筛选选择器主要是方法。

| 名称               | 用法                        | 描述                             |
| ------------------ | --------------------------- | :------------------------------- |
| children(selector) | $(“ul”).children(“li”)      | 相当于$(“ul>li”)，子类选择器     |
| find(selector)     | $(“ul”).find(“li”);         | 相当于$(“ul li”),后代选择器      |
| siblings(selector) | $(“#first”).siblings(“li”); | 查找兄弟节点，不包括自己本身。   |
| parent()           | $(“#first”).parent();       | 查找父亲                         |
| eq(index)          | $(“li”).eq(2);              | 相当于$(“li:eq(2)”),index从0开始 |
| next()             | $(“li”).next()              | 找下一个兄弟                     |
| prev()             | $(“li”).prev()              | 找上一次兄弟                     |

```javascript
【案例：下拉菜单】this+children+mouseenter+mouseleave
【案例：突出展示】siblings+find
【案例：手风琴】next+parent
【案例：淘宝精品】index+eq
```

# 案例

#### 01-下拉菜单

```js
//this+children+mouseenter+mouseleave
$(function () {
    var $li=$(".wrap>ul>li");
    $li.mouseenter(function () {
        //this是DOM对象，children（）找儿子
        $(this).children("ul").show();
    });
    $li.mouseleave(function () {
        $(this).children("ul").hide();
    });

});
```

### mouseenter和mouseover区别

mouseover：凡是经过注册事件对象及其子对象都会触发事件

mouseenter：经过注册事件对象触发事件，经过其子对象不会触发事件，减少了事件触发次数

#### 02-突出展示

```js
//siblings+find
$(function () {
    $(".wrap>ul>li").mouseenter(function () {
        //siblings是寻找他的兄弟们，不包括自己
        $(this).css("opacity","1").siblings("li").css("opacity","0.4");
    });
    $(".wrap").mouseleave(function () {
        //find是找他的后代
        $(this).find("li").css("opacity","1");//后代选择器
    })
})
```

#### 03-手风琴

```js
//next+parent
$(function () {
    $(".groupTitle").click(function () {
        //next是找下一个兄弟，parent是找爸爸
        $(this).next().slideDown(200).parent().siblings().children("div").slideUp(200);
    });

})
```

#### 04-淘宝精品

```js
//index+eq
$(function () {
    $("#left>li").mouseenter(function () {
        //index()：返回的当前元素在所有兄弟里面的索引
        var idx=$(this).index();
        //eq指定下标
        $("#center>li:eq("+idx+")").show().siblings().hide();
    });
    $("#right>li").mouseenter(function () {
        var idx=$(this).index()+9;
        $("#center>li").eq(idx).show().siblings().hide();
    });
})
```









# $的实质：一个函数

#### 以后用$的时候记得跟 $();

#### 参数不同，功能就不同

```js
console.log(typeof $);//实质是function
```

## $的三种用法

#### 1.参数是一个function,入口函数

```js
$(function () {

});
```

#### 2.$(domobj) 把dom对象转换成jQuery对象

```js
$(document).ready(function () {
    
});
```

#### 3.参数还可以是个字符串,用来找对象

```js
//$("div") $("#btn") $(".current")
```



# jQuery操作样式

## css操作

### 设置单个样式

```js
$("li")
    .css("backgroundColor","pink")
    .css("color","hotpink")
    .css("fontSize","32px")
```

### 设置多个样式

```js
$("li").css({
    backgroundColor:"pink",
    color:"hotpink",
    fontSize:"32px"
})
```

### 获取样式

```js
$("li").eq(0).css("fontSize","10px");
$("li").eq(1).css("fontSize","8px");
$("li").eq(2).css("fontSize","6px");
console.log($("li").css("fontSize"));//10px
//隐式迭代：
// 设置操作的时候：会给jq内部的所有对象都设置上相同的值。
// 获取的时候：只会返回第一个元素对应的值。
```

## class操作

### .addClass(name):添加类

### .removeClass(name):移除类

### .hasClass(name):判断类

### .toggleClass(name):切换

### 案例：tab栏的切换

```js
$(function () {
    $(".tab-item").mouseenter(function () {
        $(this).addClass("active").siblings().removeClass("active");
        var idx=$(this).index();
        $(".main").eq(idx).addClass("selected").siblings().removeClass("selected");

    })
})
```

# jQuery操作属性

```
样式：在style里面写的，用css来操作
属性：在里面里面写的，用attr方法操作
```

## attr操作

使用方法和css一样

### 设置单个属性

### 设置多个属性

### 获取属性

## 案例：相册

```js
$(function () {
    $("#imagegallery a").click(function () {
        var src=$(this).attr("href");
        $("#image").attr("src",src);

        var des=$(this).attr("title");
        $("#des").text(des);

        return false;
    })
})
```

## prop操作

在jQuery1.6之后，对于checked、selected、disabled这类boolean类型的属性来说，不能用attr方法，只能用prop方法。

## 案例：全选和全不选

```js
$(function () {
    $("#j_cbAll").click(function () {
        $("#j_tb input").prop("checked",$(this).prop("checked"));

    });
    $("#j_tb input").click(function () {
        var ckall=$("#j_tb input").length;
        var ck=$("#j_tb input:checked").length;
        if(ckall==ck){
            $("#j_cbAll").prop("checked",true)
        }else {
            $("#j_cbAll").prop("checked",false)
        }

    })
})
```

## removeAttr(name):移除某个属性

# jQuery动画

## 三组基本动画

```
show/hide   slideDown/slideUp/slideToggle  fadeIn/fadeOut/fadeToggle
```

## 案例：京东切换栏

```js
$(function () {
    var count=0;
 $(".arrow-right").click(function () {
     count++;
     if(count==$(".slider li").length){
         count=0;
     }
     $(".slider li").eq(count).fadeIn().siblings("li").fadeOut();
 });
    $(".arrow-left").click(function () {
        count--;
        if(count==-1){
            count=$(".slider li").length-1;
        }
        $(".slider li").eq(count).fadeIn().siblings("li").fadeOut();
    })
})
```

## 自定义动画

```js
animate(prop, [speed], [swing/linear], [callback])
//第一个参数：对象，里面可以传需要动画的样式
//第二个参数：speed 动画的执行时间
//第三个参数：动画的执行效果 秋千/匀速
//第四个参数：回调函数
```

## 动画队列与停止动画

在同一个元素上执行多个动画，那么对于这个动画来说，后面的动画会放到动画队列中，等前面的动画执行。

```js
//stop方法：停止动画效果
stop(clearQueue,jumpToEnd)
//第一个参数：是否清除队列
//第二个参数：是否跳转到最终队列即是否跳转到当前动画的最终效果
//stop:停止当前正在执行的动画
```

## 案例：手风琴

```js
$(function () {
    var $li=$("#box li");
    for (var i=0;i<$li.length;i++){
        $li.eq(i).css("backgroundImage","url(../images/"+(i+1)+"-"+(i+1)+".jpg)");
    }
    $("#box li").mouseenter(function () {
        $(this).stop().animate({width:800}).siblings().stop().animate({width:100});
    }).mouseleave(function () {
        $li.stop().animate({width:240})
    })
})
```



# jQuery节点操作

## 创建节点

```
$("<span></span>")
```

## 添加节点

```
append appendTo prepend prependTo after before
```

## 清空节点

```
empty
```

## 删除节点

```
remove
```

## 克隆节点

```
clone
```

## 案例

### 城市选择

```js
$(function () {
    $("#btn1").click(function () {
        $("#src-city>option").appendTo("#tar-city")
    });
    $("#btn2").click(function () {
        $("#src-city").append($("#tar-city>option"));
    });
    $("#btn3").click(function () {
        $("#src-city>option:selected").appendTo("#tar-city")
    });
    $("#btn4").click(function () {
        $("#src-city").append($("#tar-city>option:selected"));
    });
})
```

### 微博发布

```js
$(function () {

    $("#btn").click(function () {
        if($("#txt").val().trim().length==0){
            return 0;
        }
        $("<li></li>").text($("#txt").val()).prependTo("#ul");
        $("#txt").val("");
    })
})
```

### 弹幕效果

```js
$(function () {
    var colors = ["red", "green", "hotpink", "pink", "cyan", "yellowgreen", "purple", "deepskyblue"]
    //注册事件
    $("#btn").click(function () {
        var randomColor = parseInt(Math.random() * colors.length);
        var randomY = parseInt(Math.random() * 400);
        console.log(randomColor+"----------"+randomY);
        $("<span></span>")//创建span
            .text($("#text").val())//设置内容
            .css("color", colors[randomColor])//设置颜色
            .css("left", "1400px")//设置left值
            .css("top", randomY)//设置top值
            .animate({left: -500}, 10000, "linear", function () {
                $(this).remove();
            })//添加动画
            .appendTo("#boxDom");
        $("#text").val("");
    });
    $("#text").keyup(function (e) {
        if(e.keyCode==13){
            $("#btn").click();
        }
    })

})
```

