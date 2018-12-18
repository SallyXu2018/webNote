### 复习

#### 创建对象的三种方式

```js
//对象：特指的某个事物，具有属性和方法，是一组无序属性的集合
//特征----属性
//行为----方法

//创建对象的三种方式
//1.字面量的方式
var per1={
    name:"sally",
    age:18,
    readBook:function () {
        console.log("aaaa");
    }
};
//2.调用系统函数的方式
var per2=new Object();
per2.name="cendy";
per2.age=19;
per2.run=function () {
    console.log("bbb");
};
console.log(per1 instanceof Object);//T
console.log(per2 instanceof Person);//F
//以上两种方式都属于object类型的


//3.自定义构造函数的方式
function Person(name,age) {
    this.name=name;
    this.age=age;
    this.play=function () {
        console.log("ccc");
    };
}
//创建对象--->实例化一个对象的同时对属性进行初始化
var per3=new Person("luna",20);
//1, 开辟空间存储对象
//2,把this值设置为当前的对象
//3,设置属性和方法的值
//4,把this对象返回
console.log(per3 instanceof Person);//T
```

#### 工厂模式创建对象

```js
function createPerson(name,age) {
    var obj=new Object();
    obj.name=name;
    obj.age=age;
    obj.sayHi=function () {
        console.log("oooo");
    };
    return obj;
}
var per=createPerson("sally",18);
console.log(per instanceof Object);
```

#### 自定义构造函数创建对象和工厂模式创建对象异同点

```js
 /*
* 共同点:都是函数,都可以创建对象,都可以传入参数
*
* 工厂模式:
* 函数名是小写
* 有new,
* 有返回值
* new之后的对象是当前的对象
* 直接调用函数就可以创建对象
*
* 自定义构造函数:
* 函数名是大写(首字母)
* 没有new
* 没有返回值
* this是当前的对象
* 通过new的方式来创建对象
* */
```

#### 实例对象和构造函数之间的关系

1. 实例对象是通过构造函数来创建的---创建的过程叫实例化

2. 如何判断对象是不是这个数据类型?

   1) 通过构造器的方式 实例对象.构造器==构造函数名字

   2) 对象 instanceof 构造函数名字

   尽可能的使用第二种方式来识别,为什么?原型讲完再说





## 面向对象编程

### 原型

#### 作用

一：数据共享

```js
/*
* 实例对象中有个属性,__proto__,也是对象,叫原型,不是标准的属性,浏览器使用的
* 构造函数中有一个属性,prototype,也是对象,叫原型,是标准属性,程序员使用
*
* 原型---->__proto__或者是prototype,都是原型对象,
* 原型的作用:共享数据,节省内存空间
* */
```

#### 构造函数、原型对象、实例对象之间的关系

```js
/**
 * 构造函数可以实例化对象
 * 构造函数中有个属性叫做prototype，是构造函数的原型对象
 * 构造函数的原型对象中（prototype）中有个constructor构造器，这个构造器指向的就是自己所有在原型对象所在的构造函数
 * 实例对象的原型对象（__proto__）指向的是该构造函数的原型对象
 * 构造函数的原型对象（prototype）中的方法是可以被实例对象直接访问的
 *
 */
```

#### 什么样的数据是需要写在原型中的？

需要共享的数据写在原型对象中



### 局部变量变成全局变量

```js
//函数的自调用
//一次性函数--声明的同时，直接调用了
(function () {
    console.log("aa");
    var num=10;
})();
console.log(num);//报错
```

页面加载后，这个自调用函数的代码就执行完了
(function (形参) {
​    var num=10;//局部变量
})(实参);

```js
(function (window) {
    window.num=10;
})(window);
console.log(num);
```

### 案例-把随机数对象暴露给Windows成为全局变量

```js
//通过自调用函数长生一个随机数对象，在自调用函数外面，调用该随机数对象方法产生随机数
(function (window) {
    //产生随机数的构造函数
    function Random() {}
    //在原型对象中添加方法
    Random.prototype.getRandom=function (min,max) {
        return Math.floor(Math.random()*(max-min)+min)//0-4
    };
    //把Random对象暴露给顶级对象window--->外部可以直接使用这个对象
    window.Random=Random;
})(window);
var rm=new window.Random;
console.log(rm.getRandom(0,5));
```



### 面向对象游戏案例：贪吃蛇







## 继承









## 函数进阶













## 正则表达式
