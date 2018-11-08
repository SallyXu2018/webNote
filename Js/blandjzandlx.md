# 变量

作用：操作数据（存储数据，读取数据）

### 声明变量

var 变量名字;

每一行代码结束应该有分号

区分大小写

字符串可以使用的单引号，也可以使用双引号，目前我们暂时使用双引号



### 变量名的注意问题

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

### js数据类型

##### 原始数据类型：number、string、boolean、null、undefined、object

##### 基本类型（简单类型），值类型：number、string、boolean

##### 复杂类型（引用类型）：object

##### 空类型：null、undefined

值类型的值在哪一块内存空间存储？栈

引用类型的值在哪一块内存空间存储？栈和堆 栈放地址，堆放对象

### 值类型之间传递的是值

```js
function f1(x) {
    x=100;
}
var num=10;
f1(num);
console.log(num);
```

### 引用之间传递的是地址

```js
//object对象（引用类型）在栈中名为obj的内存块存储的是obj对象属性的地址，obj对象属性存放在堆中，栈中的地址指向堆
var obj={
    name:"sally"
};
function f2(obj2) {//在栈中名为obj2的内存块存储的是obj2对象属性的地址,还未赋值
    obj2.name="candy";
};
console.log(obj.name);//sally
f2(obj);
// 执行时obj2的栈中的地址被obj赋值，此时obj2也指向堆中obj的属性
// 执行语句，obj2属性赋值为candy，由于obj和obj2为同一堆的地址，则obj的name值为candy
console.log(obj.name);//candy
```

```js
function Person(name,age,salary) {
    this.name=name;
    this.age=age;
    this.salary=salary;
}
function f1(person) {
    person.name="ls";
    person=new Person("aa",18,10);//代码执行到这里时，person指向新的对象属性，原先的指向作废。但是仍旧指向zs
}

var p=new Person("zs",18,1000);
console.log(p.name);//zs
f1(p);
console.log(p.name);//ls
```

### 什么情况下的结果是undefined？

变量声明了，没有赋值

函数没有明确返回值，如果接收了，结果也是undefined

如果一个变量的结果是undefined和一个数字进行计算，结果是NaN --not an number 不是一个数字，也没有意义

object --->对象

当一个变量被赋值为null时，它的类型是对象object



### 如何获取这个变量的数据类型是什么呢？

使用typeof来获取，适用语法：

typeof 变量名

typeof(变量名)



# 进制

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



### 如何验证一个结果是不是NaN？

使用isNaN()函数，不是数字情况下为true



### 字符串拼接

使用+可以把多个字符串放在一起形成一个字符串

只要有一个是字符串的，其他是数字那么结果也是拼接

如果有一个是字符串，另一个不是字符串，-，*等可以进行计算，隐式转换



# 类型转换

### 其他类型转数字类型

- parseInt() 转整数

`console.log(parseInt(10.1dnuei));` //10

- parseFloat()转小数
- Number()转数字 严格

`console.log(parseInt(10.1dnuei));`// NaN

### 其他类型转字符串类型 

- .toString()
- String()

如果变量有意义调用  .toString()

如果变量没有意义使用String() 

### 其他类型转布尔类型

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



### 字面量：把一个值直接赋值给一个变量

声明变量并初始化

`var a=10;//字面量`

`var b=a;//不是字面量`



### 一元运算符：++  -- 

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

