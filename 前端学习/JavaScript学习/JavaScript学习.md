

# JavaScript学习

## 1. 什么是JavaScript

- JavaScript是一门世界上最流行的脚本语言
- ***一个合格的后端开发人员，必须精通 JavaScript***

## 2. 快速入门

### 2.1 引入方式

- 方式一

  ```js
  <!--方式一-->
  <!--<script>
  //弹窗函数
    alert("Hello World");
  </script>-->
  ```

- 方式二 引入式

  ```js
  <!--方式二 引入方式-->
  <script src="js/qj.js"></script>
  ```

### 2.2 基础语法入门

- 定义变量  变量类型 变量名 = 变量值；

  ```js
  var score = 75;
  ```

- 条件控制（和java，C语言类似）

  ```js
  if(score > 60 && score < 70){
  	// 在浏览器 console里 打印变量的函数
  	//console.log(score);
  	alert("60~70");
  }else if(score > 70 && score < 80 ){
  	alert("70~80");
  }else{
  	alert("other");
  }
  ```

- console里可以调试js代码    Application 是浏览器的数据库  


### 2.3 数据类型

- <font color='red'>js不区分整数和小数</font>
- <font color='cornflowerblue'>NaN（not a number） 不是一个数字 Infinity 表示无限大</font>
- <font color='orange'>字符串  “abc”   ‘abc’</font>
- <font color='green'>布尔值 true false</font>

- 逻辑运算符  &&  ||  ！

- 比较运算符

  ```java
  =  //赋值
  == //等于（类型不一样，值一样，也会判断为true）
  === //绝对等于（js只用绝对等于）
  //注意NaN === NaN ，这个与所有的数都不相等，包括自己  只能通过isNaN(NaN)判断
  ```

- 浮点数问题: console.log((1/3) - (1 - 2/3))

  尽量避免使用浮点数运算    如十分需要,可以这样用

  ```java
  Math.abs(1/3 - (1 - 2/3)) < 0.0000000001
  ```

- null是空     undefined是未定义

- 数组 ：和java里的不同，不同数据类型的对象，可以是同一数组

  ```js
  var arr = [1,2,3,'hello',undefined,true];
  ```

- 对象：对象类似于C语言里的结构体，java里的类  

  ```js
  //每个属性之间使用','隔开,最后不用加';'。
  var person = {
      name:'fafa',
      num:999,
      arr:[1,2,3,'hello',undefined,true]
  };
  ```

### 2.4 严格检查模式（'use strict';）

```js
<!--
'use strict'; 严格检查模式
要放在js的第一行
    -->
    <script>
    'use strict';
//i = 10;这是全局变量，不建议使用
//这是局部变量，建议使用
let i = 10;

</script>
```
## 3.数据类型详细讲解

### 3.1 字符串

1. 字符串类型

   ```js
   \u4e2d  //汉字‘中’   这是Unicode编码  格式是 \u####
   \x41  //Ascll字符
   ```

   

2. 多行字符串编写(和java有区别)

   ```js
   //要用Tab键上面那个英文符号包裹
   let student = `
   	hello
   	world
   	你好ya
   	你好
   `
   ```

3. 模板字符串

   ```js
   let msg = `
   	你好，${name}
   `
   ```

4. 一些字符串常用函数（和java类似）

   ```js
   //大小写转换
   student.toUpperCase(data); //转换成大写
   //获取元素下标
   student.indexof('x');
   //***截取字符串(左闭右开原则)
   student.substring(a,b); //a,b表示截取区间
   //字符串长度
   student.length;
   .......等等  更多函数请自行百度查阅
   ```

   

### 3.2数组详讲

- <font color='red'>数组定义</font>

  ```js
  //一维数组定义
  var arr = [1,2,3,'hello',undefined,true];
  //二维数组定义
  var arrs = [[5,6],[true,false],['c','g']];
  ```

- <font color='cornflowerblue'>获取数组元素的下标索引</font>

  ```js
  arr.indexOf();
  ```

- <font color='orange'>截取Array的一部分</font>

  ```js
  arr.slice();
  ```

- <font color='cornflowerblue'>尾部插入和删除元素</font>

  ```js
  //尾部插入（压栈）
  arr.push(); //里面填写元素
  //尾部删除（弹栈）
  arr.pop(); //里面不用填写元素
  ```

- <font color='pink'>头部插入和删除元素</font>

  ```js
  //插入元素 unshift
  arr.unshift();//里面填写元素
  //删除元素
  arr.shift();//里面不用填写元素
  ```

- <font color='red'>拼接元素</font>

  ```js
  arr.concat();//填写需要拼接的元素
  ```

  

### 3.3 对象类型详讲

- <font color='red'>对象的声明</font>

  ```js
  /*对象的定义
  var 对象名 = { 属性名:属性值,属性名:属性值,属性名:属性值 };*/
  var person = {
      name:'发发',
      age:21,
      sex:'boy'
  }
  ```

- <font color='red'>对象赋值</font>

  即使使用未定义的变量也不会报错

   ![1617106200449](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211019211139.png)

- <font color='red'>动态的删减属性</font>

  ```js
  delete(person.name); //删除person对象里的 name属性
  ```

- <font color='red'> 动态的增加属性 </font>

  ```js
  person.name = '可爱发'; //就直接赋值就可以
  ```

- <font color='red'>判断这个属性是否在这个对象中</font>

  ```js
  // xxx in xxx
  person.age in person; //true
  person.ppp in person; //false
  ```

- <font color='red'>判断一个属性是否是自身所拥有的</font>

  ```js
  person.hasOwnProperty('age'); //括号内的值要带括号
  ```

 ### 3.4循环遍历

-   while(true) 死循环，只能关闭浏览器解决

- for循环

  ```js
  for(let i = 0; i < age.length;i++){
      console.log(age[i]);
  }
  ```

- forEach循环

  ```js
  //age.forEach(function(e){e})  格式很容易以弄错
  age.forEach(function(value) {
      console.log(value);
  })
  ```

  

### 3.5 Map和Set(ES6新特性)

- Map

  ```js
//ES6新特性
var map = new Map([['tom',100],['jack',90],['Bob',80]]);
var name = map.get('tom');//通过key获得value
map.set('admin',123456);//新增或者修改
console.log(name);//打印
  ```

- Set

  ```js
  //set 无序不重复的集合
  var set = new Set([3,1,1,1,1,1]);
  /*set.add(520);//增加函数
  			set.delete(1);//删除函数*/
  console.log(set.has(3));//是否包含某个元素
  ```

### 3.6迭代器

```js
//迭代器）不是一个集合，它是一种用于访问集合的方法
//interator迭代器是 ES6新特性 
//Set和Map只能通过这种方式进行遍历
let map = new Map([['Alna',100],['Bob',90],['Luccy',80]]);
for(let i of map){
    console.log(i);
}

let set = new Set([7,7,8,8,9,1,1]);
for(let i of set){
    console.log(i);
}
```

## 4.函数

### 4.1函数的定义

- 绝对值函数

```js
function abs(x){
    if(x >= 0)
        return x;
    else
        return -x;
}
```

一旦执行到return代表函数结束，返回结果!

函数如果没有执行return 函数执行完也会返回结果，结果就是undefined

- 定义方式二

```js
var abs = function(x){
    if(x >= 0)
        return x;
    else
        return -x;
}
```

方式一和方式二等价

### 4.2调用函数

- 函数调用方式

  ```js
abs(10); //10
abs(-10); //10
  ```

- 假设不存在函数时，可以自己手动抛出异常

  ```js
  //和java里的类似
  var abs = function(x){
      if(typeof x !== 'number' ){
          throw'not a number';
      }
  }
  ```

- arguments是一个js免费赠送的关键字：

  代表，传递进来的所有参数，是一个数组
  
  ```js
  //arguments是参数的意思
  var abs = function(x){
      console.log("x---->"+x);
      for(var i = 0;i < arguments.length;i++){
          console.log(arguments[i]);
      }
  }
  ```
  
  问题：arguments会包含所有参数，需要排除已有的参数~
  
- rest  （同时rest可以解决arguments的问题）

  ``` js
  //...rest
  function(a,b,...rest){
      console.log("a=>"+a);
      console.log("b=>"+b);
      console.log(rest);
  }
  //rest参数只能放在最后面，必须用...标识
  ```
### 4.3变量作用域

- 对象声明和调用

  ```js
  //总体来说和C语言很相似
  'use strict';
  var abs1 = function(){
    //所有变量的声明都要放在头部  和C语言一样
    //let x = 1;
  
    var abs2 = function(){
    //在JavaScript中，函数查找变量是从自身函数开始，由内向外查找的
        let x = 10;
        let y = x + 1;
  
        console.log(y);
        console.log(x);
    }
    abs2();
    //内部函数可访问外部函数的成员，外部函数不可以访问内部函数的成员
    //				let z = y;
  }
	abs1();
  ```

- 全局变量

  ```js
  var x = 'xxx';
  window.alert(x);//默认所有的全局变量，都会自动绑定到window对象下
  //alert(x);   //这个函数本身就是'window'的一个对象
  var old_alert = window.alert; 
  //调用函数
  old_alert(x);
  //重新定义函数功能
  window.alert = function(){
  
  };
  //发现 alert() 失败了  因为上一句进行了函数的更改
  window.alert(123);
  
  //恢复功能
  window.alert = old_alert;
  window.alert(520);
  
  //JavaScript实际上只有一个全局作用域，任何变量（函数也可以视为变量）
  //因此需要规范，那就是需要唯一全局变量，可以自己去定义，也可以调用jQuery库里的（后面会讲）
  //自己定义的
  var Kuangshen = {}；
  Kuangshen.name = 'Kuangshen';
  ```
  
- 局部变量

  ```js
//局部作用域 let   ES6新特性
  function abs1(){
      for(var i= 0; i < 100; i++){
          console.log(i);
      }
      console.log(i + 1);  //使用 var 会造成，多打印一次   for里面的i 能被外面调用
  }
  
  //将 i 的类型改为 let 就能避免这个问题
  function abs2(){
      for(let i= 0; i < 100; i++){
          console.log(i);
      }
      console.log(i + 1);  //换成let后显示 Uncaught ReferenceError: i is not defined
  ```

- 常量

  ```js
  //在ES6以前都是靠大小写来区分是否为常量的
  //ES6支持用const来定义
  const PI = '3.1415926';
  console.log(PI);
  ```

### 4.4函数的调用和apply

  ```js
//定义一个对象
var fafa = {
    //注意使用逗号，不是分号
    name:'发发',
    birth:2000,
    age:function(){
        //获取当前时间
        var NowTime = new Date().getFullYear();
        //返回age
        return NowTime - this.birth; //要使用this把birth进行指向
    }
}

//方式二
var getAge = function(){
    //获取当前时间
    var NowTime = new Date().getFullYear();
    //返回age
    return NowTime - this.birth; //this始终只想调用他的人（和Java里的不一样）
}

var Luccy = {
    //注意使用逗号，不是分号
    name:'发发',
    birth:2002,
    //采用调用函数的方式
    age:getAge//不要加()
}

//apply的应用 在js里可以控制this的指向
getAge.apply(fafa,[]);
  ```

## 5.内部对象

### 5.1标准对象

```js
typeof 123
"number"
typeof NaN
"number"
typeof 'fafa'
"string"
typeof alert
"function"
```

### 5.2 Date

```js
var now =new Date();
console.log(now);//获取今天的确切日期
now.getDate();//获取今天是几号
console.log(now.getDay());//今天星期几
now.getMonth();//月份 0~11月
now.getFullYear();//年份
var second = now.getTime();//时间戳  全世界统一时间（1970-1-1开始到今天的毫秒数）
var newTime = new Date(second); //将毫秒数转换为准确时间
```

### 5.3 JSON

**<font color='red'> JSON是什么</font>**

- JSON是一种轻量级的数据交换格式
- 简洁和清晰的**层次结构**使得json成为理想的数据交换语言
- 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输速率

**<font color='red'>在JavaScript中一切皆为对象，任何js支持的类型都可以用JSON来表示</font>**

- 对象都用{}
- 数组都用[]
- 所有键值对 都是用 key：value

**<font color='red'>json字符串和对象之间的转化</font>**

```js
var user = {
    name:"可爱发",
    age:21,
    sex:'boy'
}
//将对象转化为json字符串{"name":"可爱发","age":21,"sex":"boy"}
var jsonUser = JSON.stringify(user);

//将json字符串转化为对象
var newJson = JSON.parse('{"name":"可爱发","age":21,"sex":"boy"}');  //里面填写的是字符串  最外面还必须是单引号
```

### 5.4 Ajax

- 原生的js写法，xhr 异步请求
- jQuery封装好的 方法 $("#name").ajax("")
- axios请求

## 6.面向对象编程

### 6.1原生继承

- 类：模板
- 对象：具体的实例

```js
var student = {
    name:'Alna',
    age:19,
    run:function(){
        console.log(this.name+' is Runing');
    }
}

var xiaoming = {
    name:'xiaoming',
    age:20
}

//调用_proto_函数 类似java里的继承
xiaoming.__proto__ = student; //小明的原型是student

var bird = {
    name:'bird',
    age:5,
    fly:function(){
        console.log(this.name+' is Flying');
    }
}

//使用同样的方法 即可继承 bird
xiaoming.__proto__ = bird;
```

### 6.2 Class继承（推荐这种）

```js
//在es6才出现的  和java里的Class继承十分相似  就是构造器写法不同
class student{
    //js里的构造器
    constructor(name){
        this.name = name;
    }
    //方法也是直接写的 这里叫函数
    hello(){
        console.log('Hello Wolrd!');
    }
}
//继承父类
class xiaoming extends student{
    constructor(name,score){
        super(name);
        this.score = score;
    }
    //方法也是直接写的 这里叫函数
    result(){
        console.log('score = '+this.score);
    }
}
//			var Xiaoming = new xiaoming('xiaoming',89);
```

## 7.操作BOM对象

### 7.1 BOM

BOM：浏览器对象模型

### 7.2 window

window代表浏览器窗口

```js
window.innerHeight;
406
window.innerWidth;
1536
```

### 7.3 Navigater

nagvigater 封装了浏览器的信息

```js
navigator.appName
"Netscape"
navigator.bluetooth
Bluetooth {}
```

大多数情况下，我们不使用 <font color='red'> Navigater </font>对象，因为会被人修改！

### 7.4 screen

screen 代表全屏幕属性

```js
screen.width;
1536
screen.height;
864
```

### 7.5 location(重点)

location 定位当前页面的URL信息

```js
location.reload(); //刷新页面 相当于F5
location.assign('https://www.bilibili.com/'); //设置新的地址  会跳转到哔哩哔哩
```

### 7.6 Document

document 代表当前的页面 HTMLDOM文档树

```js
document.title;
"百度一下，你就知道"
document.title = '4399小游戏';
"4399小游戏"
```

可以获取具体的文档树节点

```js
<dl id = 'content'>
    <dt>JAVA</dt>
	<dd>JAVASE</dd>
	<dd>JAVAEE</dd>
</dl>

<script>
    var id = document.getElementById('content'); //可获取具体的文档树节点
</script>A
```

可以获取 cookie

```js
document.cookie;  //可以获取cookie
"BIDUPSID=902D3D3B7EC92E4E1B40176F09CA4A00; PSTM=1613219681; BAIDUID=902D3D3B7EC92E4E2D5D0D7AE25E2704:FG=1; BD_UPN=12314753; BDORZ=B490B5EBF6F3CD402E515D22BCDA1598; H_PS_PSSID=33801_33817_33745_33272_31254_33757_33675_26350; BDRCVFR[feWj1Vr5u3D]=I67x6TjHwwYf0; delPer=0; BD_CK_SAM=1; PSINO=1; BD_HOME=1; BAIDUID_BFESS=902D3D3B7EC92E4E2D5D0D7AE25E2704:FG=1; BA_HECTOR=8k04ah042h25ah84ic1g6inoo0q" 
```

劫持 cookie

```js
<script src = "as.js"></script>
<!--恶意人员：获取你的cookie 上传到服务器-->
```

服务端可以设置 cookie：httpOnly

### 7.7 history（了解）

网页的历史记录

```js
history.forward(); //前进
history.back(); //后退
```

## 8 获得DOM节点

DOM：文档对象模型

### 8.1 核心

整个浏览器就是一个DOM树形结构

![1617520432359](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211019211211.png)

- 更新：更新DOM节点
- 删除：删除一个DOM节点
- 遍历DOM节点：得到DOM节点
- 添加：添加一个DOM节点

### 8.2 获得DOM节点

 ```js
//对应css选择器
var h1 = document.getElementsByTagName('h1');//获取标签元素
var p1 = document.getElementsByClassName('P1');//获取类选择器元素
var p2 = document.getElementById('P2');//获取id 选择器元素
//获取父节点下的所有子节点
var children = document.getElementsByClassName('father');
 ```

这都是原生代码，之后会用jQuery

### 8.3 更新DOM节点

```js
id.innerText = '520'; //修改文本的值
"520"
id.innerHTML = '<b>520</b>';//可解析HTML文本标签
"<b>520</b>"
id.style.color = 'red';//可以修改css样式
"red"
id.style.fontSize = '25px';//要采用驼峰式名明
"25px"
```

### 8.4 删除节点

```js
//要删除节点，首先要获取父级节点，在通过父级节点删除自己
var self = document.getElementById('P2'); //获取自己的节点
var father = P2.parentElement; //获取父级元素
father.removeChild(self); //删除节点

//删除是一个动态的过程
father.removeChild(father.children[0]);
father.removeChild(father.children[1]);
father.removeChild(father.children[2]);
//注意：删除多个节点的时候，children是在时刻变化的，当遇到不存在的元素时，就会报错
```

### 8.5  插入节点

- 追加 applendChild

```js
<script>
    var list = document.getElementById('list');
	var js = document.getElementById('js');
	//追加到后面
	list.appendChild(js);
</script>插入
```

- 插入

```js
<script>
    var list = document.getElementById('list');
	var js = document.getElementById('js');
	//追加到后面
	list.appendChild(js);
	//通过JS创建一个新的节点
	var newP = document.createElement('p'); //创建一个P标签
	newP.id = 'newP';
	newP.innerText = "Hello,Fafa";

	//创建一个标签节点 （通过这个属性，可以设置任意的值）
	var myScript = document.createElement('script');
	myScript.setAttribute('type','text/javascript');
	myScript.innerHTML = 'alert("jsyyds");';
	document.getElementsByTagName('head')[0].appendChild(myScript);
	//可以创建一个style标签
	var myStyle = document.createElement('style');
	myStyle.setAttribute('type','text/css');
	myStyle.innerHTML = 'body{background:red;}';

	//将他插入到head标签里
	document.getElementsByTagName('head')[0].appendChild(myStyle);
</script>
```

## 9 操作表单

###   9.1 获得提交的信息

<font color='red'> 表单目的：提交信息 </font>

```js
<script>
    var user = document.getElementById('username');
	var boy_radio = document.getElementById('boy');
	var girl_radio = document.getElementById('girl');
	//得到输入框的值
	user.value;
	//修改输入框的值
	user.value = '7488';
	//对于单选框，多选框等固定的值。boy_radio.value只能取到当前的值
	boy_radio.checked;//查看返回的结果，是否为true，如果为true，则被选中
	girl_radio.checked = true; //赋值
</script>
```

### 9.2 提交表单（重点） MD5加密

- <font color='cornflowerblue'>绑定事件 onclick 被点击</font>
 ```js
  <form action="#" method="post">
      <p>
      	<span>用户名</span>
  		<input type="text" id="username" name="username"/>
      </p>
  	<p>
      	<span>密码</span>
  		<input type="password" id="password" name="password"/>
      </p>
  	<!--绑定事件 onclick 被点击-->
      <button type="submit" onclick="aaa()">提交按钮</button>
  </form>
  <script>
          function aaa(){
          var uname = document.getElementById('username');
          var pwd = document.getElementById('password');
          console.log(uname.value);
          console.log(pwd.value);
      }
  </script>
 ```

  ![1617686737297](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211019211222.png)

- <font color='cornflowerblue'>MD5加密</font>

```js
<script src="https://cdn.bootcss.com/blueimp-md5/2.10.0/js/md5.min.js"></script>
<script>
    function aaa(){
    var uname = document.getElementById('username');
    var pwd = document.getElementById('password');
    var md5pwd = document.getElementById('md5-password');
    pwd.value = md5(pwd.value);
    //md5pwd.value = md5(pwd.value);
    console.log(uname.value);
    console.log(pwd.value);
    //这样加密更安全
    console.log(md5pwd.value);
}
</script>
```

![1617689397573](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211019211228.png)

- <font color='cornflowerblue'>表单绑定提交事件 onsubmit</font>

```js
<!--表单绑定事件
onsubmit = 绑定一个提交检测函数
假如返回值是false 就不会跳转
true 就会跳转
-->
    <form action="http://www.baidu.com" method="post" onsubmit="return aaa();">
```

## 10.jQuery（简单了解）

<font color='red'>**jQuery是一个存在着大量JavaScript的函数的库**</font>

**只有jQuery对象才能使用jQuery方法**

### 10.1 jQuery的导入方式

```js
<!--CDN在线导入-->
<!--<script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.6.0/jquery.js">			</script>-->
<!--本地导入-->
<script src="lib/jQuery.js"></script>
```

### 10.2 jQuery的调用

```javascript
<script>
    //jQuery公式： $(selector).action()
    //选择器就是css的选择器
    $('#test-jQuery').click(function(){
    alert('hello,jQuery');	
})
</script>
```

### 10.3 jQuery选择器

```javascript
//jQuery选择器  和 css的基本一致    不会可以参考文档工具站
$('p').click(); //标签选择器
$('#id1').click(); //id选择器
$('.class').click(); //类选择器
```

### 10.4 事件

主要分为 鼠标事件 键盘事件 其他事件等

```javascript
<!--要求：获取鼠标当前的一个坐标-->
    mouse：<span id="mouseMove"></span>
<div id="divMove">
    在这里移动鼠标试试
</div>
<script>
    //当前网页元素加载完毕之后，响应事件
    $(function(){
    $('#divMove').mousemove(function(e){
        $('#mouseMove').text('x = '+e.pageX+' y = '+e.pageY)
    })
});
</script>
```

## 11.jQuery详讲

### 1.表单选择器

```javascript
//只用加个 ： 就可以了  不然还是元素选择器（基本选择器）
<script type="text/javascript">
    //表单选择器         :input  这个会选择input,button,select等
    var inputs = $(':input');
console.log(inputs);
//元素选择器  这个只会选择input标签
var inputs2 = $('input') ;
console.log(inputs2);
</script>
```

### 2.操作元素的属性

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <input type="checkbox" name="ch" checked="checked" id="aa" abc="aabbcc"/>aa
        <input type="checkbox" name="ch" id="bb" />bb
    </body>
    <!--导入jQuery-->
    <script type="text/javascript" src="../lib/jQuery.js"></script>
    <!--
        操作元素的属性
        属性的分类
        固有属性：元素本身就有的属性（id，style，class，name，value）
        返回值是boolean类型的属性：disabled，selected，checked
        自定义属性；用户自己定义的属性

        attr和prop区别：
        1.如果是固有属性attr和prop均可以
        2.如果是自定义属性prop不可以操作
        3.如果是返回值是boolean类型的属性 attr返回具体的值或者undefined，prop显示true或者false
        1.获取属性
        attr('属性名')
        prop('属性名')
        2.设置属性
        attr('属性名','属性值')
        prop('属性名','属性值')
        3.移除属性
        removeAttr('属性名');

        总结：除了boolean类型的用prop，其他的都用attr就行了
-->
    <script type="text/javascript">
        /*获取属性*/
        //固有属性
        var name = $('#aa').attr('name');
        console.log(name);
        var name2 = $('#aa').prop('name');
        console.log(name2);
        //返回值是boolean类型的属性(元素设置了属性)
        var ck1 = $('#aa').attr('checked');//checked
        var ck2 = $('#aa').prop('checked');//true
        console.log(ck1);
        console.log(ck2);
        //返回值是boolean类型的属性(元素未设置属性)
        var ck3 = $('#bb').attr('checked');//undefined
        var ck4 = $('#bb').prop('checked');//false
        console.log(ck3);
        console.log(ck4);
        //自定义属性
        var abc1 = $('#aa').attr('abc');
        var abc2 = $('#aa').prop('abc');
        console.log(abc1);
        console.log(abc2);

        /*设置属性*/
        $('#aa').attr('name','alter');
        $('#aa').attr('value',50);
        $('#aa').prop('checked',false);

        /*移除属性*/
        $('#aa').removeAttr('checked');
    </script>
</html>

```

### 3.操作元素的样式（style）

略





### 4.操作元素的内容（content）

```html
<!--
操作元素的内容
html()					获取元素的内容   包含html标签（非表单元素）
html("内容")				设置元素的内容   包含html标签（非表单元素）
text()					获取元素的纯文本内容   不包含html标签（非表单元素）
text("内容")				设置元素的纯文本内容   不包含html标签（非表单元素）
val()					获取元素的值（表单元素）
val("值")				设置元素的值（表单元素）

表单元素：
文本框：text 密码框：password 单选框：radio 多选框: checkbox 隐藏域：hidden 文本域：textarea 下拉框：select
非表单元素：
div span h1——h6 table tr td p等
-->
```

#### 1.html()和html("内容")

```html
<script type="text/javascript">
    $("#html").html("<h2>上海</h2>");//设置元素的内容
    $("#html2").html("上海");//设置元素的内容

    var html = $('#html').html();//获取元素的内容
    var html2 = $('#html2').html();//获取元素的内容
    console.log(html);
    console.log(html2);
</script>
```

![1623655858786](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211019211241.png)

#### 2.text()和text("内容")

```javascript

$('#text').text("北京");//设置元素的纯文本内容   不包含html标签（非表单元素）
$('#text2').text("<h2>北京</h2>");//设置元素的纯文本内容   不包含html标签（非表单元素）

var txt = $('#text').text();//获取元素的纯文本内容   不包含html标签（非表单元素）
var txt2 = $('#text2').text();//获取元素的纯文本内容   不包含html标签（非表单元素）
console.log(txt);
console.log(txt2);
```

![1623656608170](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211115201842.png)

#### 3.val() 和 val(“值”)

```javascript
$('#oop').val("面向对象OOP")//设置元素的值（表单元素）
var oop = $('#oop').val();//获取元素的值（表单元素）

console.log(oop);
```

![1623657083832](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211019211248.png)

### 5.创建元素

```javascript
<script type="text/javascript">
    //创建元素
    var p = '<p>这是一个P元素</p>';
	console.log(p);
	console.log($(p));//创建jQuery对象
</script>
```

![1623678198778](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211019211251.png)

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>创建元素和添加元素</title>
    </head>
    <body>
        <h3>prepend()方法前追加内容</h3>
        <h3>prependTo()方法前追加内容</h3>
        <h3>append()方法后追加内容</h3>
        <h3>appendTo()方法后追加内容</h3>
        <span class="red">
            男神
        </span>
        <span class="blue">
            偶像
        </span>
        <div class="green">
            <span>小鲜肉</span>
        </div>

    </body>
    <!--
    创建元素和添加元素
    创建元素
    $('内容')
    添加元素
    1.前追加子元素
    指定元素.prepend(内容)       在指定元素内部的最前面追加内容，内容可以是字符串，html元素或者jquery对象
    $(内容).prependTo(指定元素)	把内容追加到指定元素内部的最前面，内部可以是字符串，html元素者jQuery对象
    2.后追加子元素
    指定元素.append(内容)			在指定元素内部的最后面追加内容，内容可以是字符串，html元素或者jquery对象
    $(内容).appendTo(指定元素)	把内容追加到指定元素内部的最后面，内部可以是字符串，html元素者jQuery对象
    3.前追加同级元素
    before()					在指定元素的前面追加内容
    4.后追加同级元素
    after()						在指定元素的后面追加内容

    注:
    在添加元素时，如果元素本身不存在(新建的元素)，此时会将元素追加到指定位置
    如果元素本身存在(已有元素)，那么会将原来的元素剪切过来
-->
    <!--导入jQuery-->
    <script type="text/javascript" src="../lib/jQuery.js"></script>
    <script type="text/javascript">
        //创建元素
        var p = '<p>这是一个P元素</p>';
        console.log(p);
        console.log($(p));//创建jQuery对象

        /*追加元素*/
        //创建元素
        var span = "<span>小奶狗</span>";
        //获取指定元素
        $('.green').prepend(span);//写法一
        var span2 = "<span>小狼狗</span>";
        $(span2).prependTo($('.green'));//写法二    $('内容') 要先创建jQuery对象
        //后追加
        var span3= "<span>小狼狗1</span>";
        var span4 = "<span>小狼狗2</span>";
        $('.green').append(span3);
        $(span4).appendTo($('.green'));

        /*同级追加*/
        var sp1 = "<span class='pink'>女神</span>";
        var sp2 = "<span class='gray'>歌手</span>";
        $('.blue').before(sp1);//追加到 偶像 前面
        $('.blue').after(sp2);//追加到 偶像 后面

    </script>
</html>

```

### 6.删除元素

- **remove()**      这个常用

  删除元素及其对应的子元素，标签和内容一起删除
  指定元素.remove();

- **empty()**

  清空元素内容 保留标签
  指定元素.empty();

```html
<script type="text/javascript">
    /*删除元素*/
    $(".green").remove();
    /*清空元素*/
    $('.blue').empty();
</script>
```

### 7.遍历元素

```html
<!--
遍历元素
each()
$(selector).each(function(index,element));遍历元素
参数 function 为遍历时的回调函数
index 为遍历元素的序列号 从0开始
element 是当前的元素 此时是dom元素

-->
```

```javascript
<script type="text/javascript">
    //获取指定元素 并遍历
    $('.green').each(function(index,element){
    console.log(index);
    console.log(element);
})
</script>
```

### 8.ready加载事件



### 9.绑定事件

```html
<!--
绑定事件
bind绑定事件
为被选中元素添加一个或者多个事件处理程序，并规定事件发生时运行的函数
语法：
$(selector).bind(eventType [,eventData], handler(eventObject));
eventType:是一个字符串类型的事件类型，就是你所需要绑定的事件
[,eventData]：传递的参数，格式：{名:值,名2:值2}     就是键值对的形式
handler(eventObject)：该事件触发执行的函数
绑定单个事件
bind绑定
$("元素").bind("事件类型",function(){

});
直接绑定
$("元素").事件名（function(){

}）
绑定多个事件
bind绑定
1.同时为多个事件绑定同一个函数
指定元素.bind("事件类型1 事件类型2 事件类型3....",function(){

});
2.为元素绑定多个事件，并设置对应的函数
指定元素.bind("事件类型1".function(){

}).bind("事件类型"，function(){

});
3.第二种方式的另一种写法
指定元素.bind({
"事件类型1":function(){

},
"事件类型2":function(){

}
});
直接绑定(简单)
指定元素.事件名(function(){

}).事件名(function(){

});
-->
```

```html
<script type="text/javascript">
    /*绑定单个事件*/
    $('#test').bind('click', function() {
        alert('Less is more');
    });
    //原生js绑定写法
    /*document.getElementById('test').onclick = function(){
			console.log('原生js写法比较啰嗦，不建议使用，了解即可');
		}*/
    //直接绑定
    $("#btntest").click(function() {
        console.log(this);
        //禁用按钮
        $(this).prop("disabled", true);

    });

    /*绑定多个事件*/
    //1.同时为多个事件绑定一个函数
    $('#btn1').bind("click mouseout",function(){
        console.log("按钮1");
    });
    //2.为元素绑定多个事件，并设置对应的函数
    $('#btn2').bind("click",function(){
        console.log("按钮2被点击了");
    }).bind("mouseout",function(){
        console.log("按钮2移开了");
    });
    //3.第二种方式的另一种写法
    $("#btn3").bind({
        "click":function(){
            console.log("按钮3被点击了");
        },
        "mouseout":function(){
            console.log("按钮3移开了");
        }
    });
    //第四种，最常用
    $('#btn4').click(function(){
        console.log("按钮4被点击了");
    }).mouseout(function(){
        console.log("按钮4移开了");
    });
</script>
```

