# 对象

### js学习中的三中对象

内置对象--------js系统自带的对象(Math\Date\String\Array\Object)

自定义对象-----自己定义的构造函数创建的对象

浏览器对象-----BOM的时候讲

### 定义

有特征（属性）和行为（方法），具体特指的某个事物

一组无序属性的集合的键值对，属性的值可以是任意类型

### 创建对象（三种方式）

- ##### 调用系统的构造函数创建对象

  ```js
  //js实例化对象
  
  var obj=new Object();
  
  //对象有特征----属性和行为
  
  //添加属性-----如何添加属性？  对象.名字=值；
  
  obj.name="小佳"；
  
  obj.age=18;
  
  obj.sex="女";
  
  //添加方法-----如何添加方法？  对象.名字=函数；
  
  obj.eat=function(){
  
  console.log("我喜欢吃榴莲")；
  
  }；
  
  console.log(obj.name);//获取---输出了
  
  obj.eat();
  
  
  ```

- ##### 自定义构造函数创造对象

  函数和构造函数的区别？名字首字母是不是大写

  ```js
  //自定义构造函数
  function Person(name,age) {
      this.name=name;
      this.age=age;
      this.sayHi=function () {
          console.log("im "+this.name+",im "+this.age);
      };
  }
  //创建对象
  //- 创建对象做了四件事：
  //1. 在内存中申请一块空间，存储创建的新对象
  //2. 把this设置为当前的对象
  //3. 设置对象的属性和方法
  //4. 把this这个对象返回
  var per1=new Person("sally",1);
  per1.sayHi();
  ```

- ##### 字面量的方式创建

  ```js
  var obj={};
          obj.name="sally";
          obj.eat=function () {
            console.log("eating");
          };
          obj.eat();
  
          //字面量方式创建对象优化
  var obj1={
              name:"sally",//注意是冒号和逗号
              age:18,
              eat:function () {
                  console.log("eating");
              },
              sayHi:function () {
                  console.log("Hi");
              };
          }
          obj1.eat();
          obj1.sayHi();
  ```

  缺陷：一次性的对象

- ##### 点语法

  对象.名字=值； 

  对象.名字=函数；

  没有什么点什么

- 访问属性的另一种写法

  ```js
  per1["name"]="candy";
  console.log(per1["name"]);
  
  per1.sayHi();
  per1["sayHi"]();
  ```

### 对象不能分别出到底属于哪个类型？

```js
//console.log(对象名 instanceof 构造函数名);
 console.log(per1 instanceof Person);
```

### 如何一次性创建多个对象呢？

把创建对象的代码封装在函数中---->工厂模式创建对象

```js
function createObject(name,age) {
    var person=new Object;
    person.name=name;
    person.age=age;
    person.sayHi=function () {
        console.log("hello,my name is "+this.name+",i'm "+this.age);
    };
    return person;
}
var per1=createObject("sally",18);
per1.sayHi();
var per2=createObject("candy",18);
per2.sayHi();
```
### json（是一种轻量级的数据交换格式）

JSON格式的数据：一般都是成对的，是键值对。一般json格式的数据无论是键还是值都使用双引号括起来的

遍历对象不能通过for循环，无序;可以通过for-in循环

```js
var json={
    "name":"sally",//左键右值
    "age":18,
}
// var key="name";
// console.log(json[key]);//sally
// console.log(json.adg);//undefined js是一门动态性语言

for(var key in json){//key是一个变量，这个变量存储的是这个对象所有属性的名字
    console.log(key+"-------"+json[key]);
}
```



### 内置对象

##### Math（是个函数，不是对象）

Math.PI、Math.E、Math.abs()；绝对值、Math.ceil()；向上取整\Math.floor()；向下取整、Math.max()；最大值、Math.min()；最小值、Math.pow()；幂次方、Math.sqrt()；开根、Math.random()；0-1随机数、Math.pow()；一个数字的多少次方

Math对象下的属性都是静态的；

```js
//自己定义一个方法，实现系统的Max方法
    function MyMath() {
        this.getMax=function () {
            var max=arguments[0];
            for (var i=0;i<arguments.length;i++){
                if(max<arguments[i]){
                    max=arguments[i];
                }
            }
            return max;
        };
    }
    var test=new MyMath();
    var r=test.getMax(10,20,30,53,1000,0,1);
    console.log(r);
```

```js
//随机产生一个十六进制的颜色值
//封装成一个函数
function getColor() {
    var str="#";
    var arr=["0","1","2","3","4","5","6","7","8","9","a","b","c","d","e","f"];
    for (var i=0;i<6;i++){
        var num=parseInt(Math.random()*16);
        str+=arr[num];
    }
    return str;
}
console.log(getColor());
//页面加载的事件
window.onload=function (ev) {
    //在文档中通过ID属性的值查找这个元素的标签，设置该标签的背景颜色
    document.getElementById("aaa").style.backgroundColor=getColor();
}
```

##### Date

```js
var dt=new Date();
dt.getFullYear();
dt.getMonth();//从0开始计算
dt.getDate();
dt.getHours();
dt.getMinutes();
dt.getSeconds();
dt.getDay();
dt.toDateString();//英文格式日期
dt.toLocaleDateString();//数字格式日期
dt.toTimeString();//英文格式时间
dt.toLocaleTimeString();//数字格式日期
dt.valueOf();//毫秒

var dt1=Date.now();
console.log(dt1);//得到的是毫秒数

var dt2=+new Date();
console.log(dt);//毫秒
```

```js
//格式化日期和时间
function getDate(dt) {
    var Y=dt.getFullYear();
    var M=dt.getMonth()+1;
    var D=dt.getDate();
    var h=dt.getHours();
    var m=dt.getMinutes();
    var s=dt.getSeconds();
    M=M<10?"0"+M:M;
    D=D<10?"0"+D:D;
    h=h<10?"0"+h:h;
    m=m<10?"0"+m:m;
    s=s<10?"0"+s:s;
    return Y+"年"+M+"月"+D+"日  "+h+":"+m+":"+s;
}
console.log(getDate(new Date()));
```

##### String（是个对象）

- 字符串可以看成数组，用for进行遍历。但js中没有字符类型。

字符是一个一个的，在别的语言中字符用单引号括起来

在js中字符串可以用单引号也可以用双引号

```js
var str="hello";
str[1]="w";
console.log(str);//字符串可以通过索引访问字符串里的某个值
    //但是是指可以访问---只读
    //设置：是可以改变
    //对象的方式来看待
    var str1="aaaa";
    str1="ccccc";
    console.log(str1);//重新赋值，在堆中重新开空间
```

- 字符串特性：不可变性，字符串的值是不可以改变的

字符串的值之所以看起来改变了，那是因为指向变了，并不是真的值改变了

- 字符串的常用属性：

.length;

.charAt(索引);；返回值是指定索引位置的字符串，超出索引，结果是空字符串

String.fromCharCode(数字值，多个参数)；返回值ASCII码值

.concat(字符串1，字符串2等)；拼接字符串

.indexOf(要找的字符串)；返回要找的字符串的索引，没找到-1

.lastIndexOf(要找的是字符串)；从后往前找，但是索引仍旧是从左向右的方式

.replace(原来的字符串，新的字符串)；用来替换字符串的

.slice(开始的索引a，结束的索引b)；从a的位置开始，到b的位置的前一个位置结束进行截取

.split(要干掉的字符串，切割后留下的个数)；切割后的字符串

.substr(开始位置，个数)；截取后的字符串

.substring(开始的索引，结束的索引)；截取后的字符串，不包含截取后的

.toLocaleLowerCase()；

.toLowerCase();转小写

.toLocaleUpperCase()；

.toUpperCase();转大写

.trim()；切掉字符串两端的空格

```js
//找到这个字符串中，所有o出现的位置
var str="hello wod odd ott fbo nhyo";
var index=0;
var key="o";
while ((index=str.indexOf(key,index))!=-1){
    console.log(index);
    index+=index+key.length;
}
```

```js
//找到这个字符串中每个字符出现了多少次
var str="sajfbJAkSAFvnjGzdvRnjWdkskdcmxs";
//第一步，把所有的字母变成小写
str=str.toLocaleLowerCase();
console.log(str);
//第二步，创建一个空对象，目的把所有的字符作为一个键出现，次数作为值出现在键值对中
var obj={};
//第三步，遍历字符串，获取每个字母
for(var i=0;i<str.length;i++){
    //判断这个obj中有没有这个字母，没有添加到对象中去
    var key=str[i];
    if(obj[key]){//obj[key]就是键值对中的值，判断这个值来确定是否存在这个字母
        obj[key]++;
    }else{//obj中没有该字符，添加进去
        obj[key]=1;
    }
};
for(var key in obj ){
    console.log(key+"这个字母出现了"+obj[key]+"次");
};
```



##### Array（是个对象）

 Array.isArray()；判断是不是数组 incetanceOf关键字

.cancat(数组，数组);拼接多个数组数组

.every(函数)；----->返回值是布尔类型，函数作为参数使用，函数中有三个参数，第一个参数是是元素的值，第二个参数是索引的值，第三个参数是原来的数组（一般来说没用）。

如果数组中的每个元素的值都符合条件，则返回TRUE

```js
var arr=[1000,2000,3000];
var flag=arr.every(function (ele,index) {
    //ele----元素的值
    //index----索引的值
    //c----谁调用了这个方法arr，c就是谁 一般不用
    return ele>2000;//数组中的每个元素都要大于2000才返回true
});
console.log(flag);
```

.filter(函数);返回的是函数中数组里每一个都符合条件的数组

```js
var arr=[1,2,3,4,5,6];
var newarr=arr.filter(function (ele,index) {
    return ele>3;
});
console.log(newarr);

var arr1=[1,0,2,2,34,0,9,7,0,4];
    var newarr1=arr1.filter(function (ele) {
        return ele!=0;
    });
    console.log(newarr1);
```

.push(值);把值追加到数组最后

.pop();删除数组中最后一个值并返回值

.shift();删除数组中第一个值并返回值

.unshift(值);把值追加到数组最前面

.forEach(函数);遍历数组用,相当于for循环

```js
var arr=[1,2,3,4,5,6];
arr.forEach(function (ele,index) {
    console.log(ele+"-------------"+index);
});
```

.indexOf();差某个元素的索引

.lastIndexOf();

.join("字符串");返回一个字符串

```js
var arr=["a","b","c"];
var newarr=arr.join("|");
console.log(newarr);
```

.map(函数);数组中的每个元素都要执行这个函数，返回新的数组

```js
var arr=[1,4,9,16];
arr=arr.map(Math.sqrt);
console.log(arr);
```

.reverse();反转数组

.sort(固定函数);为数组排序，不稳定，要放入固定函数

```js
var arr=[1,4,9,1000,1,-111,16];
arr.sort(function (a,b) {
    if(a>b){
        return 1;
    }else if(a==b){
        return 0;
    }else {
        return -1;
    }
});
console.log(arr);
```

.slice(开始的索引，结束的索引);把截取后的数组的值放在新数组里，不包含结束的索引

.splice(开始的位置，要删除的个数，替换的元素的值);一般用于删除数组中的值、或者是替换元素中、或者是插入元素



##### Object



### 基本包装类型（string number 布尔）

普通变量不能直接调用属性和方法

对象可以直接调用属性或方法

定义：本身是基本类型，但在执行代码过程中，如果这种类型的变量调用了属性或者方法，那么这种类型就不再是基本类型，而是基本包装类型，这个变量也不再是普通变量，而是基本包装对象

```js
var num1=10;//基本类型
var num2=Number("10");//基本类型 没有new
var num3=new Number("10");//基本包装类型
```

如果是一个对象&&true 结果是true

如果是true&&一个对象 结果是对象


