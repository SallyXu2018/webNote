# 函数

作用：代码的重用(把一坨代码封装，在需要的时候直接调用即可)

### 函数的两种定义方式

##### 命名函数----函数的声明

function 函数名字(){

函数体--------一坨重复的代码 

}

 调用方法：函数名（）

```js
function f1() {
    console.log("1111111");
}
f1();//2222222
function f1() {
    console.log("2222222");
}
f1();//2222222

console.log(f1);//函数名里存的是函数的代码
console.log(typeof f1);//函数是有数据类型的，其数据类型为function
```

##### 匿名函数----函数的表达式（把一个函数给一个变量）

var 变量=匿名函数；

如果是函数表达式，那前面的变量中存储的就是一个函数，而这个变量就是一个函数，这个变量加个小括号就可以调用了即：

变量（）；

```js
var f2=function () {
    console.log("3333333");
};
f2();
var f2=function () {
    console.log("4444444");
};//注意：函数表达式赋值后必须要加分号
f2();
```

```js
//含数自调用，一次性调用
(function () { console.log("bbbbb")})();//函数代码块(); 
```

### 函数名字：要遵循驼峰命名法

### 函数参数

在函数定义的时候，函数名字后面的小括号里的变量就是参数，目的是在函数调用时，用户传进来的值操作；在函数调用的时候，按照提示的方式，给变量赋值就叫做传参

```js
function consoleSum(x,y){//形参
    var sum=x+y;
    console.log(sum);
}
var num1=parseInt(prompt("请输入第一个数字"));
var num2=parseInt(prompt("请输入第二个数字"));
consoleSum(num1,num2);//实参：可以是变量也可以是值
//形参的个数和实参的个数可以不一致
```

set:设置

get:获取

### 函数的返回值

在函数内部有关键字return，并且在return后面有内容，这个内容就被返回了；如果一个函数没有明确的返回值，那么被调用的时候被接受了，结果是undefined(没有明确的返回值：函数中没有return；函数中有return，但是return后面没有任何内容)

当函数调用之后，需要这个返回值，那么就定义这个函数有返回值

```js
//有参数有返回值的函数
function getSum(x,y){
    var sum=x+y;
    return sum;
}
var result=getSum(22,33)+11;
console.log(result);a

console.log(getSum);//输出的是这个函数的代码
```

函数没有返回值，但是在调用的时候被接受了，那结果是undefined

变量声明了，没有赋值，结果也是undefined

return下面的代码是不会执行的



### 函数案例

```js
//函数练习 输入年月日获取日期是这一年的多少天
function getDay(year,month,day) {
    //已经将输入月份的日子存进了第几天里
    var days=day;
    //如果十一月份，直接返回天数
    if(month==1){
        return days;
    }
    //定义一个数组，存储每个月的天数
    var months=[31,28,31,30,31,30,31,31,30,31,30,31];
    //小于的是输入的月份-1
    //如果输入的是7月份，前六个月的天数相加
    for( var i=0;i<month-1;i++){
        days+=months[i];
    }
    //判断这个年份是不是闰年，是的话并且月份大于2月days就加1
    if(isYear(year)&&month>2){//函数里可以调用函数
        days++;
    }
    return days;
}
function isYear(y) {
    return y%4==0&&y%100!=0||y%400==0;
}
console.log(getDay(2000,3,20));
```

### 函数作为参数使用

```js
function sayHi(fn) {
    console.log("hi!");
    sayBye();
}
function sayBye() {//看到这个函数作参数了，那就是回调函数
    console.log("bye-bye");
}
sayHi(sayBye);
```

### 函数作为返回值使用

```js
function f1() {
    console.log("f1被调用了");
    return function () {
        console.log("这是一个函数");
    }
}
var ff=f1();
ff();
```

### arguments伪数组元素

定义一个函数，如果不能确定用户是否传入参数，或者不知道用户传入了几个参数，没办法计算，但是如果知道了 函数的参数的个数，也知道了每个参数的值，可以使用arguments。使用arguments对象可以获取传入的每个参数的值。

```js
	//argument 计算n个数字的和
function f1() {
    var sum=0;
    //arguments  当数组使用-------->伪数组
    for(var i=0;i<arguments.length;i++){
        sum+=arguments[i];
    }
    return sum;
}
console.log(f1(10,20,30,40));
```



### 作用域

##### 全局变量

声明的变量是使用var声明的，这个变量就是全局变量，在页面的任何地方都可以使用。

除了函数里面以外定义的变量，都是全局变量。全局变量，如果页面不关闭那么就不会释放，就会占空间，消耗内存。

##### 局部变量

在函数内部定义的变量，是局部变量，外面不能使用。

##### 隐式全局变量

声明的变量没有var，在一个函数里面定义了隐式全局变量在函数外部是可以被访问的。

```js
function f1() {
    num1=10;//隐式全局变量
    var num2=20;//局部变量
}
f1();
console.log(num1);
console.log(num2);//!!!ReferenceError: num2 is not defined
```

全局变量是不能被删除的，隐式全局变量是可以被删除的。

```js
var num1=10;
num2=20;//隐式全局变量
delete num1;
delete num2;
console.log(num1+10);//20
console.log(typeof num2);//undefined 隐式全局变量可以被删除
```

```js
var num1=55;
var num2=66;
function f1(num,num1) {
    num=100;
    num1=100;
    num2=100;//隐式全局变量
    console.log(num);//100
    console.log(num1);//100
    console.log(num2);//100
}
f1(num1,num2);
console.log(num1);//55
console.log(num2);//100
console.log(num);//报错
```

全局作用域：全局变量的适用范围

局部作用域：局部变量的适用范围

块级作用域：一对大括号就可以看成是一块，在这对大括号里定义的变量只能在这块中使用。但是在Js中在大括号中定义的变量，在大括号外仍旧能访问，所以Js中没有块级作用域，只有函数除外。

```js
<script>//0级作用域
    var num1=10;
    function f1() {//1级作用域
        var num1=20;
        function f2() {//2级作用域
            var num1=30;
            function f3() {//3级作用域
                var num1=40;
                console.log(num1);
            }
            f3();
        }
        f2();
    }
    f1();//输出3级，如果3级作用域没定义，则往上找定义的变量直至0级，还没有的话则报错
    //整个形成的关系叫做作用域链
</script>
```

### 预解析

##### 预解析过程

- 把变量的声明提前到当前作用域的最前面，只提升声明，不提升赋值
- 把函数的声明提前到当前作用域的最上面，只提升声明，不提升赋值
- 先提升var，再提升function

```js
// function f1() {
//     //var num;
//     console.log(num);
//     var num=20;
// }//函数声明提前
f1();//调用
var num=10;
function f1() {
    //var num;
    console.log(num);
    var num=20;
}//undefined
//存在预解析，f1声明提前

//var num;//变量声明提前，先提升var
// function f1() {
//     console.log(num);
// }//函数声明提前，再提升function
f1();//调用
var num=10;
function f1() {
    console.log(num);
}//undefined
```

##### 注意

- 函数中的变量值会提升到函数作用域的最上面，不会出去

```
function f2() {
    //var num;
    console.log(num);//undefined
    var num=10;
}
f2();
console.log(num);//报错

```

- 预解析会分段，多对script标签中函数重名，预解析的时候不会冲突



##### 快速解析预解析结果案例

```js
//var a;//先提前声明var
// function a() {
// console.log("aaaa");
// }//在提前声明函数
console.log(a);//输出a函数代码
function a() {
    console.log("aaaa");
}
var a=10;
console.log(a);//输出10
```

```js
//var a;//提前声明var变量
var a=18;
// function f1() {
//     var b;
//     var a;
//     b=9;
//     console.log(a);//输出undefined
//     console.log(b);//输出9
//     a="123";
// }//提前声明function
f1();
function f1() {
    var b=9;
    console.log(a);//undefined
    console.log(b);//9
    var a="123";
}
```

```js
// function f1() {
//     var a;//局部变量
//     a=9;
//隐式全局变量b,c 在外不可以访问
//     b=9;
//     c=9;
//     console.log(a);
//     console.log(b);
//     console.log(c);
// }
f1();
console.log(c);//输出9
console.log(b);//输出9
console.log(a);//输出报错
function f1() {
    var a=b=c=9;
    console.log(a);//输出9
    console.log(b);//输出9
    console.log(c);//输出9
}
```

```js
//var f1;
f1();//报错，这是种假象
var f1=function () {
  console.log(a);
  var a=10;
};
```
