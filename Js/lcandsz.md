# 流程控制

代码的执行过程，有三种方式

顺序结构：从上到下，从左到右

### 分支语句

包含if语句 ，if-else语句，if-else if-else if...语句，switch-case语句，三元表达式语句

分支语句总结：if-else if...一般是对范围的判断；switch-case一般是对值得判断

##### if-else语句

```js
/*if-else语句*/
var age=parseInt(prompt("请您输入年龄"));//弹框，并且有输入
if(age>18){
    console.log("可以去看电影啦哈哈");
}else{
    console.log("看什么看");
}
```



##### 三元表达式，运算符号：   ？ ：

语法： var 变量=表达式1？表达式2：表达式3；

执行过程：表达式1的结果是true还是false，true则执行表达式2，然后将结果交给变量；false则执行表达式3，将结果交给变量。

一般情况下if-else的语句都可以用三元表达式的方式表达出来



##### switch-case语句

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

循环语句：while循环，do-while循环，for循环，后期还有个for-in语句

##### while循环语句

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

##### do-while循环语句

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

##### for循环语句

for（表达式1；表达式2；表达式3）{

​	循环体

}

执行过程：先执行一次表达式1.然后判断表达式2；如果不成立，则不执行循环体；

如果表达式2成立，执行循环体的代码.....结束后，跳到表达式3，再跳到表达式2判断....



alert();弹框

console.log();在控制台

document.write();在网页中直接打印



##### for的嵌套循环

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



##### break关键字

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

##### continue关键字

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



# 数组（一组有序的数据）

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



##### 如何设置数组中某个位置的值？

数组名[下标]=值；

##### 如何获取数组中某个位置的值？

var result=数组名[下标]；

console.log(result)； 

##### 数组中存储的数据类型一定是一样的吗？

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



### 冒泡排序

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

