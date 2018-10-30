## JavaScript是什么？

脚本语言：不需要编译，直接运行

解释性语言：遇到一样代码就解释一行代码（c#是一门面向对象的语言，也是编译语言，是.net技术使用的）

动态类型的语言：

基于对象的语言：

弱类型的语言：声明变量的时候都是用var（强类型的语言，如c#。存储一个数字：int num1=10;float num2=90.3;）



##### js分三个部分：

ECMAScript标准:js的基本语法

DOM:

BOOM:



程序员用的浏览器推荐：MDN



# js语法

### 变量

作用：操作数据（存储数据，读取数据）

#### 声明变量

var 变量名字;

每一行代码结束应该有分号

区分大小写

字符串可以使用的单引号，也可以使用双引号，目前我们暂时使用双引号



#### 变量名的注意问题：

- 变量的名字有意义
- 变量名有一定的规范：一般以字母，$符号，下划线开头，中间或后面可以有$、字母、数字
- 变量名一般都是小写，多个单词使用驼峰命名法



两变量值交换（适用于数字交换的第二种方式）

```js
var num1=10;

var num2=20;

num1=num1+num2;

num2=num1-num2;

num1=num1-num2;
```

c++中数字交换 位运算（只需要了解）

```js
var num1=10;

var num2=20;

num1=num1^num2;

num2=num1^num2;

num1=num1^num2;
```



ctrl+alt+l----->格式化代码的

ctrl+/------->代码块注释

#### js中的原始数据类型有

number、string、boolean、null、undefined、object

#### 什么情况下的结果是undefined？

变量声明了，没有赋值

函数没有明确返回值，如果接收了，结果也是undefined

如果一个变量的结果是undefined和一个数字进行计算，结果是NaN --not an number 不是一个数字，也没有意义

object --->对象

当一个变量被赋值为null时，它的类型是对象object



#### 如何获取这个变量的数据类型是什么呢？

使用typeof来获取，适用语法：

typeof 变量名

typeof(变量名)



### 进制

十进制：正常数字

八进制：0开头

十六进制“：0x开头

不要拿小数验证小数，有bug

```js
var a=0.1;

var b=0.2;

var sum=a+b;

console.log(sum==0.3)；
```

输出为false



#### 如何验证一个结果是不是NaN？

使用isNaN()函数，不是数字情况下为true



#### 字符串拼接：

使用+可以把多个字符串放在一起形成一个字符串

只要有一个是字符串的，其他是数字那么结果也是拼接

如果有一个是字符串，另一个不是字符串，-，*等可以进行计算，隐式转换



### 类型转换

#### 其他类型转数字类型

- parseInt() 转整数

`console.log(parseInt(10.1dnuei));` //10

- parseFloat()转小数

- Number()转数字 严格

`console.log(parseInt(10.1dnuei));`// NaN

#### 其他类型转字符串类型 

- .toString()

- String()

如果变量有意义调用  .toString()

如果变量没有意义使用String() 

#### 其他类型转布尔类型

- Boolean()

没有意义的或者为空的 为false

```js
console.log(Boolean(1));//true

console.log(Boolean(0));//false

console.log(Boolean(11));//true

console.log(Boolean(-11));//true

console.log(Boolean("哈哈"));//true

console.log(Boolean(" "));//false

console.log(Boolean(null));//false

console.log(Boolean(undefined));//false
```



#### 字面量：把一个值直接赋值给一个变量

声明变量并初始化

`var a=10;//字面量`

`var b=a;//不是字面量`



#### 一元运算符：++  -- 

```js
var num=10;

var sum=num++ +10;

console.log(sum);//20
```

如果++在后面：现参与运算，运算结束后自身再加1



```
var num=10;

var sum=++num +10;

console.log(sum);//21
```

如果++在前面：自身再加1，再现参与运算



### 流程控制

代码的执行过程，有三种方式

顺序结构：从上到下，从左到右

#### 分支结构：if语句 ，if-else语句，if-else if-else if...语句，switch-case语句，三元表达式语句

分支语句总结：if-else if...一般是对范围的判断；switch-case一般是对值得判断

#### 循环语句：while循环，do-while循环，for循环，后期还有个for-in语句

```js
/*if-else语句*/
var age=parseInt(prompt("请您输入年龄"));//弹框，并且有输入
if(age>18){
    console.log("可以去看电影啦哈哈");
}else{
    console.log("看什么看");
}
```



#### 三元表达式，运算符号：   ？ ：

语法： var 变量=表达式1？表达式2：表达式3；

执行过程：表达式1的结果是true还是false，true则执行表达式2，然后将结果交给变量；false则执行表达式3，将结果交给变量。

一般情况下if-else的语句都可以用三元表达式的方式表达出来



#### switch-case语句

语法：

switch（表达式）{

case 值1：代码1；break；

case 值2：代码2；break；

case 值3：代码3；break；

case 值4：代码4；break；

...

default：代码5；

}

执行过程：获取表达式的值，和值1比较，如果一样，则执行代码1，遇到break则跳出整个语句，后面代码不执行；如果表达式的值和值1不一样，则和值2比较，如果相同则执行代码2.......

注意问题：

default后面的break是可以省略的

default也可以省略

语句中和后面的case中的值比较的时候用的是严格的模式

```js
//判断一个月份有多少天
var month=parseInt(prompt("请输入月份"));
switch (month){
    case 1:
    case 3:
    case 5:
    case 7:
    case 8:
    case 10:
    case 12:console.log("31天");break;
    case 4:
    case 6:
    case 9:
    case 10:console.log("30天");break;
    case 2:console.log("28天");break;
}
```



### 循环语句

#### while循环语句

```js
//while语句练习，求账号和密码是否一致，登录效果的实现 账号：admin 密码：123（字符串类型）
var userName=prompt("请输入账号");
var userPsw=prompt("请输入密码");
while(userName!="admin"||userPsw!="123"){
    //变量的重新赋值
    userName=prompt("请输入账号");
    userPsw=prompt("请输入密码");
}
console.log("登录成功");
```

#### do-while循环语句

do{

​	循环体

}while（条件）；

执行过程：先执行一次循环体，然后判断条件是否成立，不成立，则跳出循环，成立则继续循环体....

```js
//例子：问用户：您觉得我帅吗？如果回答y则跳出循环，如果回答为否定则直到回答为肯定为止，并提示用户：您真正有眼光
do{
    var reson=prompt("您觉得我帅吗？y/n");
}while(reson!="y");
console.log("您真有眼光");
```

#### for循环语句

for（表达式1；表达式2；表达式3）{

​	循环体

}

执行过程：先执行一次表达式1.然后判断表达式2；如果不成立，则不执行循环体；

如果表达式2成立，执行循环体的代码.....结束后，跳到表达式3，再跳到表达式2判断....



alert();弹框

console.log();在控制台

document.write();在网页中直接打印



#### for的嵌套循环

```js
//画星星案例 for的嵌套循环
//控制行数
for(var i=0;i<3;i++){
    //控制每行个数
    for(var j=0;j<5;j++){
        document.write("☆");
    }
    document.write("<br/>");
}
```

```js
//画三角形的星星
for(var i=0;i<5;i++){
    for(var j=0;j<i;j++){
        document.write("☆");
    }
    document.write("<br/>");
}
```

```js
//有表格的九九乘法表
document.write("<table border='1' cellpadding='0' cellspacing='0'>")//建立table
for(var i=0;i<9;i++){
    document.write("<tr>")//确定行数
    for(var j=0;j<=i;j++){
     document.write("<td style='border: 1px dashed #ccc'>")//确定单元格
        document.write(j+"*"+i+"="+j*i);
        document.write("</td>")
    }
    document.write("</tr>")
}
document.write("</table>")
```



调试

f12寻找sorces



习题

```js
//本金10000元存入银行，年利率是千分之三，每过一年，将本金和利息相加作为新的本金。计算五年后，获得的本金多少
var BJ=10000;
var LL=0.003;
for(var i=1;i<=5;i++){
    BJ=BJ*(1+LL);
}
console.log(BJ);
```

```js
//有个人想知道一对兔子一年内能繁衍多少对？于是就筑了一道围墙把一对兔子关在一起。一对兔子一个月可以生一对小兔子， 而一对小兔子从出生后第三个月起每个月生一对小兔子。假如一年内没有发生死亡现象，那么一对兔子一年内能繁衍多少对兔子，兔子的规律数列 1,1,2,3,5,8,13,21 每个月的值是前两个月的和
var num1=1;
var num2=1;
var sum=0;
for(var i=3;i<=12;i++){
    sum=num1+num2;
    num1=num2;
    num2=sum;
}
console.log(sum);
```



#### break关键字

在循环里，遇到break可跳出循环

```js
//在100-200之间，找出第一个能被7整除的数字
for(var i=100;i<=200;i++){
    if(i%7==0){
        console.log(i);
        break;
    }
}
```

#### continue关键字

在循环中如果遇到continue关键字，直接开始下一次循环 ，不执行后面的代码 

```js
    //求整数1-100的累加值，但要求跳过所有个位为三的数
    var sum=0;
    var i=1;
    while(i<=100){
        if(i%10==3){
            i++;
            continue;
        }
        sum+=i;
        i++
    }
    console.log(sum)
```



### 数组（一组有序的数据）

作用：可以一次性存储多个数据

包含：数组元素、数组长度、数组索引（下标）

定义：

- 通过构造函数创建数组

语法：

var 变量名=new Array();

数组的名字如果直接输出，那么直接就可以把数组中的数字直接输出

var 变量名=new Array(长度);

爱护组的长度是可以改变的

如果数组中只有长度没有数据，数组值每个都是undefined

Array（一个值）表示长度，Array（多个数字）表示值

- 通过字面量的方式创建数组

语法：

var 数组名=[ ];空数组



#### 如何设置数组中某个位置的值？

数组名[下标]=值；

#### 如何获取数组中某个位置的值？

var result=数组名[下标]；

console.log(result)； 

#### 数组中存储的数据类型一定是一样的吗？

类型可以不一样

```js
//案例7：去掉数组中重复的0,将其他的数据放在新的数组里
var arr2=[0,100,20,39,0,98,0,12,0,45];
var arr3=[];
for(var i=0;i<arr2.length;i++){
    if(arr2[i]!=0){
        arr3[arr3.length]=arr2[i];//把新数组的长度作为下标使用，数组的长度是可以改变的
    }
}
console.log(arr3);
```

```js
//案例8：反转数组----把数组中的数据位置调换
for(var i=0;i<arr1.length/2;i++){
    var temp=arr1[i];
    arr1[i]=arr1[arr1.length-1-i];
    arr1[arr1.length-1-i]=temp;
}
console.log(arr1);
```

```js
// 案例9：提示用户输入班级人数，求总成绩、平均值、最高分、最低分----扩展
var perCount=parseInt(prompt("请输入班级人数"));
var perGrade=[];
for(var i=0;i<perCount;i++){
    perGrade[perGrade.length]=parseInt(prompt("请输入第"+i+1+"人的成绩："));//把数组的长度作为下标使用，数组长度可以改变
}
//求总成绩
var sum=0
for(var i=0;i<perGrade.length;i++){
    sum+=perGrade[i];
}
console.log("这个班的总成绩为"+sum);
//求平均值
var avg=sum/perGrade.length;
console.log("这个班的平均成绩为"+avg);
//求最高分,求最低分
var max=perGrade[0];
var min=perGrade[0];
for(var i=0;i<perGrade.length;i++){
    if(max<perGrade[i]){
        max=perGrade[i];
    }
    if(min>perGrade[i]){
        min=perGrade[i];
    }
}
console.log("最高分为"+max);
console.log("最低分为"+min);

```



#### 冒泡排序

```js
var bubble=[12,10,32,25,9,28];
for(var i=0;i<bubble.length-1;i++){
    for(var j=0;j<bubble.length-1-i;j++){
        if(bubble[j]<bubble[j+1]){
            var temp=bubble[j];
            bubble[j]=bubble[j+1];
            bubble[j+1]=temp;
        }
    }
    console.log(bubble[j]);
}
```





### 函数：把一坨代码封装，在需要的时候直接调用即可

作用：代码的重用

语法：

function 函数名字(){

​	函数体--------一坨重复的代码

}

函数的调用

函数名()；

函数名字：要遵循驼峰命名法

函数参数：

在函数定义的时候，函数名字后面的小括号里的变量就是参数，目的是在函数调用时，用户传进来的值操作

在函数调用的时候，按照提示的方式，给变量赋值就叫做传参

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

函数的返回值:在函数内部有关键字return，并且在return后面有内容，这个内容就被返回了；如果一个函数没有明确的返回值，那么被调用的时候被接受了，结果是undefined(没有明确的返回值：函数中没有return；函数中有return，但是return后面没有任何内容)

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
