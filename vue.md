# Vue.js - Day1

### 什么是Vue.js

- Vue.js 是目前最火的一个前端框架，React是最流行的一个前端框架（React除了开发网站，还可以开发手机App， Vue语法也是可以用于进行手机App开发的，需要借助于Weex）
- Vue.js 是前端的**主流框架之一**，和Angular.js、React.js 一起，并成为前端三大主流框架！
- Vue.js 是一套构建用户界面的框架，**只关注视图层**，它不仅易于上手，还便于与第三方库或既有项目整合。（Vue有配套的第三方类库，可以整合起来做大型项目的开发）
- 前端的主要工作？主要负责MVC中的V这一层；主要工作就是和界面打交道，来制作前端页面效果；



## 为什么要学习流行框架

- 企业为了提高开发效率：在企业中，时间就是效率，效率就是金钱；

- 企业中，使用框架，能够提高开发的效率；



- 提高开发效率的发展历程：原生JS -> Jquery之类的类库 -> 前端模板引擎 -> Angular.js / Vue.js（能够帮助我们减少不必要的DOM操作；提高渲染效率；双向数据绑定的概念【通过框架提供的指令，我们前端程序员只需要关心数据的业务逻辑，不再关心DOM是如何渲染的了】）
- 在Vue中，一个核心的概念，就是让用户不再操作DOM元素，解放了用户的双手，让程序员可以更多的时间去关注业务逻辑；



- 增强自己就业时候的竞争力

- 人无我有，人有我优
- 你平时不忙的时候，都在干嘛？

## 框架和库的区别

- 框架：是一套完整的解决方案；对项目的侵入性较大，项目如果需要更换框架，则需要重新架构整个项目。

- node 中的 express；



- 库（插件）：提供某一个小功能，对项目的侵入性较小，如果某个库无法完成某些需求，可以很容易切换到其它库实现需求。

- 1. 从Jquery 切换到 Zepto
- 1. 从 EJS 切换到 art-template

## Node（后端）中的 MVC 与 前端中的 MVVM 之间的区别

- MVC 是后端的分层开发概念；
- MVVM是前端视图层的概念，主要关注于 视图层分离，也就是说：MVVM把前端的视图层，分为了 三部分 Model（保留每个页面中的单独的数据）, View（每个页面的html结构） , VM ViewModel（mvvm思想核心，是一个调度者，提供了数据的双向绑定）
- 为什么有了MVC还要有MVVM



## Vue.js 基本代码 和 MVVM 之间的对应关系

## Vue 基本的代码结构`和`插值表达式`v-cloak`

html

```
<div id="app">
    <!--使用 v-cloak能够解决插值表达式闪烁的问题-->
    <p v-cloak>{{msg}}</p>
</div>
```

javascript

```javascript
//02 创建一个vue的实例
//当我们导入包之后，在浏览器的内存中，就多了一个vue构造函数
//注意：我们new出来的这个vm对象，就是我们mvvm中的vm调度者
var vm = new Vue({
    el: '#app',//表示当前我们new的这个vue实例，要控制页面上的哪个区域
    //这里的data就是mvvm中的m，专门用来保存每个页面的数据的
    data: { //data属性中，存放的是el中要用到的数据
        msg: '欢迎学习vue',//通过vue提供的指令，很方便的就能把数据渲染到页面上
        // 程序员不在手动操作DOM元素，【前端的vue之前，不提倡手动操作DOM元素了】
    }
})
```

v-cloak使用时style的配置

```css
[v-cloak]{
    display: none;
}
```



## Vue指令之`v-text`和`v-html`

### v-text

```
<h4 v-text="msg"></h4>
```

注意：

- 默认v-text没有闪烁问题，不需要设置style
- v-text会覆盖元素中原本的内容，但是v-cloak插值表达式只会替换自己的这个占位符不会把整个元素的内容清空

### v-html

```
<div v-html="msg2">原始内容</div>
```

作用：

可以解析`msg2:'<h1>哈哈，我是一个大大的h1</h1>'`中的html到页面中，但是会替换掉div中`原始内容`



## Vue指令之`v-bind`

作用：

提供的用于绑定属性的指令

注意：v-bind中可以写合法的JavaScript表达式

三种用法：

1.直接使用指令`v-bind`

```
<input type="button" value="按钮" v-bind:title="mytitle">
```

```JavaScript
var vm = new Vue({
    el: '#app',
    data:{
        mytitle:'这是一个自己定义的title'
    }
})
```

2.使用简化指令`:`

```
<input type="button" value="按钮" :title="mytitle">
```

3.在绑定的时候，拼接绑定内容：`:title="mytitle + ', 这是追加的内容'"`

## Vue指令之`v-on`和`跑马灯效果`

### v-on

作用：这个methods属性中定义了当前vue实例所有可用的方法

两种用法：

1.直接使用指令`v-on

```
<!--<input type="button" value="按钮" :title="mytitle+'123'" v-on:click="alert('hello')">这个方法不可用-->
<input type="button" value="按钮" v-on:click="show">
```

```javascript
var vm = new Vue({
    el: '#app',
    methods:{//这个methods属性中定义了当前vue实例所有可用的方法
        show:function () {
            alert('hello')
        }
    }
});
```

2.使用简化指令`@`

```
<input type="button" value="按钮" @mouseover="show">
```

### 跑马灯效果

#### 分析:

- 给【浪起来】按钮，绑定一个点击事件 v-on @
- 在按钮的处理函数中写相关业务逻辑代码：拿到msg字符串，然后调用字符串的substring来进行字符串的截取操作，把第一个字符截取出来放到最后一个位置即可
- 为了实现点击一下按钮，自动截取的功能，需要把2中的代码放到一个定时器中

#### HTML结构：

```
<div id="app">
    <input type="button" value="浪起来" @click="lang">
    <input type="button" value="低调" @click="stop">
    <h4>{{msg}}</h4>
</div>
```

#### Vue实例：

```javascript
    var vm=new Vue({
        el:'#app',
        data:{
            msg:'猥琐发育，别浪~~!',
            intervalId:null
        },
        methods:{
            lang(){
                // console.log(this.msg);
                // var _this=this;
                if(this.intervalId!=null)return;
               // setInterval( ()=> {},400);  使内部的this指向内部的this
               this.intervalId=setInterval( ()=> {
                   //获取到头的第一个字符
                   var start=this.msg.substring(0,1);
                   //获取到后面的所有字符
                   var end=this.msg.substring(1);
                   //重新拼接得到新的字符串，并且重新赋值给this.msg
                   this.msg=end +start;
               },400)
            },
            stop(){//停止定时器
                clearInterval(this.intervalId);
                //每当清除了定时器之后，应重新把intervalId置为null
                this.intervalId=null
            }
        }
    })
```

#### 注意

- 在vm实例中，如果想要调用data上的数据，或者想要调用methods中的方法，必须通过this.数据数据名或者this.方法名来进行访问。这里的this就表示我们new出来的vm实例对象。
- vm实例，会监听自己身上data中所有数据的改变。只要数据已发生变化，就会自动把最新的数据，从data上同步到页面中。【好处：程序员只需要关心数据，不需要考虑如何重新渲染DOM页面】



## Vue指令`事件修饰符`

- .stop       阻止冒泡

```
<input type="button" value="戳他" @click.stop="btnHandler">
```

- .prevent    阻止默认事件

```
<a href="http://www.baidu.com" @click.prevent="linkClick">有问题去百度</a>
```

- .capture    添加事件侦听器时使用事件捕获模式

```
<div class="inner" @click.capture="divHandler">
<input type="button" value="戳他" @click="btnHandler">
</div>
```

- .self       只当事件在该元素本身（比如不是子元素）触发时触发回调

注意：只会阻止自己身上的冒泡行为，不能阻止别人的。作用不能和.stop不一样。

```
<div class="inner" @click.self="divHandler">
    <input type="button" value="戳他" @click="btnHandler">
</div>
```

- .once       事件只触发一次

```
<a href="http://www.baidu.com" @click.prevent.once="linkClick">有问题去百度</a>
```





## Vue指令之`v-model`和`双向数据绑定`

作用：使用v-model指令，可以实现表单元素和model中数据的双向数据绑定。

```
<input type="text" v-model="msg" style="width: 100%">
```

注意：

- v-bind只能实现数据的单向绑定，从m自动绑定到v，无法实现数据的双向绑定
- v-model只能运用在表单元素中如input(radio,text,address,email...)、 select、 checkbox、 textarea 



## 简易计算器案例

1. HTML 代码结构

```
<div id="app">
    <input type="text" v-model="n1">

    <select v-model="opt">
        <option value="+">+</option>
        <option value="-">-</option>
        <option value="*">*</option>
        <option value="/">/</option>
    </select>

    <input type="text" v-model="n2">

    <input type="button" value="=" @click="calc">

    <input type="text" v-model="result">
</div>
```

1. Vue实例代码：

```JavaScript
var vm = new Vue({
        el: '#app',
        data: {
            n1: 0,
            n2: 0,
            result: 0,
            opt: '+'
        },
        methods: {
            calc() { // 计算器算数的方法
                // 逻辑：
                 switch (this.opt) {
                  case '+':
                    this.result = parseInt(this.n1) + parseInt(this.n2)
                    break;
                  case '-':
                    this.result = parseInt(this.n1) - parseInt(this.n2)
                    break;
                  case '*':
                    this.result = parseInt(this.n1) * parseInt(this.n2)
                    break;
                  case '/':
                    this.result = parseInt(this.n1) / parseInt(this.n2)
                    break;
                }

                // 注意：这是投机取巧的方式，正式开发中，尽量少用
                // var codeStr = 'parseInt(this.n1) ' + this.opt + ' parseInt(this.n2)'
                // this.result = eval(codeStr)
            }
        }
    });
```

 

## 在Vue中使用样式 

### 使用class样式

1. 数组

```
<h1 :class="['red', 'thin']">这是一个邪恶的H1</h1>
```

1. 数组中使用三元表达式

```
data:{
    flag:true
}
```

```
<h1 :class="['red', 'thin', flag?'active':'']">这是一个邪恶的H1</h1>
```

1. 数组中嵌套对象

```javascript
data:{
    flag:true
}
```



```
<h1 :class="['red', 'thin', {'active': flag}]">这是一个邪恶的H1</h1>
```

1. 直接使用对象

对象的属性名是类名，对象的属性可带引号，也可以不带引号

```
    <h1 :class="{red:true, italic:true, active:true, thin:true}">这是一个邪恶的H1</h1>
```

 

### 使用内联样式

1. 直接在元素上通过 `:style` 的形式，书写样式对象

```
<h1 :style="{color: 'red', 'font-size': '40px'}">这是一个善良的H1</h1>
```

1. 将样式对象，定义到 `data` 中，并直接引用到 `:style` 中

- 在data上定义样式：

```
data: {
        h1StyleObj: { color: 'red', 'font-size': '40px', 'font-weight': '200' }
}
```

- 在元素中，通过属性绑定的形式，将样式对象应用到元素中：

```
<h1 :style="h1StyleObj">这是一个善良的H1</h1>
```

1. 在 `:style` 中通过数组，引用多个 `data` 上的样式对象

- 在data上定义样式：

```
data: {
        h1StyleObj: { color: 'red', 'font-size': '40px', 'font-weight': '200' },
        h1StyleObj2: { fontStyle: 'italic' }
}
```

- 在元素中，通过属性绑定的形式，将样式对象应用到元素中：

```
<h1 :style="[h1StyleObj, h1StyleObj2]">这是一个善良的H1</h1>
```



## Vue指令之`v-for`和`key`属性

1. 迭代数组

```
data:{
    list:[1,2,3,4,5,6]
}
```

```
<ul>
  <li v-for="(item, i) in list">索引：{{i}} --- 姓名：{{item.name}} --- 年龄：{{item.age}}</li>
</ul>
```

1. 迭代对象中的属性

```
data: {
    user: {
        id: 1,
        name: 'tony·a',
        gender: '男'
    }
}
```

```
<p v-for="(val,key,i) in user">值:{{val}}---键:{{key}}---index:{{i}}</p>
```

1. 迭代数字

count从1开始循环

```
<p v-for="count in 10">这是第{{count}}次循环</p>
```



> 2.2.0+ 的版本里，**当在组件中使用** v-for 时，key 现在是必须的。



当 Vue.js 用 v-for 正在更新已渲染过的元素列表时，它默认用 “**就地复用**” 策略。如果数据项的顺序被改变，Vue将**不是移动 DOM 元素来匹配数据项的顺序**， 而是**简单复用此处每个元素**，并且确保它在特定索引下显示已被渲染过的每个元素。



为了给 Vue 一个提示，**以便它能跟踪每个节点的身份，从而重用和重新排序现有元素**，你需要为每项提供一个唯一 key 属性。

```
<div id="app">
    <div>
        <label>ID:
        <input type="text" v-model="id">
        </label>

        <label>NAME:
            <input type="text" v-model="name">
        </label>

        <input type="button" value="添加" @click="add">
    </div>

    <!--注意：v-for循环的时候，key属性只能使用number获取string-->
    <!--注意:key在使用的时候，必须用v-bind属性绑定的形式，指定key得值-->
    <!--在组件中，使用v-for循环的时候，或者在一些特殊情况中，如果v-for有问题，必须在使用v-for的同时，指定唯一的字符串/数字类型的:key值-->
    <p v-for="item in list" :key="item.id">
        <input type="checkbox"> {{item.id}}--{{item.name}}
    </p>
</div>
```



```JavaScript
var vm=new Vue({
    el:'#app',
    data:{
        list:[
            {id:1,name:'sally1'},
            {id:2,name:'sally2'},
            {id:3,name:'sally3'},
            {id:4,name:'sally4'},
            {id:5,name:'sally5'}
        ],
        id:'',
        name:''
    },
    methods:{
        add(){
            this.list.push({id:this.id,name:this.name})
        }
    }
});
```

## Vue指令之`v-if`和`v-show `

> 一般来说，v-if 有更高的切换消耗而 v-show 有更高的初始渲染消耗。因此，如果需要频繁切换 v-show 较好，如果在运行时条件不大可能改变 v-if 较好。

```
<div id="app">
    <!--<input type="button" @click="toggle" value="toggle">-->
    <input type="button" @click="flag=!flag" value="toggle">
    
    <!--v-if的特点：每次都会重新删除创建元素-->
    <!--v-show的特点：每次不会进行DOM的删除和创建操作，只是切换了元素的display:none的样式-->

    <!--v-if有较高的切换性能-->
    <!--v-show有较高的初始渲染消耗-->

    <!--如果元素涉及到频繁的切换，最好不要使用v-if，而是使用v-show -->
    <!--如果元素坑永远也不会被显示出来，则推荐使用v-if-->
    <h3 v-if="flag">这是用v-if控制的元素</h3>
    <h3 v-show="flag">这是用v-show控制的元素</h3>
</div>
```

```JavaScript
var vm=new Vue({
    el:'#app',
    data:{
        flag:true
    },
    methods:{
        // toggle(){
        //     this.flag=!this.flag
        // }
    }
});
```

