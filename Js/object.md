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

