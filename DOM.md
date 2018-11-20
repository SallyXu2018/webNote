# DOM：文档对象模型

# 名词的基本概念

### 文档（document）

把一个html文件（页面）看成一个文档。由于万物皆对象，所以把这个文档看成对象

### HTML

展示信息，展示对象

### XML

侧重于存储数据，XML文件也可以是一个对象

### 元素（element）

页面中所有的标签都是元素，元素可以看成是对象

### 节点（node）

页面中所有的内容都是节点：有标签、属性、文本

### 根（root）

### 树状图（DOM树）

由文档中及文档中所有元素（标签）组成的一个树形机构

把html页面或者是xml文件看成一个文档，文档就是一个对象，这个文档中所有的标签都是元素，元素也可以看成是一个对象，标签（元素、对象）有很多，还有嵌套的关系，组成的这种层次结构，可以模拟成树形结构图，简称：树状图，就是DOM树

### 根元素：html标签

页面中的顶级对象：document

# 操作基本标签的属性

### src，title，alt，href，id属性

### 基本标签的新属性设置

.setAttribute（）；

### 基本标签的新属性获取

.getAttribute（）；

### 基本标签的新属性移除

.removeAttribute（）；

# 操作表单标签属性

name，value，type，checked，selected，disabled，readonly

# 元素的样式操作

对象.style.属性=值；	

对象.className=值；



# 为元素添加事件操作

事件：就是一件事，有事件源、触发和响应

### 点击事件

.onclick=function（）{}

### 鼠标滑进事件

.onmouseover=function （）{}

### 鼠标离开事件

.onmouseleave=function （）{}

# this关键字

如果是在当前的元素的事件中使用this，那么this就是当前的对象

# 对象

内置对象：系统自带的

自定义对象	自己写的

浏览器对象：

BOM对象：通过DOM方式获取的元素得到的对象

如：document.getElementsByTagName("标签的名字");

# day1-练习总结

- 凡是成对标签，中间的文本内容设置的时候，都用innerText这个属性的方式
- document.getElementsByTagName("标签的名字");返回的是一个伪数组
  无论获取的是一个标签还是多个标签，最终都是在数组中存储的，这行代码代码的返回值就是一个数组
- 若使用document.getElementsByTagName("标签的名字");来接收image对象，返回的是一个伪数组，没有alt属性，那就获取第一个数组来更改属性
- alt属性是当图片加载不出来挂了显示的文字 title是当鼠标经过图片时所显示出的文字
- 规律： 在表单标签中，如果属性和值只有一个（如checked），并且是这个属性本身，那么在写Js代码，DOM操作的时候，这个属性值，是布尔类型就可以了
- 凡是css中这个属性是多个单词的写法，在Js代码中DOM操作的时候，把-干掉，后面的单词首字母大写即可
- 在js代码中DOM操作的时候，设置元素的类样式，不用class关键字，应该使用className



# 获取元素的总结

**根据id从整个文档中获取元素--------->返回的是一个元素对象**

document.getElementById("id属性的值")；

**根据标签的名字获取元素-------->返回的是元素对象组成的伪数组**

document.getElementByTagName("标签的名字")；

**根据name属性值获取元素---------->返回的是元素对象组成的伪数组（有的浏览器不支持）**

document.getElementByName("属性的名字")； 

通过name属性值获取标签-------->表单标签（属于H5）

根据类样式的名字来获取元素-------->返回的是元素对象组成的伪数组（有的浏览器不支持）

document.getElementsByClassName("类型样式的名字")； 

根据选择器的方式获取元素----->返回的是一个对象

document.querySelector("选择器的名字")；

根据选择器的方式获取元素---->返回的是一个伪数组

document.querySelectorAll("选择器的名字")；

# day2-练习总结

- 兼容代码1、2（使innerText在IE8中兼容）

- 禁用文本框，设置disabled属性

- 如何阻止超链接跳转 点击事件return false

- 为鼠标添加进入事件：onmouseover

- 为鼠标添加离开事件：onmouseleave

- 注册获取焦点事件：onfocus

- 注册失去焦点事件：onblur

- innerHTML是可以设置文本内容---------->推荐。innerHTML主要的作用是在标签中设置新的html标签内容，是有标签效果的

- 在html标签中添加的自定义属性，如果想要获取这个属性的值，需要调用getAttribute("属性的名字")才能获取到这个属性的值

- 设置自定义属性：setAttribute("属性的名字",属性的值);

- 获取自定义属性的值：getAttribute("属性的名字")

- 移除自定义属性：removeAttribute("属性的名字");，也可以移除元素的自带的属性

- 案例tab切换案例实现

  ```js
  //获取最外面的div
  var box=my$("box");
  //获取第一个div
  var hd=box.getElementsByTagName("div")[0];
  //获取第二个div
  var bd=box.getElementsByTagName("div")[1];
  //获取所有的span标签
  var spans=hd.getElementsByTagName("span");
  //获取所有的li标签===========================================================
  var lists=bd.getElementsByTagName("li");//==================================
  //遍历所有的span标签，添加点击事件
  for(var i=0;i<spans.length;i++){
      //点击之前就把索引保存到span标签中=========================================
      spans[i].setAttribute("index",i);//======================================
      spans[i].onclick=function () {
          //第一件事所有的span的类样式全部移除
          for(var j=0;j<spans.length;j++){
              spans[j].removeAttribute("class");
          }
          //第二件事，当前被点击的span应用类样式
          this.className="current";
  
          //span被点击时获取存储索引的值=========================================
          var num=this.getAttribute("index");//=========================以下全部
          //获取所有的li标签，每个li标签线全部隐藏
          for(var k=0;k<lists.length;k++){
              lists[k].removeAttribute("class");
          }
          //当前被点击的span标签对应的li标签显示
          lists[num].className="current";
      }
  }
  ```

# 节点（node）

页面中所有的内容都是节点：有标签、属性、文本（文字、换行、空格、回车）

节点的属性：（可以使用标签----元素.出来，可以使用属性节点.出来，文本节点.出来）

### nodeType（节点的类型）

 1---标签，2---属性，3---文本

### nodeName（节点的名字）

标签节点---大写的标签名字，节点属性---小写的属性名宁子，文本节点---#text

### nodeValue（节点的值 ）

标签节点---null，属性节点---属性值，文本节点---文本内容

```js
<div id="dv">
    <cspan>这是div中的第一个标签span标签</cspan>
    <p>这是div中的第二个标签p标签</p>
    <ul id="uu">哈哈
        <li>aa</li>
        <li>aabb</li>嘿嘿
        <li id="three">aabbcc</li>呵呵
        <li>aabbccdd</li>
        <li>aabbccddee</li>嘎嘎
    </ul>
</div>
<script>
    //十二行代码都是获取节点和元素的
    //ul
    var ulObj=my$("uu");
    //父级节点
    console.log(ulObj.parentNode);//DIV(id=dv)
    //父级元素
    console.log(ulObj.parentElement);//DIV(id=dv)
    //子节点
    console.log(ulObj.childNodes);//#text LI #text LI #text LI（id=three）#text LI #text LI #text
    //子元素
    console.log(ulObj.children);//LI LI LIi(id=three) LI LI
    console.log("---------------------------------------------------------");
    //第一个子节点------------------------------------------------------>IE8中获取的是子元素
    console.log(ulObj.firstChild);//哈哈
    //第一个子元素------------------------------------------------------>IE8中不支持
    console.log(ulObj.firstElementChild);//LI
    //最后一个子节点---------------------------------------------------->IE8中获取的是子元素
    console.log(ulObj.lastChild);//嘎嘎
    //最后一个子元素------------------------------------------------------>IE8中不支持
    console.log(ulObj.lastElementChild);//LI
    //某个元素的前一个兄弟结点-------------------------------------------->IE8中获取的是子元素
    console.log(my$("three").previousSibling);//嘿嘿
    //某个元素的前一个兄弟元素-------------------------------------------------->IE8中不支持
    console.log(my$("three").previousElementSibling);//LI
    //某个元素的后一个兄弟结点-------------------------------------------->IE8中获取的是子元素
    console.log(my$("three").nextSibling);//呵呵
    //某个元素的后一个兄弟元素-------------------------------------------------->IE8中不支持
    console.log(my$("three").nextElementSibling);//LI
</script>
```

# 元素创建

### document.write("标签的代码及内容");

这种创建方式有缺陷：如果在页面加载完毕后如果用这种方式创建元素，页面上所有内容都会被替换掉

### 对象.innerHTML="标签及代码";

### document.createElement("标签的名字");

# day3-练习总结

- 兼容代码3（获取任意一个父级元素的第一个子级元素）
- 兼容代码4（获取任意一个父级元素的最后一个子级元素）
- element.firstChild-->谷歌火狐获取的是第一个子节点,IE8获取的是第一个子元素
  element.firstElementChild-->谷歌火狐获取的是第一个子元素,IE8不支持
- 第一个节点和第一个元素的获取的代码在IE8中不支持
  最后一个节点和最后一个元素的获取的代码在IE8中不支持
  前一个节点和前一个元素的获取的代码在IE8中不支持
  后一个节点和后一个元素的获取的代码在IE8中不支持
- 兼容代码5（为任意元素绑定任意的事件）
- 兼容代码6（为任意元素解除绑定任意的事件）
- 案例全选和全不选

<div class="wrap">
    <table>
        <thead>
        <tr>
            <th>
                <input type="checkbox" id="j_cbAll"/>
            </th>
            <th>菜名</th>
            <th>饭店</th>
        </tr>
        </thead>
        <tbody id="j_tb">
        <tr>
            <td>
                <input type="checkbox"/>
            </td>
            <td>红烧肉</td>
            <td>田老师</td>
        </tr>
        <tr>
            <td>
                <input type="checkbox"/>
            </td>
            <td>西红柿鸡蛋</td>
            <td>田老师</td>
        </tr>
        </tbody>
    </table>
</div>



```js
//获取全选的这个复选框
var ckAll=my$("j_cbAll");
//获取tbody中所小的的复选框
var cks=my$("j_tb").getElementsByTagName("input");
//点击全选的这个复选框，获取当前状态，然后设置tbody中所有小复选框的状态
ckAll.onclick=function () {
    for(var i=0;i<cks.length;i++){
        cks[i].checked=this.checked;
    }
};
//获取tbody中所小的的复选框,分别注册点击事件
for(var i=0;i<cks.length;i++){
  cks[i].onclick=function () {
      var flag=true;//默认都被选中了
      //判断是否所有的复选框都被选中了
      for(var i=0;i<cks.length;i++){
          if(!cks[i].checked){
              //没选中就进来
              flag=false;
              break;
          }
      }
      //全选的这个复选框的状态就是flag这个变量的值
      ckAll.checked=flag;
  }  
```

- 点击按钮动态创建列表

```js
var zimubiao=["aaaaaaaaaa","bbbbbbbbbb","ccccccccc","ddddddd","eeeeeeeeee","ffffffffffffffffffff"];
			//点击按钮动态的创建列表，把列表添加到div中
			my$("btn").onclick=function(){
				//创建ul，把ul立刻添加到父级元素div中
				var ulObj=document.createElement("ul");
				my$("dv").appendChild(ulObj);
				//动态创建li，加到ul中
				for(var i=0;i<zimubiao.length;i++){
					var liObj=document.createElement("li");
					//设置li中间的文字内容
					liObj.innerHTML=zimubiao[i];
					ulObj.appendChild(liObj);
				//为li添加鼠标进入事件
				liObj.onmouseover=mouseoverHandle;
				//为li添加鼠标离开事件
				liObj.onmouseout=mouseoutHandle;
			}
		}
		function mouseoverHandle(){
			this.style.backgroundColor="pink";
		}
		function mouseoutHandle(){
			this.style.backgroundColor="";
		}
		//如果是用循环的方式添加事件，推荐用命名函数
		//如果不是循环的方式添加事件，推荐使用匿名函数
```

- .appendChild（对象名字）；这个方法是有缺陷的，会无限添加元素

```js
//值创建一个按钮的案例
my$("btn").onclick=function(){
				if(!my$("btn2")){
					var obj=document.createElement("input");
					obj.value="按钮";
					obj.type="button";
					obj.id="btn2";
					my$("dv").appendChild(obj);
				}
			}
```

# 为元素绑定事件（DOM）

### 1.对象.addEventListen("事件类型"，事件处理函数，false);

------------------------------------------------------------------------------------------------------IE8不支持

为同一个元素绑定多个相同的点击事件
参数1：事件的类型---事件的名字，没有on
参数2：事件处理函数---函数（命名函数，匿名函数）
参数3：布尔类型，目前就写false---诶呦为什么，不解释，明天说er("事件类型"，事件处理函数，false);-

这个中调用的的this是 当前绑定的对象

### 2.对象.attachEvent("有on的事件类型"，事件处理函数);

----------------------------------------------------------------------------------------------------谷歌、火狐不支持

参数1：事件类型---事件名字，有on
参数2：事件处理函数---函数（命名函数，匿名函数）

这个中调用的的this是window

### 3.对象.on事件名字=事件处理函数;



# 元素的相关方法

追加（后面）子元素：.appendChild（）

插入（前面）子元素：.insertBefore（）

替换子元素：.replaceChild（）

移除父级中的第一个子元素：.removerChild（）

# 为元素解除绑定事件（DOM）

注意：用什么方式绑定事件，就应该用对应的方式解绑事件

第一种方式：

对象.on事件名字=事件处理函数；----->绑定事件 

对象.on事件名字=null；

第二种方式：

对象.addEventListen("事件类型"，命名函数，false);----->绑定事件 

对象.removeEventListen("事件类型"，命名函数，false);

第三种方式：

对象.attachEvent("有on的事件类型"，命名函数);----->绑定事件 

对象.detachEvent("有on的事件类型"，命名函数);

# 事件冒泡

### 定义

多个元素冒泡，有层次关系，都注册了相同的事件，如果里面的元素的事件触发了,外面的元素的该事件自动触发了----->由内向外

### 如何阻止事件冒泡

window.event.cancelBubble=true;IE8、谷歌支持，火狐不支持
e.stopPropagation();火狐、谷歌、IE11支持，IE8不支持

### 事件有三个阶段

##### 1.事件的捕获阶段：从外向内

##### 2.事件目标阶段

##### 3.事件冒泡阶段：从里向外

##### 注意

- 事件的捕获阶段和冒泡阶段不可以同时出现
- 通过e.eventPhase这个属性可以知道当前的事件是什么阶段的：如果这个属性的值是1----->事件的捕获阶段，2----->事件目标阶段，3----->事件冒泡阶段
- addEventListener中的第三个参数是控制事件阶段的，一般默认都是冒泡阶段false，很少用捕获阶段true

### 为元素绑定事件

addEventListener("没有on的事件类型",事件处理函数,控制事件阶段的)
事件触发过程中，可能会出现事件冒泡的效果，

### 为阻止事件冒泡

1 window.event.cancelBubble=true;谷歌、IE8支持,火狐不支持
window.event就是一个对象，是IE中的标准

2 e.stopPropagation();谷歌、火狐支持，IE8不支持
window.event和e都是事件参数对象，一个是IE标准，一个是火狐的标准
事件参数e在IE8浏览器中是不存在的，此时用window.event来代替

```js
//三个嵌套得div，最外面的div的id为dv1一次嵌套
//同时注册点击事件
var objs=[my$("dv1"),my$("dv2"),my$("dv3")];
//遍历注册事件
objs.forEach(function(e){
   //为每个元素绑定事件
   e.addEventListener("click",function(){
      console.log(this.id+"--->"+e.eventPhase);//通过e.eventPhase这个属性可以知道当前的事件是什么阶段的：如果这个属性的值是1----->事件的捕获阶段，2----->事件目标阶段，3----->事件冒泡阶段
   },false);//addEventListener中的第三个参数是控制事件阶段的，一般默认都是冒泡阶段false，很少用捕获阶段true
});
//输出id结果为321，eventphase结果为322
```

# day4-练习总结

- 案例：为同一个元素绑定多个不相同事件,指向同一个事件处理函数

```js
my$("btn").onclick=f1;
my$("btn").onmouseover=f1;
my$("btn").onmouseout=f1;
function f1(e) {
   console.log(e);
   switch(e.type){
      case "click":alert("aaaa");break;
      case "mouseover":this.style.backgroundColor="hotpink";break;
      case "mouseout":this.style.backgroundColor="white";break;
   }
}
```

- 案例：百度搜索框（搜索时，输入关键字会弹出下拉框提示相应的搜索内容）

```js
var keyWords=["苹果有什么营养","今天多少度","今天穿什么","今天还好吗","你好啊","今日新闻","今日报道","你吃饭了吗","谁最漂亮啊"];
//获取文本框，注册键盘抬起事件
my$("txt").onkeyup=function () {
    //==========bug1，输入多个字的时候删除一个字会出现两个div==============
   //每一次的键盘抬起都判断这个页面中有没有这个div（解决bug1）
   if (my$("dv")){
       //删除一次
      my$("box").removeChild(my$("dv"));
   }
   //console.log("aaaaaa");//测试抬起事件
   //获取文本框输入的内容
   var text=this.value;
          var tempArr=[];//临时数组，存放对应上的数据
   //把文本框输入的内容和数组中每个数据对比
   for(var i=0;i<keyWords.length;i++){
       //是否是最开始出现的
       if(keyWords[i].indexOf(text)==0){
           tempArr.push(keyWords[i]);//追加
      }
   }
   //console.log(tempArr.length);//临时数组有数据
   console.log(tempArr);
   //============bug2，文本框、临时数组都为空时，仍旧有下拉框================
   //如果文本框是空的，临时数组也是空的，不用创建div
   if(this.value.length==0||tempArr.length==0){
       //如果页面中有这个div删除这个div
      if(my$("dv")){
          my$("box").removeChild(my$("dv"))
      }
      return;
   }
   //遍历临时数组，创建div。把div放在名为box的div中
   var dvObj=document.createElement("div");
   my$("box").appendChild(dvObj);
   dvObj.id="dv";
   dvObj.style.width="141px";
   dvObj.style.border="1px solid #ccc";

   //循环遍历临时数组，创建对应的p标签
   for(var i=0;i<tempArr.length;i++){
       //创建p标签
      var pObj=document.createElement("p");
      //把p添加到名为dv的div标签中
      my$("dv").appendChild(pObj);
      setInnerText(pObj,tempArr[i]);
      pObj.style.margin="3px";
      pObj.style.padding=0;
      pObj.style.cursor="pointer";
      //鼠标进入
      pObj.onmouseover=function () {
          this.style.backgroundColor="pink";
      };
      //鼠标离开
      pObj.onmouseout=function (ev) {
          this.style.backgroundColor="";
      };

   }

      };
```







# 兼容代码

### 1 设置任意的标签中的任意文本内容  

设置没有返回值（使innerText在IE8中兼容）

```js
function setInnerText(element,text) {
    //判断这个浏览器是否支持这个属性--------------------------------->undefined
    if(typeof element.textContent=="undefined"){//浏览器不支持
        element.innerText=text;
    }else{//浏览器支持
        element.textContent=text;
    }
}
```

### 2 获取任意标签中的内容

```js
function getInnerText(element) {
    if(typeof  element.textContent=="undefined"){
        return element.innerText;
    }else {
            return element.textContent;
    }
}
```

### 3 获取任意一个父级元素的第一个子级元素

```js
function getFirstElementChild(element) {
    if(element.firstElementChild){//true 支持
        return element.firstElementChild;
    }else{
        var node=element.firstChild;
        while (node&&node.nodeType!=1){
            node=node.nextSibling;
        }
        return node;
    }
}
```

### 4 获取任意一个父级元素的最后一个子级元素

```js
function getLastElementChild(element) {
    if(element.lastElementChild){//true 支持
        return element.lastElementChild;
    }else{
        var node=element.lastChild;
        while (node&&node.nodeType!=1){
            node=node.previousSibling;
        }
        return node;
    }
}
```

### 5 为任意元素绑定任意的事件

```js
function addEventListener(element,type,fn){
	//判断浏览器是否支持这个方法
	if(element.addEventListener){
		element.addEventListener(type,fn,false);
	}else if(element.attachEvent){
		element.attachEvent("on"+type,fn);
	}else{
		element["on"+type]=fn;
	}
}
```

### 6 为任意元素解除绑定任意的事件

```js
function removeEventListener(element,type,fn){
	if(element.removeEventListener){
		element.removeEventListener(type,fn,false);
	}else if(element.detachEvent){
		element.detachEvent(type,fn);
	}else{
		element["on"+type]=null;
	}
}
```

