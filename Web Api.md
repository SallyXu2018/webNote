# DOM：文档对象模型

### 名词的基本概念

##### 文档（document）

把一个html文件（页面）看成一个文档。由于万物皆对象，所以把这个文档看成对象

##### HTML

展示信息，展示对象

##### XML

侧重于存储数据，XML文件也可以是一个对象

##### 元素（element）

页面中所有的标签都是元素，元素可以看成是对象

##### 节点（node）

页面中所有的内容都是节点：有标签、属性、文本

##### 根（root）

##### 树状图（DOM树）

由文档中及文档中所有元素（标签）组成的一个树形机构

把html页面或者是xml文件看成一个文档，文档就是一个对象，这个文档中所有的标签都是元素，元素也可以看成是一个对象，标签（元素、对象）有很多，还有嵌套的关系，组成的这种层次结构，可以模拟成树形结构图，简称：树状图，就是DOM树

##### 根元素：html标签

页面中的顶级对象：document



### 获取元素的两种方式（重点）

- ##### 根据id从整个文档中获取元素---返回的是一个元素对象

document.getElementById("id属性的值")；

- ##### 根据标签的名字获取元素--返回的是元素对象组成的伪数组

document.getElementByTagName("标签的名字")；



### 操作基本标签的属性

src，title，alt，href，id属性

### 操作表单标签属性

name，value，type，checked，selected，disabled，readonly

### 元素的样式操作

对象.style.属性=值；	

对象.className=值；



### 为元素添加时间操作

事件：就是一件事，有事件源、触发和响应



### this关键字

如果是在当前的元素的事件中使用this，那么this就是当前的对象



内置对象：系统自带的

自定义对象	自己写的

浏览器对象：

BOM对象：通过DOM方式获取的元素得到的对象

如：document.getElementsByTagName("标签的名字");

## day1-练习总结

- 凡是成对标签，中间的文本内容设置的时候，都用innerText这个属性的方式
- document.getElementsByTagName("标签的名字");返回的是一个伪数组
  无论获取的是一个标签还是多个标签，最终都是在数组中存储的，这行代码代码的返回值就是一个数组
- 若使用document.getElementsByTagName("标签的名字");来接收image对象，返回的是一个伪数组，没有alt属性，那就获取第一个数组来更改属性
- alt属性是当图片加载不出来挂了显示的文字 title是当鼠标经过图片时所显示出的文字
- 规律： 在表单标签中，如果属性和值只有一个（如checked），并且是这个属性本身，那么在写Js代码，DOM操作的时候，这个属性值，是布尔类型就可以了
- 凡是css中这个属性是多个单词的写法，在Js代码中DOM操作的时候，把-干掉，后面的单词首字母大写即可
- 在js代码中DOM操作的时候，设置元素的类样式，不用class关键字，应该使用className



### 其他的获取元素的总结

前面的两个由的浏览器不支持

- ##### 根据name属性值获取元素------->返回的是元素对象组成的伪数组

document.getElementByName("属性的名字")； 

通过name属性值获取标签-------->表单标签（属于H5）

- ##### 根据类样式的名字来获取元素-------->返回的是元素对象组成的伪数组

document.getElementsByClassName("类型样式的名字")； 

- 根据选择器的方式获取元素----->返回的是一个对象

document.querySelector("选择器的名字")；

- 根据选择器的方式获取元素---->返回的是一个伪数组

document.querySelectorAll("选择器的名字")；



## day2-练习总结

- 禁用文本框，设置disabled属性

- 如何阻止超链接跳转 点击事件return false

- 为鼠标添加进入事件：onmouseover

- 为鼠标添加离开事件：onmouseleave

- 注册获取焦点事件：onfocus

- 注册失去焦点事件：onblur

- innerHTML是可以设置文本内容---------->推荐。innerHTML主要的作用是在标签中设置新的html标签内容，是有标签效果的

- 如何判断该浏览器是否兼容这个属性---->输出值是否为undefined

  ```js
  //兼容代码
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
