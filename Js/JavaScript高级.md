复习

#### 创建对象的三种方式

```js
//对象：特指的某个事物，具有属性和方法，是一组无序属性的集合
//特征----属性
//行为----方法

//创建对象的三种方式
//1.字面量的方式----->只能创建一个对象(一次只能创建一个)
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

#### 衔接

```js
/*
  * 面向过程和面向对象都是编程的思想,方式不一样
  * 面向过程:凡事都是亲力亲为,所有的代码都要自己写,每一步都要很清楚,注重的是过程
  * 面向对象:执行者成为指挥者,只要找对象,然后让对象做相关的事情,注重的是结果
  * 面向对象的特性:封装,继承,多态
  * 封装；就是代码的封装,把一些特征和行为封装在对象中.
  * 面向对象的编程思想:根据需求,抽象出相关的对象,总结对象的特征和行为,把特征变成属性，行为变成方法,然后定义(js)构造函数,实例化对象,通过对象调用属性和方法,完成相应的需求.---编程的思想
  *
  * 对象:具体特指的某个事物,有特征(属性)和行为(方法)，对象可以看成是一坨无序属性的集合
  *
  * 如何创建对象?
  * 通过调用new Object(),还有{},自定义构造函数
  *
  * 创建对象的方式
  * 1. 调用系统Object()----->创建出来的对象都是Object类型的,不能很明确的指出这个对象是属于什么类型
  * 2. 字面量的方式{}----->只能创建一个对象(一次只能创建一个)
  *
  * 3.工厂模式创建对象----->----->推论---->自定义构造函数的方式
  *   自定义构造函数(优化后的工厂模式)
  *
  *   自定义构造函数创建对象:4件事
  *   1.在内存中申请一块空闲的空间,存储创建的对象
  *   2.this就是当前实例化的对象
  *   3.设置对象中的属性和方法(为对象添加属性和方法,为属性和方法赋值)
  *   4.把创建后的对象返回
  *   都是需要通过new的方式
  *
  * 什么是原型?
  * 构造函数中有一个属性prototype,是原型,程序员使用的
  * 实例对象中有一个属性__proto__,是原型,浏览器使用的,不是很标准的,
  * 实例对象中的__proto__指向的就是该实例对象中的构造函数中的prototype
  * 构造函数中的prototype里面的属性或者方法,可以直接通过实例对象调用
  * 正常的写法:实例对象.__proto__才能访问到构造函数中的prototype中的属性或者方法
  * per.__proto__.eat();//__proto__不是标准的属性
  * per.eat();
  * 原型就是属性,而这个属性也是一个对象
  * Person.prototype--->是属性
  * Person.prototype.属性或者Person.ptototype.方法()
  *
  * 本身在构造函数中定义的属性和方法,当实例化对象的时候,实例对象中的属性和方法都是在自己的空间中存在的,如果是多个对象。这些属性和方法都会在单独的空间中存在,浪费内存空间,所以,为了数据共享,把想要节省空间的属性或者方法写在原型对象中,达到了数据共享，实现了节点内存空间
  *
  * 原型的作用之一:数据共享,节省内存空间
  *
  * 原型的写法:
  * 构造函数.prototype.属性=值
  * 构造函数.prototype.方法=值---->函数.prototype,函数也是对象,所以,里面也有__proto__
  * 实例对象.prototype-------->实例对象中没有这个属性,只有__proto__(暂时的)
  *
  * 简单的原型的写法
  * 缺陷:--->新的知识点---->原型直接指向{}---->就是一个对象,没有构造器
  * 构造函数.prototype={
  * 切记:如果这这种写法,要把构造器加上
  *
  * };
  *
  *
  * 通过原型为内置对象添加原型的属性或者方法----->原因:
  * 系统的内置对象的属性和方法可能不满足现在需求,所以,可以通过原型的方式加入属性或者方法,为了方便开发
  *
  * 为内置对象的原型中添加属性和方法,那么这个内置对象的实例对象就可以直接使用了
  * String.prototype.方法=匿名函数;
  * var str="哈哈";
  * str.方法();---->实例对象可以直接调用原型中的属性或者方法
  * */
```



## 面向对象编程

### 原型（既是属性又是方法）

#### 作用1：数据共享，目的：节省内存空间

```js
/*
* 实例对象中有个属性,__proto__,也是对象,叫原型,不是标准的属性,浏览器使用的
* 构造函数中有一个属性,prototype,也是对象,叫原型,是标准属性,程序员使用
*
* 原型---->__proto__或者是prototype,都是原型对象,
* 原型的作用:共享数据,节省内存空间
* */
```

#### 作用2：为了实现继承，目的：节省内存空间

#### 关于构造函数、实例对象、原型对象、及其属性的一些问题

##### 1.构造函数、原型对象、实例对象之间的关系

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

##### 2.什么样的数据是需要写在原型中的？

需要共享的数据写在原型对象中

##### 3.实例对象和原型对象属性重名问题

实例对象访问这个属性,应该先从实例对象中找,找到了就直接用，找不到就去指向的原型对象中找,找到了就使用,找不到呢?=====undefined

因为JS是一门动态类型的语言,对象没有什么,只要点了,那么这个对象就有了这个东西,没有这个属性,只要对象.属性名字,对象就有这个属性了,但是,该属性没有赋值,所以,结果是:undefined

##### 4.就想改变原型对象中属性的值,怎么办?

直接通过原型对象.属性=值;可以改变

##### 5.局部变量变成全局变量

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

### 案例

#### 1.把随机数对象暴露给Windows成为全局变量

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



#### 2.贪吃蛇

##### 游戏思路

```js
/*
*
* 地图: 宽，高，背景颜色，因为小蛇和食物都是相对于地图显示的,这里小蛇和食物都是地图的子元素,随机位置显示,脱离文档流的,地图也需要脱离文档流--css需要设置:宽,高,背景颜色,脱标
*
* 食物---div元素
* elements--->存储div的数组(将来删除的食物div时候,先从map中删除div,再从数组中移除div)
* 食物:宽,高,背景颜色,横坐标,纵坐标
* 一个食物就是一个对象,这个对象有相应的属性,这个对象需要在地图上显示
* 最终要创建食物的对象,先 有构造函数,并且把相应的值作为参数传入到构造函数中
* 食物要想显示在地图上,食物的初始化就是一个行为
* 1.食物的构造函数--->创建食物对象
* 2.食物的显示的方法-->通过对象调用方法,显示食物,设置相应的样式
* 2.1.1 因为食物要被小蛇吃掉,吃掉后应该再次出现食物,原来的食物就删除了
* 2.1.2 每一次初始化食物的时候先删除原来的食物,然后重新的初始化食物
* 2.1.3 通过一个私有的函数(外面不能调用的函数)删除地图上的食物,同时最开始的时候食物也相应的保存到一个数组中,再从这个数组中把食物删除
* 最后的时候,把食物的构造函数给window下的属性,这样做,外部就可以直接使用这个食物的构造函数了
*
* 小蛇
* 小蛇就是一个对象
* 属性: 每个身体都有宽，高，方向
* 属性:身体分三个部分,每个部分都是一个对象,每个部分都有横纵坐标,背景颜色
* 小蛇要想显示在地图上,先删除之前的小蛇,然后再初始化小蛇(小蛇要移动)--方法
*
* 小蛇要移动---方法
* 思路:把小蛇的头的坐标给小蛇第一部分的身体,第一部分的身体的坐标给下一个部分身体
* 小蛇的头,需要单独的设置:方向
* */
```

##### 游戏代码

```js
<script>
    //自调用函数----食物
    (function () {
        var elements = [];//用来保存每个小方快食物的
        //食物是一个对象，有宽，有高，有背景颜色，有横纵坐标，先定义或构造函数，然后创建对象
        function Food(width, height, color, x, y) {
            this.width = width || 20;
            this.height = height || 20;
            this.color = color || "black";
            this.x = x;
            this.y = y;
        }

        //为原型添加初始化的方法（作用：在页面上显示这个食物）
        //因为食物需要在地图上显示，需要地图这个参数（map--是页面上的.class=map的这个div
        Food.prototype.init = function (map) {
            //先删除这个小食物
            move();
            //创建div
            var div = document.createElement("div");
            //将div添加到map中
            map.appendChild(div);
            //设置div的样式
            div.style.width = this.width + "px";
            div.style.height = this.height + "px";
            div.style.backgroundColor = this.color;
            //先脱离文档流
            div.style.position = "absolute";
            //横纵坐标，随机产生
            this.x = parseInt(Math.random() * (map.offsetWidth / this.width)) * this.width;
            this.y = parseInt(Math.random() * (map.offsetHeight / this.height)) * this.height;
            div.style.left = this.x + "px";
            div.style.top = this.y + "px";
            //把div加入到数组elements中
            elements.push(div);
        };

        //私有函数，删除食物
        function move() {
            //elements中有这个食物
            for (var i = 0; i < elements.length; i++) {
                var ele = elements[i];
                //找到这个子元素的父级元素，然后删除这个元素
                ele.parentNode.removeChild(ele);
                //再次把elements中的这个字元素也要删除
                elements.splice(i, 1);
            }
        }

        //将Food暴露给window，外不可以使用
        window.Food = Food;
    }());

    //自调用函数----小蛇
    (function () {
        var elements = [];//用来存放小蛇的每个部分
        //小蛇的构造函数
        function Snake(width, height, direction) {
            //小蛇的每个部分的身体的宽
            this.width = width || 20;
            this.height = height || 20;
            //小蛇的身体
            this.body = [
                {x: 3, y: 2, color: "red"},//头
                {x: 2, y: 2, color: "orange"},//身体
                {x: 1, y: 2, color: "orange"}//身体
            ];
            this.direction = direction || "right";
        }
        //为原型添加初始化方法
        Snake.prototype.init = function (map) {
            //删除旧的小蛇
            remove();

            //循环遍历创建div
            for (var i = 0; i < this.body.length; i++) {
                //body数组中的每个数组元素都是一个对象
                var obj = this.body[i];
                //创建div
                var div = document.createElement("div");
                //把div添加到map中
                map.appendChild(div);
                //设置div的样式
                div.style.position = "absolute";
                div.style.width = this.width + "px";
                div.style.height = this.height + "px";
                div.style.left = obj.x * this.width + "px";
                div.style.top = obj.y * this.height + "px";
                div.style.backgroundColor = obj.color;

                //方先暂时不管

                //将创建的div添加到数组elements中---目的是为了删除
                elements.push(div);
            }
        };
        //为原型添加方法----小蛇移动
        Snake.prototype.move = function (food, map) {
            //改变小蛇身体坐标
            var i = this.body.length - 1;
            for (; i > 0; i--) {
                this.body[i].x = this.body[i - 1].x;
                this.body[i].y = this.body[i - 1].y;
            }
            //判断方向---改变小蛇头的坐标位置
            switch (this.direction) {
                case "right":
                    this.body[0].x += 1;
                    break;
                case "left":
                    this.body[0].x -= 1;
                    break;
                case "top":
                    this.body[0].y -= 1;
                    break;
                case "bottom":
                    this.body[0].y += 1;
                    break;
            }

            //判断小蛇有没有吃到食物
            //小蛇的头和食物的坐标一致
            var headX=this.body[0].x*this.width;
            var headY=this.body[0].y*this.height;
            if(headX==food.x&&headY==food.y){
                //获取小蛇最后的尾巴
                var last=this.body[this.body.length-1];
                //把小蛇的尾巴复制一个，重新加入到小蛇的body中
                this.body.push({
                    x:last.x,
                    y:last.y,
                    color:last.color
                });
                //把食物删除，重新初始化食物
                food.init(map);
            }
        };
        //删除小蛇的私有函数
        function remove() {
            //获取数组
            var i=elements.length-1;
            for (;i>=0;i--){
                //先从当前的子元素中找到子元素的父元素，然后再删除子元素
                var ele=elements[i];
                //从map地图上删除子元素
                ele.parentNode.removeChild(ele);
                //elements中删除这个元素
                elements.splice(i,1);
            }
        }
        //把snake暴露给window，供外部使用
        window.Snake = Snake;
    }());

    //自调用函数----动画
    (function(){
        //游戏的构造函数
        function Game(map) {
            this.food=new Food;//食物对象
            this.snake=new Snake;//小蛇对象
            this.map=map;//地图
            that=this;//保存当前实例对象到that中
        }
        //为原型添加方法-----游戏初始化
        Game.prototype.init=function () {
            //食物初始化
            this.food.init(this.map);
            //小蛇初始化
            this.snake.init(this.map);
            // setInterval(function () {
            //     that.snake.move(that.food,that.map);
            //     that.snake.init(that.map);
            // },100000000);
            this.runSnake(this.food,this.map);
            this.bindKey();
        };
        //为原型添加方法-----小蛇自动动起来
        Game.prototype.runSnake=function (food,map) {
            //此时的this是调用它的实例对象
            //自动的去移动
            var timeid=setInterval(function () {
                //此时的this是window
                //移动小蛇
                this.snake.move(food,map);
                //初始化小蛇
                this.snake.init(map);
                //横坐标的最大值
                var maxX=map.offsetWidth/this.snake.width;
                //纵坐标的最大值
                var maxY=map.offsetHeight/this.snake.height;
                //小蛇的头的坐标
                var headX=this.snake.body[0].x;
                var headY=this.snake.body[0].y;
                //判断小蛇的头是否撞墙
                if(headX<0||headX>=maxX){
                    clearInterval(timeid);
                    alert("游戏结束")
                }
                if(headY<0||headY>=maxY){
                    clearInterval(timeid);
                    alert("游戏结束")
                }
            }.bind(that),150)//使用bind函数使setinterval中的this变为that
        };
        //为原型添加方法-----获取用户按键，改变小蛇方向
        Game.prototype.bindKey=function () {
          //获取用户按键，改变小蛇方向
          document.addEventListener("keydown",function (e) {
              //这里的this应该是触发keydown的事件的对象----document
              switch (e.keyCode){
                  case 37:this.snake.direction="left";break;
                  case 38:this.snake.direction="top";break;
                  case 39:this.snake.direction="right";break;
                  case 40:this.snake.direction="bottom";break;
              }
          }.bind(that),false)
        };
        window.Game=Game;
    }());

    //外部测试代码
    var game=new Game(document.querySelector(".map"));
    game.init();

    // var fd = new Food;
    // fd.init(document.querySelector(".map"));
    // var snake = new Snake;
    // snake.init(document.querySelector(".map"));
    // setInterval(function () {
    //     snake.init(document.querySelector(".map"));
    //     snake.move(fd,document.querySelector(".map"));
    // },200);


    // fd.init(document.querySelector(".map"));
    // fd.init(document.querySelector(".map"));//？？？？？？？为什么有了food中move函数调用就可以只出现一个小方快
    //console.log(fd.width);
</script>
```



### 原型链

#### 定义

```js
是一种关系，实例对象和原型对象之间的关系，关系是通过（__proto__）来联系的
```

#### 关于原型链指向的一些问题

##### 1.原型的指向是否可以改变？是

构造函数中的this是实例对象

原型对象中方法中的this也是实例对象

```js
实例对象的原型__proto__指向的是该对象所在的构造函数的原型对象；
构造函数的原型对象(prototype)指向如果改变了,实例对象的原型(__proto__)指向也会发生改变；

```

##### 2.如果原型指向改变了,那么就应该在原型改变指向之后添加原型方法

##### 3.原型链最终指向了哪里？

```js
原型最终指向的的是Object的prototype中的__proto__是null
```

推导过程

```js
//实例对象中有__proto__原型
//构造函数中有prototype原型
//prototype是对象
//所以,prototype这个对象中也有__proto__,那么指向了哪里
//实例对象中的__proto__指向的是构造函数的prototype
//所以,prototype这个对象中__proto__指向的应该是某个构造函数的原型prototyp
function Person() {

    }
Person.prototype.eat=function () {
      console.log("吃东西");
    };

 console.log(per.__proto__==Person.prototype);
    console.log(per.__proto__.__proto__==Person.prototype.__proto__);
    console.log(Person.prototype.__proto__==Object.prototype);
    console.log(Object.prototype.__proto__);
//per实例对象的__proto__------->Person.prototype;Person.prototype的__proto__---->Object.prototype;Object.prototype的__proto__是null
```

### 一个神奇的原型链

```js
<script>
  var divObj=document.getElementById("dv");
  console.dir(divObj);
//divObj.__proto__---->HTMLDivElement.prototype的__proto__--->HTMLElement.prototype的__proto__---->Element.prototype的__proto__---->Node.prototype的__proto__---->EventTarget.prototype的__proto__---->Object.prototype没有__proto__,所以,Object.prototype中的__proto__是null

</script>
```

### 面向对象编程思想

面向对象编程思想:根据需求,分析对象,找到对象有什么特征和行为,通过代码的方式来实现需求,要想实现这个需求,就要创建对象,要想创建对象,就应该显示有构造函数,然后通过构造函数来创建对象.,通过对象调用属性和方法来实现相应的功能及需求,即可。

首先JS不是一门面向对象的语言,JS是一门基于对象的语言,那么为什么学习js还要学习面向对象,因为面向对象的思想适合于人的想法,编程起来会更加的方便,及后期的维护....

 面向对象的编程语言中有类(class)的概念(也是一种特殊的数据类型),但是JS不是面向对象的语言,所以,JS中没有类(class),但是JS可以模拟面向对象的思想编程,JS中会通过构造函数来模拟类的概念(class)

### 面向对象的特性

#### 封装

一个值存储在一个变量中--封装

一坨重复代码放在一个函数中--封装

一系列的属性放在一个对象中--封装

一些功能类似的函数(方法)放在一个对象中--封装

好多相类似的对象放在一个js文件中---封装

#### 继承

首先继承是一种关系,类(class)与类之间的关系,JS中没有类,但是可以通过构造函数模拟类,然后通过原型来实现继承

继承也是为了数据共享,js中的继承也是为了实现数据共享

#### 多态

一个对象有不同的行为,或者是同一个行为针对不同的对象,产生不同的结果,要想有多态,就要先有继承,js中可以模拟多态,但是不会去使用,也不会模拟,

## 继承

### 如何实现继承





### 原型的方式继承

为了数据共享,改变原型指向,做到了继承---通过改变原型指向实现的继承；
缺陷:因为改变原型指向的同时实现继承,直接初始化了属性，继承过来的属性的值都是一样的了,所以,这就是问题；
只能重新调用对象的属性进行重新赋值,

解决方案:继承的时候,不用改变原型的指向,直接调用父级的构造函数的方式来为属性赋值就可以了------借用构造函数:把要继承的父级的构造函数拿过来,使用一下就可以了

```js
function Person(name,age,sex,weight) {
  this.name=name;
  this.age=age;
  this.sex=sex;
  this.weight=weight;
}
Person.prototype.sayHi=function () {
  console.log("您好");
};
function Student(score) {
  this.score=score;
}
//希望人的类别中的数据可以共享给学生---继承
Student.prototype=new Person("小明",10,"男","50kg");

var stu1=new Student("100");
console.log(stu1.name,stu1.age,stu1.sex,stu1.weight,stu1.score);
stu1.sayHi();

var stu2=new Student("120");
stu2.name="张三";
stu2.age=20;
stu2.sex="女";
console.log(stu2.name,stu2.age,stu2.sex,stu2.weight,stu2.score);
stu2.sayHi();
```

### 借用构造函数继承

借用构造函数:构造函数名字.call(当前对象,属性,属性,属性....);
解决了属性继承,并且值不重复的问题

```js
function Person(name, age, sex, weight) {
      this.name = name;
      this.age = age;
      this.sex = sex;
      this.weight = weight;
    }
    Person.prototype.sayHi = function () {
      console.log("您好");
    };
    function Student(name,age,sex,weight,score) {
      //借用构造函数
      Person.call(this,name,age,sex,weight);
      this.score = score;
    }
    var stu1 = new Student("小明",10,"男","10kg","100");
    console.log(stu1.name, stu1.age, stu1.sex, stu1.weight, stu1.score);
	var stu2 = new Student("小红",20,"女","20kg","120");
	console.log(stu2.name, stu2.age, stu2.sex, stu2.weight, stu2.score);
```

缺陷:父级类别中的方法不能继承

解决方案:组合继承

### 组合继承

#### 实质

原型继承+借用构造函数继承

```js
function Person(name,age,sex) {
      this.name=name;
      this.age=age;
      this.sex=sex;
    }
    Person.prototype.sayHi=function () {
      console.log("阿涅哈斯诶呦");
    };
    function Student(name,age,sex,score) {
      //借用构造函数:属性值重复的问题
      Person.call(this,name,age,sex);
      this.score=score;
    }
    //改变原型指向----继承
    Student.prototype=new Person();//不传值
    Student.prototype.eat=function () {
      console.log("吃东西");
    };
    var stu=new Student("小黑",20,"男","100分");
    console.log(stu.name,stu.age,stu.sex,stu.score);
    stu.sayHi();
    stu.eat();
    var stu2=new Student("小黑黑",200,"男人","1010分");
    console.log(stu2.name,stu2.age,stu2.sex,stu2.score);
    stu2.sayHi();
    stu2.eat();
```



### 拷贝继承

#### 实质

把一个对象中的属性或者方法直接通过循环遍历的方式复制到另一个对象中

```js
 function Person() {
    }
    Person.prototype.age=10;
    Person.prototype.sex="男";
    Person.prototype.height=100;
    Person.prototype.play=function () {
      console.log("玩的好开心");
    };
    var obj2={};
    //Person的构造中有原型prototype,prototype就是一个对象,那么里面,age,sex,height,play都是该对象中的属性或者方法
for(var key in Person.prototype){
  obj2[key]=Person.prototype[key];
}
console.dir(obj2);
obj2.play();
```



## 函数进阶

（函数也是对象，对象不一定是函数）

```js
	//函数的角色:
    //函数的声明
    function f1() {
      console.log("我是函数");
    }
    f1();
    //函数表达式
    var ff=function () {
      console.log("我也是一个函数");
    };
    ff();
```



### 函数的不同的表现方式

#### 函数声明

```js

   if(true){
      function f1() {
        console.log("哈哈,我又变帅了");
      }
    }else{
      function f1() {
        console.log("小苏好猥琐");
      }
    }
    f1();
```

#### 函数表达式

```js
var ff;
if(true){
  ff=function () {
    console.log("哈哈,我又变帅了");
  };
}else{
  ff=function () {
    console.log("小苏好猥琐");
  };
}
ff();

```

函数声明如果放在if-else的语句中,在IE8的浏览器中会出现问题
以后宁愿用函数表达式,都不用函数声明



### 函数中的this

- 普通函数中的this是谁?-----window
- 对象.方法中的this是谁?----当前的实例对象
- 定时器方法中的this是谁?----window
- 构造函数中的this是谁?-----实例对象
- 原型对象方法中的this是谁?---实例对象

```js
//普通函数-----window
   function f1() {
     console.log(this);
   }
  f1();

//定时器中的this----window
   setInterval(function () {
     console.log(this);
   },1000);

//构造函数-----实例对象
   function Person() {
     console.log(this);

//对象的方法----当前的实例对象
     this.sayHi=function () {
       console.log(this);
     };

//原型中的方法---实例对象
   Person.prototype.eat=function () {
     console.log(this);
     this.sayHi=function () {//对象的方法----当前的实例对象
       console.log(this);
     };
   };
   var per=new Person();
   console.log(per);
   per.sayHi();//对象的方法----当前的实例对象
   per.eat();
```

### 严格模式

```js
"use strict";//严格模式
function f1() {
  console.log(this);//this----->undefined
}
f1();
```

### 函数的调用的不同的方式

```js
//普通函数
function f1() {
    console.log("aaa");
}
f1();

//构造函数---通过new 来调用,创建对象
function F1() {
    console.log("bbb");
}
var f=new F1();

//对象的方法
function Person() {
    this.play=function () {
        console.log("ccc");
    };
}
var per=new Person();
per.play();
```

### 数组中的函数如何调用

```js
function f1() {
    
}
console.log(typeof f1);//function
//函数也是一种数据类型
//数组可以存储任何类型的数据
var arr=[
    function () {
        console.log("快乐");
    },
    function () {
        console.log("开心");
    }
    ,
    function () {
        console.log("健康");
    }
    ,
    function () {
        console.log("安全");
    },
    function () {
        console.log("如意");
    }
];
//回调函数:函数作为参数使用
arr.forEach(function (ele) {
    ele();
});
```

### 方法（重点）

#### apply和call方法的使用

apply和call方法实际上并不在函数这个实例对象中,而是在Function的prototype中

##### apply的使用语法

函数名字.apply(对象,[参数1,参数2,...]);
方法名字.apply(对象,[参数1,参数2,...]);

##### call的使用语法

函数名字.call(对象,参数1,参数2,...);
方法名字.call(对象,参数1,参数2,...);

##### 作用

改变this的指向，只要是想使用别的对象的方法,并且希望这个方法是当前对象的,那么就可以使用apply或者是call的方法改变this的指向

##### 不同的地方

参数传递的方式是不一样的

#### bind方法的使用

##### 使用语法

函数名字.bind(对象,参数1,参数2,...);---->返回值是复制之后的这个函数
方法名字.bind(对象,参数1,参数2,...);---->返回值是复制之后的这个方法

参数可以在复制的时候传进去,也可以在复制之后调用的时候传入进去

##### 作用

来复制一份

```js
function Person(age) {
    this.age=age;
}
Person.prototype.play=function () {
    console.log(this.age+"===>"+this);
};
function Student(age) {
    this.age=age;
}
var per=new Person(10);
var stu=new Student(20);
//复制了一份---->改变了this的指向
var ff=per.play.bind(stu);
ff();//20 object
```

##### bind方法的应用

```js
//通过对象 调用方法 显示随机数
function ShowRandom() {
    this.number=parseInt(Math.random()*10+1);
}
ShowRandom.prototype.show1=function () {
    //改变了定时器中的this的指向了,本来应该是window,现在是实例对象了
    setInterval(this.show2.bind(this),1000);
};
ShowRandom.prototype.show2=function () {
    console.log(this.number);
};
var sr=new ShowRandom();
sr.show1();
```

### 函数中的成员（了解）

name属性：函数的名字,name属性是只读的,不能修改
arguments属性：实参的个数
length属性：函数定义的时候形参的个数
caller属性：调用(f1函数在f2函数中调用的,所以,此时调用者就是f2)

### 高阶函数

#### 函数作为参数使用的例子

函数作为参数的时候,如果是命名函数,那么只传入命名函数的名字,没有括号

```js
function f3(fn) {
    setInterval(function () {
        console.log("a");
        fn();
        console.log("b");
    },1000)
}
f3(function () {
    console.log("ccc");
})
```

#### 函数作为返回值使用的例子

获取某个对象类型是不是你传入的类型

```js
//type--是变量---是参数---"[Object Array]"
//obj--是变量---是参数---"[10,20,30]"
//判断这个对象和传入的类型是不是同一个类型
function Func(type) {
    return function (obj) {
        return Object.prototype.toString.call(obj)==type;
    }
}
var ff=new Func("[object Array]");
var result=ff([10,20,30]);
console.log(result);
```

##### 综合案例

```js
//排序,每个文件都有名字，大小,时间,都可以按照某个属性的值进行排序

//三部电影,电影有名字,大小,上映时间
function File(name,size,time) {
    this.name=name;
    this.size=size;
    this.time=time;
}
var f1 = new File("jack.avi", "400M", "1997-12-12");
var f2 = new File("tom.avi", "200M", "2017-12-12");
var f3 = new File("xiaosu.avi", "800M", "2010-12-12");
var arr = [f1, f2, f3];
function fn(attr) {
    return function getSort(obj1,obj2) {
        //函数作为返回值
        if(obj1[attr]>obj2[attr]){
            return 1;
        }else if(obj1[attr]==obj2[attr]){
            return 0;
        }else {
            return -1;
        }
    }
}
var ff=fn("size");
arr.sort(ff);
for (var i=0;i<arr.length;i++){
    console.log(arr[i].name+"---"+arr[i].size+"---"+arr[i].time);
}
```

### 作用域，作用域链，预解析

```js
//变量---->局部变量和全局变量,
//作用域(变量的使用范围)---->局部作用域和全局作用域
//js中没有块级作用域------一对括号中定义的变量,这个变量可以在大括号外面使用
//函数中定义的变量是局部变量

// 作用域链:变量的使用,从里向外,层层的搜索,搜索到了就可以直接使用了
// 层层搜索,搜索到0级作用域的时候,如果还是没有找到这个变量,结果就是报错

// 预解析:就是在浏览器解析代码之前,把变量的声明和函数的声明提前(提升)到该作用域的最上面
//变量的提升
console.log(num);
var num=100;

//函数的声明被提前了
f1();
function f1() {
    console.log("这个函数,执行了");
}

f2();
f2=function () {
    console.log("小杨好帅哦");
};//报错
```

### 闭包（重点）

概念：函数A中,有一个函数B,函数B中可以访问函数A中定义的变量或者是数据,此时形成了闭包(这句话暂时不严谨)

模式：函数模式的闭包,对象模式的闭包

作用：缓存数据,延长作用域链

优点：缓存数据

缺点：缓存数据

```js
//函数模式的闭包
function f1() {
    var num=10;
    function f2() {
        console.log(num);
    }
    f2();
}
f1();
//对象模式的闭包
function f3() {
    var num=20;
    var obj={
        age:num
    };
    console.log(obj.age);
}
f3();
```

#### 闭包案例

朋友圈某活动点赞小案例

```js
function my$(tagName) {
    return document.getElementsByTagName(tagName);
}
//闭包缓存数据
function getValue() {
    var value=2;
    return function () {
        //每点击一次的时候，都应当改变当前点击的value值
        this.value="赞("+(value++)+")";
    }
}
//获取所有的按钮
var btnObjs=my$("input");
//循环遍历每个按钮，注册点击事件
for (var i=0;i<btnObjs.length;i++){
    //注册点击事件
    btnObjs[i].onclick=getValue();
}
```

### 沙箱

是一个环境（黑盒），在一个虚拟的环境中模拟真实世界做实验。实验结果和真实世界的结果是一样，但是不会影响真实世界。

作用：避免命名冲突

### 递归（重点）

函数中调用函数自己，此时就是递归。递归一定要有结束条件，否则死循环。

递归尽量不要用，效率极低。

#### 案例1：求n个数字累积和

```js
function getSum(x) {
    if(x==1){
        return x=1;
    }
    return x+getSum(x-1);
}
console.log( getSum(5)) 
   /*
   * 执行过程:
   * 代码执行getSum(5)--->进入函数,此时的x是5,执行的是5+getSum(4),此时代码等待
   * 此时5+getSum(4),代码先不进行计算,先执行getSum(4),进入函数,执行的是4+getSum(3),等待, 先执行的是getSum(3),进入函数,执行3+getSum(2),等待,先执行getSum(2),进入函数,执行 2+getSum(1);等待, 先执行getSum(1),执行的是x==1的判断,return 1,所以,
   * 此时getSum(1)的结果是1,开始向外走出去
   * 2+getSum(1) 此时的结果是:2+1
   * 执行:
   * getSum(2)---->2+1
   * 3+getSum(2) 此时的结果是3+2+1
   * 4+getSum(3) 此时的结果是4+3+2+1
   * 5+getSum(4) 此时的结果是5+4+3+2+1
   * 结果:15
   * */
```

#### 案例2：求一个数字各个位数上的数字的和

```js
//递归案例:求一个数字各个位数上的数字的和:  123   --->6 ---1+2+3
function getEverySum(x) {
    if(x<10){
        return x;
    }
    return x%10+getEverySum(parseInt(x/10));
}
console.log(getEverySum(12345));
```

#### 案例3：求斐波那契数列

```js
    function getFib(x) {
        if(x==1||x==2){
            return 1;
        }
        return getFib(x-1)+getFib(x-2);
    }
    console.log(getFib(12));
</script>
```





浅拷贝

拷贝就是复制,就相当于把一个对象中的所有的内容,复制一份给另一个对象,直接复制,或者说,就是把一个对象的地址给了另一个对象,他们指向相同,两个对象之间有共同的属性或者方法,都可以使用

深拷贝（递归）

把一个对象中所有的属性或者方法,一个一个的找到.并且在另一个对象中开辟相应的空间,一个一个的存储到另一个对象中

遍历DOM树（递归）

```js
//获取页面中的根节点--根标签
var root=document.documentElement;
//函数遍历DOM树
//根据根节点,调用fn的函数,显示的是根节点的名字
function forDOM(root) {
    //调用f1,显示的是节点的名字
    f1(root);
    //获取根节点中所有的子节点
    var children=root.children;
    forChildren(children);
}
//给我所有的子节点,我把这个子节点中的所有的子节点显示出来
function forChildren(children) {
    //遍历所有的子节点
    for(var i=0;i<children.length;i++){
        //每个子节点
        var child=children[i];
        //显示每个子节点的名字
        f1(child);
        //判断child下面有没有子节点,如果还有子节点,那么就继续的遍历
        child.children&&forDOM(child);
    }
}

function f1(node) {
    console.log(node.nodeName);
}
forDOM(root);

//  第一个函数:给根节点,找到所有的子节点:forDOM(根节点)
//  获取这个根节点的子节点
//  var children=根节点的.children
//  调用第二个函数
//  第二个函数:给所有的子节点,把每个子节点的名字显示(children)
//  for(var i=0;i<children.length;i++){
//    每个子节点
//    var child=children[i];
//    f1(child);给我节点,我显示该节点的名字
//    child是子节点,但是如果child里面还有子节点,此时child就是爹了
//    child.children&&第一个函数(child)
//  }
```





# 正则表达式（重要）



## 定义

也叫规则表达式。按照一定的规则组成的一个表达式，这个表达式的作用主要是匹配字符串的

## 作用

匹配字符串的，在大多数编程语言中都可以使用

## 组成

是由元字符或者是限定符组成的一个式子

#### 注意

正则表达式中:/   /g 表示的是全局模式匹配
正则表达式中:/   /i 表示的是忽略大小写

### 元字符

#### 元字符

- .  表示的是:除了\n以外的任意的一个字符   "fdsfs238"

- []第一个含义 表示的是:范围 

  [0-9] 表示的是0到9之间的任意的一个数字,  "789" [0-9]

  [a-z] 表示的是:所有的小写的字母中的任意的一个

  [a-zA-Z] 表示的是:所有的字母的任意的一个

  [0-9a-zA-Z] 表示的是: 所有的数字或者是字母中的一个

- [] 第二个含义: 把正则表达式中元字符的意义干掉    

  [.] 表示的就是一个.

- | 或者     

  [0-9]|[a-z] 表示的是要么是一个数字,要么是一个小写的字母

- () 分组 提升优先级   

  [0-9]|([a-z])|[A-Z]

  ([0-9])([1-5])([a-z]) 三组, 从最左边开始计算

  (()(())) 四组 

#### 既是元字符，又是限定符

- *表示的是:前面的表达式出现了0次到多次

  【a-z】【0-9】* 小写字母中的任意一个 后面是要么是没有数字的,要么是多个数字的

  "fdsfs3223323"  【a-z】【0-9】*

- +表示的是:前面的表达式出现了1次到多次

  【a-z】【9】+  小写字母一个后面最少一个9,或者多个9 "fesfewww9fefds"

- ?  表示的是:前面的表达式出现了0次到1次,最少是0次,最多1次 ,另一个含义:阻止贪婪模式

  【4】【a-z】? "1231234ij"

#### 限定符

限定前面的表达式出现的次数

- {} 更加的明确前面的表达式出现的次数

  {0,} 表示的是前面的表达式出现了0次到多次,和 *一样的

  {1,} 表示的是前面的表达式出现了1次到多次,和 +一样的

  {0,1} 表示的是前面的表达式出现了0次到1次,和 ?一样的

  {5,10} 表示的是前面的表达式出现了5次到10次

  {4} 前面的表达式出现了4次

  {,10} 错误的========不能这么写

- ^ 表示的是以什么开始；或者是取非(取反)

  ^[0-9] 以数字开头

  ^[a-z] 以小写字母开始

  [^0-9] 取反,非数字

  [^a-z] 非小写字母

  [^0-9a-zA-Z_]非数字字母，即就是特殊符号

- $ 表示的是以什么结束  

  【0-9】【a-z】$  必须以小写字母结束

  ^【0-9】【a-z】相当于是严格模式  "4f"

- \d 数字中的任意一个,
- \D 非数字中的一个
- \s 空白符中的一个
- \S 非空白符
- \w 非特殊符号
- \W 特殊符号
- \b 单词的边界

### 正则表达式练习

```
身份证：([1-9][0-9]{14})([0-9]{2}[0-9xX])?
座机号码的正则表达：\d{3,4}[-]\d{8}
qq号码的正则表达式：[1-9]\d{4,11}：
手机号码的正则表达式：([1][358][0-9]{8})|([1][4][37][0-9]{8})|([1][7][01367][0-9]{8})
邮箱的正则表达式(记住):[0-9a-zA-Z_.-]+[@][0-9a-zA-Z_.-]+[.]([a-zA-Z]+){1,2}

```

## 创建正则表达式对象

1.通过构造函数创建对象

```js
var reg=new RegExp();
var str="im 10086";
var flag=reg.test(str);
console.log(flag);//t
```

2.字面量的方式创建对象

```js
var reg=new  RegExp(/\d{5}/);
var flag=reg.test("im 888");
console.log(flag);//f
```





## 案例



# 数组和伪数组的区别

