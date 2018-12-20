### 复习

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

#### 作用

一：数据共享，节省内存空间

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

#### 游戏思路

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

#### 游戏代码

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





## 继承









## 函数进阶













## 正则表达式
