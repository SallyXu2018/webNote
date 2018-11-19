DOM：文档对象模型

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



# 兼容代码1（使innerText在IE8中兼容）

```js
//设置任意的标签中的任意文本内容  设置没有返回值
function setInnerText(element,text) {
    //判断这个浏览器是否支持这个属性--------------------------------->undefined
    if(typeof element.textContent=="undefined"){//浏览器不支持
        element.innerText=text;
    }else{//浏览器支持
        element.textContent=text;
    }
}
//获取任意标签中的内容
function getInnerText(element) {
    if(typeof  element.textContent=="undefined"){
        return element.innerText;
    }else {
            return element.textContent;
    }
}
```



# day2-练习总结

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

# 兼容代码2（获取任意一个父级元素的第一个子级元素）

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

# 兼容代码3（获取任意一个父级元素的最后一个子级元素）

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



# day3-练习总结

- element.firstChild-->谷歌火狐获取的是第一个子节点,IE8获取的是第一个子元素
  element.firstElementChild-->谷歌火狐获取的是第一个子元素,IE8不支持
- 第一个节点和第一个元素的获取的代码在IE8中不支持
  最后一个节点和最后一个元素的获取的代码在IE8中不支持
  前一个节点和前一个元素的获取的代码在IE8中不支持
  后一个节点和后一个元素的获取的代码在IE8中不支持
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

# 为元素绑定事件（DOM）的两种方式，不兼容

### 1.对象.addEventListen

为同一个元素绑定多个相同的点击事件
参数1：事件的类型---事件的名字，没有on
参数2：事件处理函数---函数（命名函数，匿名函数）
参数3：布尔类型，目前就写false---诶呦为什么，不解释，明天说er("事件类型"，事件处理函数，false);---IE8不支持

### 2.对象.attachEvent("有on的事件类型"，事件处理函数);---谷歌、火狐不支持

参数1：事件类型---事件名字，有on
参数2：事件处理函数---函数（命名函数，匿名函数）

# 兼容代码4（为任意元素绑定任意的事件）

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



# 元素的相关方法

追加（后面）子元素：.appendChild（）

插入（前面）子元素：.insertBefore（）

替换子元素：.replaceChild（）

移除父级中的第一个子元素：.removerChild（）

