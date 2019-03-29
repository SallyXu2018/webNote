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

# Vue.js - Day2

## 品牌管理案例

```
<div id="app">
    <div class="panel panel-primary">
        <div class="panel-heading">
            <h3 class="panel-title">添加品牌</h3>
        </div>
        <div class="panel-body form-inline">
            <label>
                Id:
                <input type="text" class="form-control" v-model="id">
            </label>

            <label>
                Name:
                <input type="text" class="form-control" v-model="name">
            </label>
            <!--在vue中，使用事件绑定机制，为元素指定处理函数的时候，如果加了小括号就可以给函数加参-->
            <input type="button" value="添加" class="btn btn-primary" @click="add">

            <label>
                搜索名称关键字：
                <input type="text" class="form-control" v-model="keywords">
            </label>
        </div>
    </div>

    <table class="table table-bordered table-hover table-striped">
        <thead>
        <tr>
            <th>Id</th>
            <th>Name</th>
            <th>Ctime</th>
            <th>Operation</th>
        </tr>
        </thead>
        <tbody>
        <!--之前，v-for的数据，都是直接从data上的list直接渲染出来的-->
        <!--现在，我们自定义了一个search方法，同时把所有的关键字，通过传参的形式，传递给了search方法-->
        <!--在search方法内部，通过执行for循环，把所有符合搜索关键字的数据，保存到一个新的数组中，返回-->
        <tr v-for="item in search(keywords)" :key="item.id">
            <td>{{item.id}}</td>
            <td v-text="item.name"></td>
            <td>{{item.ctime | dateFormat()}}</td>
            <td>
                <a href="" @click.prevent="del(item.id)">删除</a>
            </td>
        </tr>
        </tbody>

    </table>
</div>
```

### 添加新品牌

```JavaScript
add(){//添加的方法
    //分析
    //01 获取id和name，直接从data上面获取
    //02 组织出一个对象
    //03 把这个对象，调用数组的相关方法，添加到当前data上的list中
    //04 注意：在vue中已经实现了数据的双向绑定，每当我们修改了data中的数据，vue会默认监听到数据改动
    //          自动把最新的数据，应用到页面上
    var car={id:this.id,name:this.name,ctime:new Date()};
    this.list.push(car);
    this.id=this.name=''
},
```

### 删除品牌

```JavaScript
del(id){//根据id删除数据
    //分析：
    //01 如何根据id找到要删除对象的索引
    //02 如果找到索引，直接调用数组的splice方法
    // this.list.some((item,i)=>{
    //     if(item.id==id){
    //         this.list.splice(i,1);
    //     //在数组的some中，如果return true，就会立即终止数组的后续循环
    //     return true;
    //
    // }
    // })

    var index=this.list.findIndex(item=>{
         if(item.id==id){
             return true;
    }
    });
    // console.log(index);
    this.list.splice(index,1);
},
```

### 根据条件筛选品牌

```JavaScript
search(keywords){//根据关键字，进行数据的搜索
    // var newList=[];
    // this.list.forEach(item=>{
    //     if(item.name.indexOf(keywords)!=-1){
    //         newList.push(item)
    // }
    // });
    // return newList;

    //注意：forEach some(return true执行终止) filter findIndex 这些都是数组的新方法
    //都会对数组中的每一项进行遍历，执行相关操作
    return this.list.filter(item=>{
        // if(item.name.indexOf(keywords)!=-1){}

        //注意：ES6中，为字符串提供了一个新方法叫做string.prototype.includes(‘要包含的字符串’)
        //如果包含，则返回true，否则返回false
        //jQuery里有个方法和includes方法一致   :contains('哈')
        if(item.name.includes(keywords)){
            return item
    }
    });
}
```

### 时间的格式化

```JavaScript
//全局过滤器，进行时间的格式化
Vue.filter('dateFormat',function (dataStr,pattern='') {
    //根据给定的时间字符串，得到特定的时间
    var dt=new Date(dataStr);

    //yyyy-mm-dd
    var y=dt.getFullYear();
    var m=dt.getMonth()+1;
    var d=dt.getDate();

    // return y+'-'+m+'-'+d
    // return `${y} - ${m} - ${d}`;
    if(pattern.toLowerCase()==='yyyy-mm-dd'){
        return `${y} - ${m} - ${d}`;
    }else {
        var hh=dt.getHours();
        var mm=dt.getMinutes();
        var ss=dt.getSeconds();

        return `${y} - ${m} - ${d} ${hh}:${mm}:${ss}`;
    }
});
```





1. 

 



1. 在2.x版本中[手动实现筛选的方式](https://cn.vuejs.org/v2/guide/list.html#显示过滤-排序结果)：

- 筛选框绑定到 VM 实例中的 `searchName` 属性：

```
<hr> 输入筛选名称：

<input type="text" v-model="searchName">

```

- 在使用 `v-for` 指令循环每一行数据的时候，不再直接 `item in list`，而是 `in` 一个 过滤的methods 方法，同时，把过滤条件`searchName`传递进去：

```
<tbody>

      <tr v-for="item in search(searchName)">

        <td>{{item.id}}</td>

        <td>{{item.name}}</td>

        <td>{{item.ctime}}</td>

        <td>

          <a href="#" @click.prevent="del(item.id)">删除</a>

        </td>

      </tr>

    </tbody>

```

- `search` 过滤方法中，使用 数组的 `filter` 方法进行过滤：

```
search(name) {

  return this.list.filter(x => {

    return x.name.indexOf(name) != -1;

  });

}

```

## Vue调试工具`vue-devtools`的安装步骤和使用

[Vue.js devtools - 翻墙安装方式 - 推荐](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=zh-CN)







## 过滤器

概念：Vue.js 允许你自定义过滤器，**可被用作一些常见的文本格式化**。过滤器可以用在两个地方：**mustache 插值和 v-bind 表达式**。过滤器应该被添加在 JavaScript 表达式的尾部，由“管道”符指示；

### 私有过滤器

1. HTML元素：

```
<td>{{item.ctime | dataFormat('yyyy-mm-dd')}}</td>

```

1. 私有 `filters` 定义方式：

```javascript
var vm2=new Vue({
        el: '#app2',
        data: {
            dt: new Date()
        },
        methods: {},
        filters: {//定义私有过滤器 过滤器有两个条件【过滤器名称 和 处理函数】
            dateFormat: function (dateStr, pattern='') {
                var dt = new Date(dateStr);

                //yyyy-mm-dd
                var y = dt.getFullYear();
                var m = (dt.getMonth() + 1).toString().padStart(2,'0');
                var d = dt.getDate().toString().padStart(2,'0');

                // return y+'-'+m+'-'+d
                // return `${y} - ${m} - ${d}`;
                if (pattern.toLowerCase() === 'yyyy-mm-dd') {
                    return `${y} - ${m} - ${d}`;
                } else {
                    var hh = dt.getHours().toString().padStart(2,'0');
                    var mm = dt.getMinutes().toString().padStart(2,'0');
                    var ss = dt.getSeconds().toString().padStart(2,'0');

                    return `${y} - ${m} - ${d} ${hh}:${mm}:${ss}~~~~~`;
                }
            }
        }
    })
```



> 使用ES6中的字符串新方法 String.prototype.padStart(maxLength, fillString='') 或 String.prototype.padEnd(maxLength, fillString='')来填充字符串；





### 全局过滤器

#### 过滤器调用时候的格式：

 {{name | 过滤器的名称}}

注意：过滤器管道符：|

```
<div id="app">
    <p>{{msg | msgFormat('疯狂','勇敢') | test}}</p>
</div>
```

#### 过滤器的定义语法：

Vue.filter('过滤器的名称',function () {})

注意：过滤器中的function，第一个参数，已经被规定死了，永远都是过滤器管道符前面传递过来的数据

```JavaScript
//定义一个vue全局的过滤器，名字叫 msgFormat
Vue.filter('msgFormat',function (msg,arg1,arg2) {
    return msg.replace(/单纯/g,arg1+arg2)//字符串的replace方法，第一个参数，除了可以写一个字符串之外，还可以定义一个正则
});
//定义第二个过滤器，名字叫 test
Vue.filter('test',function (msg) {
    return msg+'======'
});

var vm=new Vue({
    el:'#app',
    data:{
        msg:'曾经我也是一个单纯的少年，单纯的我傻傻的笑'
    },
    methods:{}
});
```

> 注意：当有局部和全局两个名称相同的过滤器时候，会以就近原则进行调用，即：局部过滤器优先于全局过滤器被调用！



## 键盘修饰符以及自定义键盘修饰符

### 全部的案件别名

- .enter
- .tab
- .delete
- .esc
- .space
- .up
- .down
- .left
- .right

### [2.x中自定义键盘修饰符](https://cn.vuejs.org/v2/guide/events.html#键值修饰符)

1. 通过`Vue.config.keyCodes.名称 = 按键值`来自定义案件修饰符的别名：

```javascript
//全局
Vue.config.keyCodes.f2 = 113;
```

1. 使用自定义的按键修饰符：

```
<input type="text" v-model="name" @keyup.f2="add">
```





## [自定义指令](https://cn.vuejs.org/v2/guide/custom-directive.html)

### 自定义全局 自定义指令：

```JavaScript
//使用Vue.directive()定义全局的指令v-focus
//其中：参数1：指令的名称，注意，在定义的时候，指令的名称前面不需要加v-前缀，在调用的时候必须在指令名称前加v-前缀
//参数2：是一个对象，在这个对象身上，有一些指令相关的函数，这些函数可以在特定的阶段，执行相关的操作
Vue.directive('focus',{
    bind:function (el) {//每当指令绑定到元素上的时候，会立即执行这个bind函数，只执行一次
        //注意：在每一个函数中，第一个参数永远是el，表示被绑定了指令的那个元素，在这个el参数是一个原生的js对象
        //在元素刚绑定了指令的时候，还没有插入到DOM中，这时候调用focus方法没有作用
        //因为一个元素，只有插入DOM之后，才能获取焦点
        // el.focus()
    },
    inserted:function (el) {//表示元素插入到DOM中的时候，会执行inserted，只触发一次
        el.focus()
    },
    updated:function () {//当VNode更新的时候，会执行updated，可能会触发多次
        
    }
});
```



```JavaScript
    //自定义一个设置字体颜色指令
    Vue.directive('color',{
        bind:function (el,binding) {
            //样式，只要通过指令绑定给了元素，不管这个元素有没有被插入到页面中去，这个元素肯定有了一个内联的样式
            //将来元素肯定会显示到页面中，这时候，浏览器的渲染引擎必然会解析样式，应用给这个元素
            el.style.color='red';

            // console.log(binding.name)//color
            // console.log(binding.value)//blue
            // console.log(binding.expression)//'blue'

            el.style.color=binding.value;
        }
    });
```



- 和就说js行为有关的，最好在inserted中去执行，防止js行为不生效
- 和样式相关的操作，一般都可以在bind中执行

```JavaScript
//自定义一个设置字体颜色指令
    Vue.directive('color',{
        bind:function (el) {
            el.style.color='red'
        }
    });
```

1. 自定义指令的使用方式：

```
<input type="text" class="form-control" v-model="keywords" v-focus v-color="'blue'">
```

### 自定义局部 自定义属性

```JavaScript
directives:{//自定义私有指令
    'fontweight':{
        bind:function (el,binding) {
            el.style.fontWeight=binding.value;
        }
    }
}
```

简写：

```JavaScript
'fontsize':function (el,binding) {//注意：这个function等同于把代码写到bind和update中去
    el.style.fontSize=parseInt(binding.value)+'px';
}
```



## [vue实例的生命周期](https://cn.vuejs.org/v2/guide/instance.html#实例生命周期)

- 什么是生命周期：从Vue实例创建、运行、到销毁期间，总是伴随着各种各样的事件，这些事件，统称为生命周期！
- [生命周期钩子](https://cn.vuejs.org/v2/api/#选项-生命周期钩子)：就是生命周期事件的别名而已；
- 生命周期钩子 = 生命周期函数 = 生命周期事件
- 主要的生命周期函数分类：

- 创建期间的生命周期函数：
  - beforeCreate：实例刚在内存中被创建出来，此时，还没有初始化好 data 和 methods 属性
  - **created：实例已经在内存中创建OK，此时 data 和 methods 已经创建OK，此时还没有开始 编译模板**
  - beforeMount：此时已经完成了模板的编译，但是还没有挂载到页面中
  - **mounted：此时，已经将编译好的模板，挂载到了页面指定的容器中显示**
- 运行期间的生命周期函数：

- beforeUpdate：状态更新之前执行此函数， 此时 data 中的状态值是最新的，但是界面上显示的 数据还是旧的，因为此时还没有开始重新渲染DOM节点
- updated：实例更新完毕之后调用此函数，此时 data 中的状态值 和 界面上显示的数据，都已经完成了更新，界面已经被重新渲染好了！

- 销毁期间的生命周期函数：

- beforeDestroy：实例销毁之前调用。在这一步，实例仍然完全可用。
- destroyed：Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

```JavaScript
// 创建 Vue 实例，得到 ViewModel
var vm = new Vue({
  el: '#app',
  data: {
    msg: 'ok'
  },
  methods: {
    show() {
      console.log('执行了show方法')
    }
  },
  beforeCreate() { // 这是我们遇到的第一个生命周期函数，表示实例完全被创建出来之前，会执行它
    // console.log(this.msg)
    // this.show()
    // 注意： 在 beforeCreate 生命周期函数执行的时候，data 和 methods 中的 数据都还没有没初始化
  },
  created() { // 这是遇到的第二个生命周期函数
    // console.log(this.msg)
    // this.show()
    //  在 created 中，data 和 methods 都已经被初始化好了！
    // 如果要调用 methods 中的方法，或者操作 data 中的数据，最早，只能在 created 中操作
  },
  beforeMount() { // 这是遇到的第3个生命周期函数，表示 模板已经在内存中编辑完成了，但是尚未把 模板渲染到 页面中
    // console.log(document.getElementById('h3').innerText)
    // 在 beforeMount 执行的时候，页面中的元素，还没有被真正替换过来，只是之前写的一些模板字符串
  },
  mounted() { // 这是遇到的第4个生命周期函数，表示，内存中的模板，已经真实的挂载到了页面中，用户已经可以看到渲染好的页面了
    // console.log(document.getElementById('h3').innerText)
    // 注意： mounted 是 实例创建期间的最后一个生命周期函数，当执行完 mounted 就表示，实例已经被完全创建好了，此时，如果没有其它操作的话，这个实例，就静静的 躺在我们的内存中，一动不动
  },


    
  // 接下来的是运行中的两个事件
  beforeUpdate() { // 这时候，表示 我们的界面还没有被更新【数据被更新了吗？  数据肯定被更新了】
    /* console.log('界面上元素的内容：' + document.getElementById('h3').innerText)
    console.log('data 中的 msg 数据是：' + this.msg) */
    // 得出结论： 当执行 beforeUpdate 的时候，页面中的显示的数据，还是旧的，此时 data 数据是最新的，页面尚未和 最新的数据保持同步
  },
  updated() {
    console.log('界面上元素的内容：' + document.getElementById('h3').innerText)
    console.log('data 中的 msg 数据是：' + this.msg)
    // updated 事件执行的时候，页面和 data 数据已经保持同步了，都是最新的
  }
});
```

```
<div id="app">
  <input type="button" value="修改msg" @click="msg='No'">
  <h3 id="h3">{{ msg }}</h3>
</div>
```

## [vue-resource 实现 get, post, jsonp请求](https://github.com/pagekit/vue-resource)

除了 vue-resource 之外，还可以使用 `axios` 的第三方包实现实现数据的请求

1. 之前的学习中，如何发起数据请求？
2. 常见的数据请求类型？  get  post jsonp
3. 测试的URL请求资源地址：

- get请求地址： http://vue.studyit.io/api/getlunbo    xujiajia  https://www.easy-mock.com/
- post请求地址：http://vue.studyit.io/api/post
- jsonp请求地址：http://vue.studyit.io/api/jsonp

1. JSONP的实现原理

- 由于浏览器的安全性限制，不允许AJAX访问 协议不同、域名不同、端口号不同的 数据接口，浏览器认为这种访问不安全；
- 可以通过动态创建script标签的形式，把script标签的src属性，指向数据接口的地址，因为script标签不存在跨域限制，这种数据获取方式，称作JSONP（注意：根据JSONP的实现原理，知晓，JSONP只支持Get请求）；
- 具体实现过程：

- 先在客户端定义一个回调方法，预定义对数据的操作；
- 再把这个回调方法的名称，通过URL传参的形式，提交到服务器的数据接口；
- 服务器数据接口组织好要发送给客户端的数据，再拿着客户端传递过来的回调方法名称，拼接出一个调用这个方法的字符串，发送给客户端去解析执行；
- 客户端拿到服务器返回的字符串之后，当作Script脚本去解析执行，这样就能够拿到JSONP的数据了；

- 带大家通过 Node.js ，来手动实现一个JSONP的请求例子；

```javascript
    const http = require('http');
    // 导入解析 URL 地址的核心模块
    const urlModule = require('url');

    const server = http.createServer();
    // 监听 服务器的 request 请求事件，处理每个请求
    server.on('request', (req, res) => {
      const url = req.url;

      // 解析客户端请求的URL地址
      var info = urlModule.parse(url, true);

      // 如果请求的 URL 地址是 /getjsonp ，则表示要获取JSONP类型的数据
      if (info.pathname === '/getjsonp') {
        // 获取客户端指定的回调函数的名称
        var cbName = info.query.callback;
        // 手动拼接要返回给客户端的数据对象
        var data = {
          name: 'zs',
          age: 22,
          gender: '男',
          hobby: ['吃饭', '睡觉', '运动']
        }
        // 拼接出一个方法的调用，在调用这个方法的时候，把要发送给客户端的数据，序列化为字符串，作为参数传递给这个调用的方法：
        var result = `${cbName}(${JSON.stringify(data)})`;
        // 将拼接好的方法的调用，返回给客户端去解析执行
        res.end(result);
      } else {
        res.end('404');
      }
    });

    server.listen(3000, () => {
      console.log('server running at http://127.0.0.1:3000');
    });
```

1. vue-resource 的配置步骤：

- 直接在页面中，通过`script`标签，引入 `vue-resource` 的脚本文件；
- 注意：引用的先后顺序是：先引用 `Vue` 的脚本文件，再引用 `vue-resource` 的脚本文件；

1. 发送get请求：

```javascript
getInfo() { // get 方式获取数据
  this.$http.get('http://127.0.0.1:8899/api/getlunbo').then(res => {
    console.log(res.body);
  })
}
```

1. 发送post请求：

```javascript
postInfo() {
  var url = 'http://127.0.0.1:8899/api/post';
  // post 方法接收三个参数：
  // 参数1： 要请求的URL地址
  // 参数2： 要发送的数据对象
  // 参数3： 指定post提交的编码类型为 application/x-www-form-urlencoded
  this.$http.post(url, { name: 'zs' }, { emulateJSON: true }).then(res => {
    console.log(res.body);
  });
}
```

1. 发送JSONP请求获取数据：

```javascript
jsonpInfo() { // JSONP形式从服务器获取数据
  var url = 'http://127.0.0.1:8899/api/jsonp';
  this.$http.jsonp(url).then(res => {
    console.log(res.body);
  });
}
```

