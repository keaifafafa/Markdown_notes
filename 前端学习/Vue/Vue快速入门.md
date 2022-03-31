# Vue

## 1、第一个Vue程序

### 1.1、什么是MVVM

MVVM（Model-View-ViewModel）是一种软件设计模式，由微软WPF（用于替代WinForm，以前就是用这个技术开发桌面应用程序的）和Silverlight（类似于Java Applet，简单点说就是在浏览器上运行WPF）的架构师Ken Cooper和Ted Peters开发，是一种简化用户界面的事件驱动编程方式。由John Gossman（同样也是WPF和Sliverlight的架构师）与2005年在他的博客上发表。

MVVM源自于经典的MVC（Model-View-Controller）模式。MVVM的核心是ViewModel层，负责转换Model中的数据对象来让数据变得更容易管理和使用。其作用如下：

- 该层向上与视图层进行双向数据绑定
- 向下与Model层通过接口请求进行数据交互

![20-1](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210920233126.png)

MVVM已经相当成熟了，主要运用但不仅仅在网络应用程序开发中。当下流行的MVVM框架有`Vue.js`，`Anfular JS`

### 1.2、为什么要使用MVVM

MVVM模式和MVC模式一样，主要目的是分离视图（View）和模型（Model），有几大好处

- 低耦合：视图（View）可以独立于Model变化和修改，一个ViewModel可以绑定到不同的View上，当View变化的时候Model可以不变，当Model变化的时候View也可以不变。
- 可复用：你可以把一些视图逻辑放在一个ViewModel里面，让很多View重用这段视图逻辑。
  独立开发：开发人员可以专注于业务逻辑和数据的开发（ViewMode），设计人员可以专注于页面设计。
- 可测试：界面素来是比较难以测试的，而现在测试可以针对ViewModel来写。

![20-2](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210920233300.png)

（1）View

View是视图层， 也就是用户界面。前端主要由HTH L和csS来构建， 为了更方便地展现vi eu to del或者Hodel层的数据， 已经产生了各种各样的前后端模板语言， 比如FreeMarker，Thyme leaf等等， 各大MV VM框架如Vue.js.Angular JS， EJS等也都有自己用来构建用户界面的内置模板语言。

（2）Model

Model是指数据模型， 泛指后端进行的各种业务逻辑处理和数据操控， 主要围绕数据库系统展开。这里的难点主要在于需要和前端约定统一的接口规则

（3）ViewModel

ViewModel是由前端开发人员组织生成和维护的视图数据层。在这一层， 前端开发者对从后端获取的Model数据进行转换处理， 做二次封装， 以生成符合View层使用预期的视图数据模型。
  需要注意的是View Model所封装出来的数据模型包括视图的状态和行为两部分， 而Model层的数据模型是只包含状态的

比如页面的这一块展示什么，那一块展示什么这些都属于视图状态(展示)
页面加载进来时发生什么，点击这一块发生什么，这一块滚动时发生什么这些都属于视图行为(交互)
视图状态和行为都封装在了View Model里。这样的封装使得View Model可以完整地去描述View层。由于实现了双向绑定， View Model的内容会实时展现在View层， 这是激动人心的， 因为前端开发者再也不必低效又麻烦地通过操纵DOM去更新视图。
  MVVM框架已经把最脏最累的一块做好了， 我们开发者只需要处理和维护View Model， 更新数据视图就会自动得到相应更新，真正实现事件驱动编程。
  View层展现的不是Model层的数据， 而是ViewModel的数据， 由ViewModel负责与Model层交互， 这就完全解耦了View层和Model层， 这个解耦是至关重要的， 它是前后端分离方案实施的重要一环。

### 1.3、Vue

Vue(读音/vju/， 类似于view) 是一套用于构建用户界面的渐进式框架， 发布于2014年2月。与其它大型框架不同的是， Vue被设计为可以自底向上逐层应用。Vue的核心库只关注视图层， 不仅易于上手， 还便于与第三方库(如：vue-router，vue-resource，vue x) 或既有项目整合。

**（1）MVVM模式的实现者**

Model：模型层， 在这里表示JavaScript对象
View：视图层， 在这里表示DOM(HTML操作的元素)
ViewModel：连接视图和数据的中间件， Vue.js就是MVVM中的View Model层的实现者
在MVVM架构中， 是不允许数据和视图直接通信的， 只能通过ViewModel来通信， 而View Model就是定义了一个Observer观察者

ViewModel能够观察到数据的变化， 并对视图对应的内容进行更新
ViewModel能够监听到视图的变化， 并能够通知数据发生改变
至此， 我们就明白了， Vue.js就是一个MV VM的实现者， 他的核心就是实现了DOM监听与数据绑定

**（2）为什么要使用Vue.js**

轻量级， 体积小是一个重要指标。Vue.js压缩后有只有20多kb(Angular压缩后56kb+，React压缩后44kb+)
移动优先。更适合移动端， 比如移动端的Touch事件
易上手，学习曲线平稳，文档齐全
吸取了Angular(模块化) 和React(虚拟DOＭ) 的长处， 并拥有自己独特的功能，如：计算属性
开源，社区活跃度高

### 1.4、第一个Vue程序

> ==下载并引入Vue.js==

- 开发版本
  包含完整的警告和调试模式：https：//yuejs.org/js/vue.js
  删除了警告， 30.96KB min+gzip：https：//vuejs.org/js/vue.min.js

- CDN

  ```html
  <script src=“https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.js”></script>
  <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
  ```

> ==编写代码==

Vue.js的核心是实现了MVVM模式， 她扮演的角色就是View Model层， 那么所谓的第一个应用程序就是展示她的数据绑定功能，操作流程如下：

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>第一个Vue程序</title>
    </head>
    <body>
        <div id="app">
            <!-- 方式一 -->
            <!-- {{msg}} -->
            <!-- 方式二  可以利用绑定元素的方式-->
            <span v-bind:title="msg">
                鼠标悬停几秒看看！
            </span>
        </div>
    </body>

    <!-- 导入Vue cdn -->
    <!-- <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script> -->
    <!-- 导入vue.js -->
    <script src="./js/vue.js"></script>
    <!-- 编写js -->
    <script>
        let vm = new Vue({
            el:"#app",
            /* Model:数据 */
            data: {
                msg:"Hello Vue!"
            }
        });
    </script>
</html>
```

## 2、基础语法指令

### 2.1、v-bind

我们已经成功创建了第一个Vue应用!看起来这跟渲染一个字符串模板非常类似， 但是Vue在背后做了大量工作。现在数据和DOM已经被建立了关联， 所有东西都是响应式的。我们在控制台操作对象属性，界面可以实时更新!
  我们还可以使用v-bind来绑定元素特性!
  **上代码**

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>

    </head>
    <body>

        <!--view层，模板-->
        <div id="app">
            <span v-bind:title="message">
                鼠标悬停几秒钟查看此处动态绑定的提示信息！
            </span>
        </div>

        <!--1.导入Vue.js-->
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
        <script type="text/javascript">
            var vm = new Vue({
                el:"#app",
                /*Model：数据*/
                data:{
                    message: '页面加载于 ' + new Date().toLocaleString()
                }
            });
        </script>
    </body>
</html>
```

你看到的v-bind等被称为指令。指令带有前缀v以表示它们是Vue提供的特殊特性。可能你已经猜到了， 它们会在渲染的DOM上应用特殊的响应式行为在这里，该指令的意思是：“将这个元素节点的title特性和Vue实例的message属性保持一致”。
  如果你再次打开浏览器的JavaScript控制台， 输入app， message=‘新消息’，就会再一次看到这个绑定了title特性的HTML已经进行了更新。

### 2.2、v-if，v-else

什么是条件判断语句，就不需要我说明了吧，以下两个属性!

- v-if
- v-else

**上代码**

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
        <!--view层，模板-->
        <div id="app">
            <h1 v-if="ok">Yes</h1>
            <h1 v-else>No</h1>

        </div>

        <!--1.导入Vue.js-->
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
        <script type="text/javascript">
            var vm = new Vue({
                el:"#app",
                /*Model：数据*/
                data:{
                    ok: false
                }
            });
        </script>
    </body>
</html>

```

**测试：**
			1.在浏览器上运行，打开控制台!
			2.在控制台输入`vm.ok=false`然后回车，你会发现浏览器中显示的内容会直接变成NO
  	注：使用`v-*`属性绑定数据是不需要`双花括号`包裹的

**v-else-if**

- v-if
- v-else-if
- v-else
  注：`===`三个等号在JS中表示绝对等于(就是数据与类型都要相等)上代码：

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
        <!--view层，模板-->
        <div id="app">
            <h1 v-if="type==='A'">A</h1>
            <h1 v-else-if="type==='B'">B</h1>
            <h1 v-else-if="type==='D'">D</h1>
            <h1 v-else>C</h1>

        </div>

        <!--1.导入Vue.js-->
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
        <script type="text/javascript">
            var vm = new Vue({
                el:"#app",
                /*Model：数据*/
                data:{
                    type: 'A'
                }
            });
        </script>
    </body>
</html>

```

### 2.3、v-for

- v-for

格式说明：

```html
<div id="app">
    <li v-for="(item,index) in items">
        {{item.message}}---{{index}}
    </li>

</div>
123456
```

注：`items`是数组，`item`是数组元素迭代的别名。我们之后学习的Thymeleaf模板引擎的语法和这个十分的相似！
  上代码：

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
        <!--view层，模板-->
        <div id="app">
            <li v-for="(item,index) in items">
                {{item.message}}---{{index}}
            </li>

        </div>

        <!--1.导入Vue.js-->
        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
        <script type="text/javascript">
            var vm = new Vue({
                el:"#app",
                /*Model：数据*/
                data:{
                    items:[
                        {message:'狂神说Java'},
                        {message:'狂神说前端'},
                        {message:'狂神说运维'}
                    ]
                }
            });
        </script>
    </body>
</html>
```

测试：在控制台输入`vm.items.push({message：'狂神说运维'})`，尝试追加一条数据，你会发现浏览器中显示的内容会增加一条`狂神说运维`.

### 2.4、v-on

`v-on`监听事件
 emsp;事件有Vue的事件、和前端页面本身的一些事件!我们这里的`click`是vue的事件， 可以绑定到Vue中的`methods`中的方法事件!
  **上代码**：

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>事件绑定</title>
    </head>
    <body>

        <div id="app">
            <!-- 官方还有很多玩法！ -->
            <!-- 写法一 -->
            <button v-on:click="warn()">Please Click Me！</button>
            <!-- 写法二 -->
            <button @click="warn()">Please Click Me！</button>
        </div>

    </body>
    <script src="./js/vue.js"></script>
    <script>
        let vm = new Vue({
            el: "#app",
            data:{
                msg: "Waring!"
            },
            // 注意是 methods ！
            methods:{
                warn: function(){
                    alert(this.msg);
                }
            }
        }) 
    </script>
</html>
```

**点击测试**
  Vue还有一些基本的使用方式， 大家有需要的可以再跟着官方文档看看， 因为这些基本的指令几乎我们都见过了，一通百通!掌握学习的方式!

## 3、表单双绑、组件

### 3.1、什么是双向数据绑定

Vue.js是一个MV VM框架， 即数据双向绑定， 即当数据发生变化的时候， 视图也就发生变化， 当视图发生变化的时候，数据也会跟着同步变化。这也算是Vue.js的精髓之处了。
  值得注意的是，我们所说的数据双向绑定，一定是对于UI控件来说的非UI控件不会涉及到数据双向绑定。单向数据绑定是使用状态管理工具的前提。如果我们使用vue x那么数据流也是单项的，这时就会和双向数据绑定有冲突。

（1）为什么要实现数据的双向绑定

在Vue.js中，如果使用vuex， 实际上数据还是单向的， 之所以说是数据双向绑定，这是用的UI控件来说， 对于我们处理表单， Vue.js的双向数据绑定用起来就特别舒服了。即两者并不互斥，在全局性数据流使用单项，方便跟踪；局部性数据流使用双向，简单易操作。

### 3.2、在表单中使用双向数据绑定

你可以用v-model指令在表单、及元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。尽管有些神奇， 但v-model本质上不过是语法糖。它负责监听用户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。
  注意：v-model会忽略所有表单元素的value、checked、selected特性的初始值而总是将Vue实例的数据作为数据来源。你应该通过JavaScript在组件的data选项中声明初始值!

#### **（1）单行文本**

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
        <div id="app">
            输入的文本：<input type="text" v-model="message" value="hello"/>
            <span>{{message}}</span>
        </div>

        <script src="./js/vue.js"></script>
        <script type="text/javascript">
            var vm = new Vue({
                el:"#app",
                data:{
                    message:""
                }
            });
        </script>
    </body>
</html>
```

#### **（2）多行文本**

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
        <div id="app">
            多行文本：<textarea v-model="pan"></textarea>&nbsp;&nbsp;多行文本是：{{pan}}
        </div>

        <script src="./js/vue.js"></script>
        <script type="text/javascript">
            var vm = new Vue({
                el:"#app",
                data:{
                    message:"Hello hello!"
                }
            });
        </script>
    </body>
</html>

```

#### **（3）单复选框**

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>

        <div id="app">
            单复选框：
            <input type="checkbox" id="checkbox" v-model="checked">
            &nbsp;&nbsp;
            <label for="checkbox">{{checked}}</label>
        </div>

        <script src="../js/vue.js"></script>
        <script type="text/javascript">
            var vm = new Vue({
                el:"#app",
                data:{
                    checked:false
                }
            });
        </script>
    </body>
</html>
```

#### （**4**）**多复选框**

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>

        <div id="app">
            多复选框：
            <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
            &nbsp;&nbsp;
            <label for="jack">Jack</label>
            <input type="checkbox" id="join" value="Join" v-model="checkedNames">
            &nbsp;&nbsp;
            <label for="join">Jack</label>
            <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
            &nbsp;&nbsp;
            <label for="mike">Mike</label>
            <span>选中的值：{{checkedNames}}</span>
        </div>

        <script src="./js/vue.js"></script>
        <script type="text/javascript">
            var vm = new Vue({
                el:"#app",
                data:{
                    checkedNames:[]
                }
            });
        </script>
    </body>
</html>

```

#### **（5）单选按钮**

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>

        <div id="app">
            单选框按钮
            <input type="radio" id="one" value="One" v-model="picked">
            <label for="one">One</label>
            <input type="radio" id="two" value="Two" v-model="picked">
            <label for="two">Two</label>
            <span>选中的值：{{picked}}</span>
        </div>

        <script src="../js/vue.js"></script>
        <script type="text/javascript">
            var vm = new Vue({
                el:"#app",
                data:{
                    picked:'Two'
                }
            });
        </script>
    </body>
</html>
```

#### **（6）下拉框**

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
        <div id="app">
            <!--    性别：
<input type="radio" name="sex" value="男" v-model="pan">男
<input type="radio" name="sex" value="女" v-model="pan">女
<p>选中了：{{pan}}</p>-->

            下拉框:
            <select v-model="pan">
                <option value="" disabled>---请选择---</option>
                <option>A</option>
                <option>B</option>
                <option>C</option>
                <option>D</option>
            </select>
            <span>value:{{pan}}</span>



        </div>

        <script src="../js/vue.js"></script>
        <script type="text/javascript">
            var vm = new Vue({
                el:"#app",
                data:{
                    pan:"A"
                }
            });
        </script>
    </body>
</html>

```



注意：`v-model`表达式的初始值未能匹配任何选项，元系将被渲染为“未选中”状态。 在iOS中， 这会使用户无法选择第一个选项，因为这样的情况下，iOS不会触发`change`事件。因此，更推荐像上面这样提供一个值为空的禁用选项。

### 3.3、什么是组件

组件是可复用的`Vue`实例， 说白了就是一组可以重复使用的模板， 跟`JSTL`的自定义标签、`Thymeleal`的`th:fragment`等框架有着异曲同工之妙，通常一个应用会以一棵嵌套的组件树的形式来组织：

 ![20-4](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210921000132.png)

 ![20-3](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210921000136.png)

例如，你可能会有页头、侧边栏、内容区等组件，每个组件又包含了其它的像导航链接、博文之类的组件。

#### **（1）第一个Vue组件**

注意：在实际开发中，我们并不会用以下方式开发组件，而是采用`vue-cli`创建，`vue`模板文件的方式开发，以下方法只是为了让大家理解什么是组件。
  **使用`Vue.component()`方法注册组件，格式如下：**

```html
<div id="app">
  <pan></pan>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script type="text/javascript">
    //先注册组件
    Vue.component("pan",{
        
        template:'<li>Hello</li>'

    });
    //再实例化Vue
    var vm = new Vue({
        el:"#app",
    });
</script>
```

说明：

- `Vue.component()`：注册组件
- `pan`：自定义组件的名字
- `template`：组件的模板

#### **（2）使用`props`属性传递参数**

像上面那样用组件没有任何意义，所以我们是需要传递参数到组件的，此时就需要使用`props`属性了！
  **注意：默认规则下props属性里的值不能为大写；**

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>

        <div id="app">
            <!--组件：传递给组件中的值：props-->
            <pan v-for="item in items" v-bind:panh="item"></pan>
        </div>

        <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
        <script type="text/javascript">
            //定义组件
            Vue.component("pan",{
                props:['panh'],
                template:'<li>{{panh}}</li>'

            });
            var vm = new Vue({
                el:"#app",
                data:{
                    items:["java","Linux","前端"]
                }
            });
        </script>
    </body>
</html>

```

说明：

v-for="item in items"：遍历Vue实例中定义的名为items的数组，并创建同等数量的组件
v-bind:panh="item"：将遍历的item项绑定到组件中props定义名为item属性上；= 号左边的panh为props定义的属性名，右边的为item in items 中遍历的item项的值

## 4、Axios异步通信

### 4.1、什么是Axios

Axios是一个开源的可以用在浏览器端和Node JS的异步通信框架， 她的主要作用就是实现AJAX异步通信，其功能特点如下：

- 从浏览器中创建XMLHttpRequests
- 从node.js创建http请求
- 支持Promise API[JS中链式编程]
- 拦截请求和响应
- 转换请求数据和响应数据
- 取消请求
- 自动转换JSON数据
- 客户端支持防御XSRF(跨站请求伪造)
- GitHub：https://github.com/axios/axios
- 中文文档：http://www.axios-js.com/

### 4.2、为什么要使用Axios

由于Vue.js是一个视图层框架并且作者(尤雨溪) 严格准守SoC(关注度分离原则)所以Vue.js并不包含AJAX的通信功能， 为了解决通信问题， 作者单独开发了一个名为vue-resource的插件， 不过在进入2.0版本以后停止了对该插件的维护并推荐了Axios框架。少用jQuery， 因为它操作Dom太频繁!

### 4.3、第一个Axios应用程序

咱们开发的接口大部分都是采用JSON格式， 可以先在项目里模拟一段JSON数据， 数据内容如下：创建一个名为data.json的文件并填入上面的内容， 放在项目的根目录下

```json
{
    "name": "狂神说Java",
    "url": "https://blog.kuangstudy.com",
    "page": 1,
    "isNonProfit": true,
    "address": {
        "street": "含光门",
        "city": "陕西西安",
        "country": "中国"
    },
    "links": [
        {
            "name": "bilibili",
            "url": "https://space.bilibili.com/95256449"
        },
        {
            "name": "狂神说Java",
            "url": "https://blog.kuangstudy.com"
        },
        {
            "name": "百度",
            "url": "https://www.baidu.com/"
        }
    ]
}

```

**测试代码**

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Axios</title>
        <!--v-cloak 解决闪烁问题-->
        <style>
            [v-cloak]{
                display: none;
            }
        </style>
    </head>
    <body>
        <div id="vue">
            <div>地名：{{info.name}}</div>
            <div>地址：{{info.address.country}}--{{info.address.city}}--{{info.address.street}}</div>
            <div>链接：<a v-binf:href="info.url" target="_blank">{{info.url}}</a></div>
        </div>
    </body>
    <script src="./js/vue.js"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script>
        let vm = new Vue({
            el: "#vue",
            //注意 这里的data是一个方法  属性:vm
            data(){
                return{
                    //请求的返回参数格式，必须和json字符串一样
                    info:{
                        name:null,
                        address:{
                            country:null,
                            street:null,
                            city:null
                        }
                    }
                }
            },
            mounted(){ //钩子函数 链式编程 ES6新特性
                axios
                    .get('data.json')
                    .then(response => (this.info = response.data));
            }  
        });
    </script>
</html>
```

说明：

1. 在这里使用了v-bind将a:href的属性值与Vue实例中的数据进行绑定
2. 使用axios框架的get方法请求AJAX并自动将数据封装进了Vue实例的数据对象中
3. 我们在data中的数据结构必须和`Ajax`响应回来的数据格式匹配！

### 4.4、Vue的生命周期

官方文档：https://cn.vuejs.org/v2/guide/instance.html#生命周期图示

Vue实例有一个完整的生命周期，也就是从开始创建初女台化数据、编译模板、挂载DOM、渲染一更新一渲染、卸载等一系列过程，我们称这是Vue的生命周

期。通俗说就是Vue实例从创建到销毁的过程，就是生命周期。

在Vue的整个生命周期中，它提供了一系列的事件，可以让我们在事件触发时注册JS方法，可以让我们用自己注册的JS方法控制整个大局，在这些事件响应方

法中的this直接指向的是Vue的实例。
![20-1](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210921001119.png)

## 5、计算属性、内容分发、自定义事件

### 5.1、什么是计算属性

计算属性的重点突出在`属性`两个字上(属性是名词)，首先它是个`属性`其次这个属性有`计算`的能力(计算是动词)，这里的`计算`就是个函数：简单点说，它就是一个能够将计算结果缓存起来的属性(将行为转化成了静态的属性)，仅此而已；可以想象为缓存!

**上代码**

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>计算属性</title>
    </head>
    <body>
        <div id="app">
            <!-- 方法 -->
            <p>{{currentTime1()}}</p>
            <!-- 计算属性 可以看成是一个缓存 计算属性不用加“()” -->
            <p>{{currentTime2}}</p>
        </div>

    </body>
    <script src="./js/vue.js"></script>
    <script>
        let vm = new Vue({
            el: "#app",
            data: {
                msg: "demo"
            },
            methods: {
                currentTime1: function(){
                    //返回当前时间
                    return Date.now().toLocaleString();
                }
            },
            //计算属性 
            computed: {//计算属性：methods，computed方法名不能重名，重名之后，只会调用methods的方法
                currentTime2: function(){
                    this.msg;
                    return Date.now().toLocaleString();
                }
            }
        });
    </script>
</html>

```

注意：methods和computed里的东西不能重名
说明：

- methods：定义方法， 调用方法使用currentTime1()， 需要带括号


- computed：定义计算属性， 调用属性使用currentTime2， 不需要带括号：this.message是为了能够让currentTime2观察到数据变化而变化


- 如何在方法中的值发生了变化，则缓存就会刷新!可以在控制台使用vm.message=”q in jiang"， 改变下数据的值，再次测试观察效果!


**结论：**
  调用方法时，每次都需要讲行计算，既然有计算过程则必定产生系统开销，那如果这个结果是不经常变化的呢?此时就可以考虑将这个结果缓存起来，采用计算属性可以很方便的做到这点，**计算属性的主要特性就是为了将不经常变化的计算结果进行缓存，以节约我们的系统开销；**

### 5.2、内容分发

在==Vue.js==中我们使用**<slot>**元素作为承载分发内容的出口，作者称其为插槽，可以应用在组合组件的场景中；

**测试**
比如准备制作一个待办事项组件(todo) ， 该组件由待办标题(todo-title) 和待办内容(todo-items)组成，但这三个组件又是相互独立的，该如何操作呢?

**第一步定义一个待办事项的组件**

```html
<div id="app">
    <todo></todo>
</div>
<!--1.导入Vue.js-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script type="text/javascript">
    Vue.component('todo',{
        template:'<div>\
                <div>代办事项</div>\
                <ul>\
                    <li>学习狂神说Java</li>\
                </ul>\
            </div>'
    })
</script>
```

**第二步 我们需要让，代办事项的标题和值实现动态绑定，怎么做呢？我们可以留一个插槽！**
  1-将上面的代码留出一个插槽，即slot

```javascript
 Vue.component('todo',{
        template:'<div>\
                <slot name="todo-title"></slot>\
                <ul>\
                    <slot name="todo-items"></slot>\
                </ul>\
            </div>'
    });

```

2-定义一个名为todo-title的待办标题组件 和 todo-items的待办内容组件

```javascript
Vue.component('todo-title',{
        props:['title'],
        template:'<div>{{title}}</div>'
    });
   
12345
//这里的index，就是数组的下标，使用for循环遍历的时候，可以循环出来！
    Vue.component("todo-items",{
        props:["item","index"],
        template:"<li>{{index+1}},{{item}}</li>"
    });

```

3-实例化Vue并初始化数据

```javascript
 var vm = new Vue({
        el:"#vue",
        data:{
            todoItems:['test1','test2','test3']
        }
    });

```

4-将这些值，通过插槽插入

```html
<div id="vue">
    <todo>
        <todo-title slot="todo-title" title="秦老师系列课程"></todo-title>
        <!--<todo-items slot="todo-items" v-for="{item,index} in todoItems" v-bind:item="item"></todo-items>-->
        <!--如下为简写-->
        <todo-items slot="todo-items" v-for="item in todoItems" :item="item"></todo-items
    </todo>
</div>

```

说明：我们的todo-title和todo-items组件分别被分发到了todo组件的todo-title和todo-items插槽中
  完整代码如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!--view层，模板-->
<div id="vue">
    <todo>
        <todo-title slot="todo-title" :title="title"></todo-title>
        <!--<todo-items slot="todo-items" v-for="{item,index} in todoItems" v-bind:item="item"></todo-items>-->
        <!--如下为简写-->
        <todo-items slot="todo-items" v-for="item in todoItems" :item="item"></todo-items
    </todo>
</div>
<!--1.导入Vue.js-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script type="text/javascript">
    Vue.component('todo',{
        template:'<div>\
                <slot name="todo-title"></slot>\
                <ul>\
                    <slot name="todo-items"></slot>\
                </ul>\
            </div>'
    });
    Vue.component('todo-title',{
        props:['title'],
        template:'<div>{{title}}</div>'
    });
    //这里的index，就是数组的下标，使用for循环遍历的时候，可以循环出来！
    Vue.component("todo-items",{
        props:["item","index"],
        template:"<li>{{index+1}},{{item}}</li>"
    });

    var vm = new Vue({
        el:"#vue",
        data:{
            title:"秦老师系列课程",
            todoItems:['test1','test2','test3']
        }
    });
</script>
</body>
</html>

```

### 5.3、自定义事件

通以上代码不难发现，数据项在Vue的实例中， 但删除操作要在组件中完成， 那么组件如何才能删除Vue实例中的数据呢?此时就涉及到参数传递与事件分发了， Vue为我们提供了自定义事件的功能很好的帮助我们解决了这个问题； 使用this.$emit(‘自定义事件名’， 参数) ， 操作过程如下：
  

1-在vue的实例中增加了methods对象并定义了一个名为removeTodoltems的方法

```javascript
var vm = new Vue({
        el:"#vue",
        data:{
            title_text:"秦老师系列课程",
            todoItems:['test1','test2','test3']
        },
        methods:{
            removeItems:function(index){
                console.log("删除了"+this.todoItems[index]+"OK");
                //splice（） 方法向/从数组中添加/删除项目，然后返回被删除的项目，其中index
                this.todoItems.splice(index,1);
            }
        }
    });

```

2-修改todo-items待办内容组件的代码，增加一个删除按钮，并且绑定事件！

```javascript
 Vue.component("todo-items",{
        props:["item_p","index_p"],
        template:"<li>{{index_p+1}},{{item_p}} <button @click='remove'>删除</button></li>",
        methods:{
            remove:function (index) {
            //这里的remove是自定义事件名称，需要在HTML中使用v-on:remove的方式
                //this.$emit 自定义事件分发
                this.$emit('remove',index);
            }
        }
    });

```

3-修改todo-items待办内容组件的HTML代码，增加一个自定义事件，比如叫remove，可以和组件的方法绑定，然后绑定到vue的方法！

```html
<!--增加了v-on:remove="removeTodoItems(index)"自定义事件，该组件会调用Vue实例中定义的-->
<todo-items slot="todo-items" v-for="(item,index) in todoItems"
            :item_p="item" :index_p="index" v-on:remove="removeItems(index)" :key="index"></todo-items>

```

**对上一个代码进行修改，实现删除功能**

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
        <!--view层，模板-->
        <div id="vue">
            <todo>
                <todo-title slot="todo-title" :title="title_text"></todo-title>
                <!--<todo-items slot="todo-items" v-for="(item,index) in todoItems" v-bind:item="item"></todo-items>-->
                <!--如下为简写-->
                <todo-items slot="todo-items" v-for="(item,index) in todoItems"
                            :item_p="item" :index_p="index" v-on:remove="removeItems(index)" :key="index"></todo-items>
            </todo>
        </div>
        <!--1.导入Vue.js-->
        <script src="../js/vue.js"></script>
        <script type="text/javascript">
            Vue.component('todo',{
                template:'<div>\
<slot name="todo-title"></slot>\
<ul>\
<slot name="todo-items"></slot>\
            </ul>\
            </div>'
            });
            Vue.component('todo-title',{
                props:['title'],
                template:'<div>{{title}}</div>'
            });
            //这里的index，就是数组的下标，使用for循环遍历的时候，可以循环出来！
            Vue.component("todo-items",{
                props:["item_p","index_p"],
                template:"<li>{{index_p+1}},{{item_p}} <button @click='remove_methods'>删除</button></li>",
                methods:{
                    remove_methods:function (index) {
                        //this.$emit 自定义事件分发
                        this.$emit('remove',index);
                    }
                }
            });

            var vm = new Vue({
                el:"#vue",
                data:{
                    title_text:"秦老师系列课程",
                    todoItems:['test1','test2','test3']
                },
                methods:{
                    removeItems:function(index){
                        console.log("删除了"+this.todoItems[index]+"OK");
                        this.todoItems.splice(index,1);
                    }
                }
            });
        </script>
    </body>
</html>

```

> ==逻辑理解==

![21-1](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210921215144.png)

### 5.4、Vue入门小结

核心：数据驱动，组件化

优点：借鉴了AngularJS的模块化开发和React的虚拟Dom，虚拟Dom就是把Demo操作放到内存中执行；

​	**常用的属性：**

- v-if

- v-else-if

- v-else

- v-for

- v-on绑定事件，简写@

- v-model数据双向绑定

- v-bind给组件绑定参数，简写：

  **组件化：**

- 组合组件slot插槽
- 组件内部绑定事件需要使用到this.$emit("事件名",参数);
- 计算属性的特色，缓存计算数据
- 遵循SoC关注度分离原则，Vue是纯粹的视图框架，并不包含，比如Ajax之类的通信功能，为了解决通信
- 问题，我们需要使用Axios框架做异步通信；

**说明**
Vue的开发都是要基于NodeJS，实际开发采用Vue-cli脚手架开发，vue-router路由，vuex做状态管理；Vue UI，界面我们一般使用ElementUI（饿了么出品），或者ICE（阿里巴巴出品）来快速搭建前端项目~~

官网：

- https://element.eleme.cn/#/zh-CN
- https://ice.work/

## 6、第一个Vue-cli项目

### 6.1、什么是vue-cli

vue-cli是官方提供的一个脚手架，用于快速生成一个vue的项目模板；

预先定义好的目录结构及其基础代码，就好比咱们在创建Maven项目时就可以选择创建一个骨架项目，这个估计项目就是脚手架，我们的开发更加的快速；

**项目的功能**

- 统一的目录结构
- 本地调试
- 热部署
- 单元测试
- 集成打包上线

### 6.2、需要的环境

- Node.js:http://nodejs.cn/download/
  安装就是无脑的下一步就好，安装在自己的环境目录下
- Git：https://git-scm.com/doenloads
  镜像：https://npm.taobao.org/mirrors/git-for-windows/

**确认nodejs安装成功：**

- cmd下输入`node -v`，查看是否能够正确打印出版本号即可！
- cmd下输入`npm -v`，查看是否能够正确打印出版本号即可！
  这个npm，就是一个软件包管理工具，就和linux下的apt软件安装差不多！
    **安装Node.js淘宝镜像加速器（cnpm）**
    这样的话，下载会快很多~

```cmd
# -g 就是全局安装
npm install cnpm -g

# 或使用如下语句解决npm速度慢的问题
npm install --registry=https://registry.npm.taobao.org
```

安装的过程可能有点慢~，耐心等待！虽然安装了cnpm，但是尽量少用！
  安装的位置：`C:\Users\administrator\AppData\Roaming\npm`

![22-2](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210922222855.jpg)

**安装vue-cli**

```cmd
cnpm instal1 vue-cli-g
#测试是否安装成功#查看可以基于哪些模板创建vue应用程序，通常我们选择webpack
vue list
```

![22-3](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210922223357.jpg)

### 6.3、第一个vue-cli应用程序

1.创建一个Vue项目，我们随便建立一个空的文件夹在电脑上，我这里在D盘下新建一个目录

```cmd
D:\Project\vue-study;
```

2.创建一个基于webpack模板的vue应用程序

```cmd
#1、首先需要进入到对应的目录 cd D:\Project\vue-study
#2、这里的myvue是顶日名称，可以根据自己的需求起名
vue init webpack myvue
```

一路都选择no即可；
  **说明：**

- Project name：项目名称，默认回车即可
- Project description：项目描述，默认回车即可

- Author：项目作者，默认回车即可
- Install vue-router：是否安装vue-router，选择n不安装（后期需要再手动添加）

- Use ESLint to lint your code:是否使用ESLint做代码检查，选择n不安装（后期需要再手动添加)
- Set up unit tests:单元测试相关，选择n不安装（后期需要再手动添加）

- Setupe2etests with Nightwatch：单元测试相关，选择n不安装（后期需要再手动添加）
- Should we run npm install for you after the,project has been created:创建完成后直接初始化，选择n，我们手动执行；运行结果！
  

**(1）初始化并运行**

```cmd
cd myvue
npm install
npm run dev
```

执行完成后，目录多了很多依赖

当出现问题时，可以查看提示进行处理如下

![22-1](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210922223850.jpg)

## 7、Webpack使用

### 7.1、什么是webpack

本质上， webpack是一个现代JavaScript应用程序的静态模块打包器(module bundler) 。当webpack处理应用程序时， 它会递归地构建一个依赖关系图(dependency graph) ， 其中包含应用程序需要的每个模块， 然后将所有这些模块打包成一个或多个bundle.
  Webpack是当下最热门的前端资源模块化管理和打包工具， 它可以将许多松散耦合的模块按照依赖和规则打包成符合生产环境部署的前端资源。还可以将按需加载的模块进行代码分离，等到实际需要时再异步加载。通过loader转换， 任何形式的资源都可以当做模块， 比如Commons JS、AMD、ES 6、CSS、JSON、Coffee Script、LESS等；
  伴随着移动互联网的大潮， 当今越来越多的网站已经从网页模式进化到了WebApp模式。它们运行在现代浏览器里， 使用HTML 5、CSS 3、ES 6等新的技术来开发丰富的功能， 网页已经不仅仅是完成浏览器的基本需求； WebApp通常是一个SPA(单页面应用) ， 每一个视图通过异步的方式加载，这导致页面初始化和使用过程中会加载越来越多的JS代码，这给前端的开发流程和资源组织带来了巨大挑战。
  前端开发和其他开发工作的主要区别，首先是前端基于多语言、多层次的编码和组织工作，其次前端产品的交付是基于浏览器的，这些资源是通过增量加载的方式运行到浏览器端，如何在开发环境组织好这些碎片化的代码和资源，并且保证他们在浏览器端快速、优雅的加载和更新，就需要一个模块化系统，这个理想中的模块化系统是前端工程师多年来一直探索的难题。

### 7.2、模块化的演进

#### 1、**Script标签**

```javascript
<script src = "module1.js"></script>
<script src = "module2.js"></script>
<script src = "module3.js"></script>
```

这是最原始的JavaScript文件加载方式，如果把每一个文件看做是一个模块，那么他们的接口通常是暴露在全局作用域下，也就是定义在window对象中，不同模块的调用都是一个作用域。
  这种原始的加载方式暴露了一些显而易见的弊端：

- 全局作用域下容易造成变量冲突
- 文件只能按照`<script>`的书写顺序进行加载
- 开发人员必须主观解决模块和代码库的依赖关系
- 在大型项目中各种资源难以管理，长期积累的问题导致代码库混乱不堪

#### 2、**CommonsJS**

服务器端的NodeJS遵循CommonsJS规范，该规范核心思想是允许模块通过require方法来同步加载所需依赖的其它模块，然后通过exports或module.exports来导出需要暴露的接口。

```javascript
require("module");
require("../module.js");
export.doStuff = function(){};
module.exports = someValue;
1234
```

**优点：**

- 服务器端模块便于重用
- NPM中已经有超过45万个可以使用的模块包
- 简单易用

**缺点：**

- 同步的模块加载方式不适合在浏览器环境中，同步意味着阻塞加载，浏览器资源是异步加载的
- 不能非阻塞的并行加载多个模块

**实现：**

- 服务端的NodeJS
- •Browserify，浏览器端的CommonsJS实现，可以使用NPM的模块，但是编译打包后的文件体积较大
- modules-webmake，类似Browserify，但不如Browserify灵活
- wreq，Browserify的前身

**AMD**
Asynchronous Module Definition规范其实主要一个主要接口define(id?,dependencies?,factory);它要在声明模块的时候指定所有的依赖dependencies，并且还要当做形参传到factory中，对于依赖的模块提前执行。

### 7.3、安装webpack

WebPack是一款模块加载器兼打包工具， 它能把各种资源， 如JS、JSX、ES 6、SASS、LESS、图片等都作为模块来处理和使用。

**安装：**

```cmd
npm install webpack -g
npm install webpack-cli -g
```

**测试安装成功:**

- `webpack -v`
- `webpack-cli -v`

**配置**

创建 `webpack.config.js`配置文件

- entry：入口文件， 指定Web Pack用哪个文件作为项目的入口
- output：输出， 指定WebPack把处理完成的文件放置到指定路径

- module：模块， 用于处理各种类型的文件
- plugins：插件， 如：热更新、代码重用等

- resolve：设置路径指向
- watch：监听， 用于设置文件改动后直接打包

```javascript
module.exports = {
    entry:"",
    output:{
        path:"",
        filename:""
    },
    module:{
        loaders:[
            {test:/\.js$/,;\loade:""}
        ]
    },
    plugins:{},
    resolve:{},
    watch:true
}
```

直接运行`webpack`命令打包

### 7.4、使用webpack

1. 创建项目

2. 创建一个名为modules的目录，用于放置js模块等资源文件

3. 在modules下创建模块文件，如hello.js,用于编写js模块相关代码

   ```javascript
   //暴露一个方法：sayHi
   exports.sayHi = function(){
       document.write("<div> Hello Webpack </div>");
   };
   ```

4. 在modules下创建一个名为main.js的入口文件，用于打包时设置entry属性

   ```javascript
   // require 导入一个模块，就可以调用这个模块中的方法了
   var hello = require("./hello");
   hello.sayHi();
   ```

5. 在项目目录下创建webpack.config.js配置文件，使用webpack命令打包

   ```javascript
   module.exports = {
       entry: "./modules/main.js",
       output: {
           filename:"./js/bundle.js"
       },
       mode: 'development'
   };
   ```

6. 在项目目录下创建HTML页面，如index.html，导入webpack打包后的JS文件

   ```html
   <!DOCTYPE html>
   <html lang="en">
       <head>
           <meta charset="UTF-8">
           <meta http-equiv="X-UA-Compatible" content="IE=edge">
           <meta name="viewport" content="width=device-width, initial-scale=1.0">
           <title>可爱发说编程</title>
       </head>
       <body>
   
       </body>
       <script src="./dist/js/bundle.js"></script>
   </html>
   ```

7. 最后进入当前文件夹（以cmd形式）

   输入：

   ```cmd
   webpack
   ```

   **说明**

   ```cmd
   # 参数--watch 用于监听变化
   webpack --watch
   ```

## 8、Vue-router 路由

### 8.1、说明

学习的时候尽量打开官方的文档

Vue Router是Vue.js官方的路由管理器。它和Vue.js的核心深度集成， 让构建单页面应用变得易如反掌。包含的功能有：

- 嵌套的路由/视图表
- 模块化的、基于组件的路由配置
- 路由参数、查询、通配符
- 基于Vue js过渡系统的视图过渡效果
- 细粒度的导航控制
- 带有自动激活的CSS class的链接
- HTML5 历史模式或hash模式， 在IE 9中自动降级
- 自定义的滚动行为

### 8.2、安装

**基于第一个`vue-cli`进行测试学习； 先查看node modules中是否存在vue-router**
  vue-router是一个插件包， 所以我们还是需要用n pm/cn pm来进行安装的。打开命令行工具，进入你的项目目录，输入下面命令。

```cmd
npm install vue-router --save-dev
```

如果提示需要修复，就按照如图操作即可

![23-1](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210923194853.png)

如果在一个模块化工程中使用它，必须要通过Vue.use()明确地安装路由功能：

```javascript
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter);
```

### 8.3、测试

1、先删除没有用的东西

2、`components` 目录下存放我们自己编写的组件

3、定义一个`Content.vue` 的组件

```vue
<template>
    <div>
        <h1>内容页面</h1>
    </div>
</template>

<script>
    export default {
        name:'Content'
    }
</script>
```

定义==Main.vue==组件（和上一个类似，只是重复，增加熟悉度）

```vue
<template>
    <div>
        <h1>首页</h1>
    </div>
</template>

<script>
    export default {
        name: 'Main'
    }
</script>
```

4、安装路由，在src目录下，新建一个文件夹：`router`，专门存放路由，配置路由index.js，如下

```javascript
// 导入 Vue
import Vue from "vue";
// 导入 Router  这里配置了（main.js里就不用配置了）
import VueRouter from "vue-router";

//  导入 Content.vue
import Content from '../components/Content.vue'
//  导入 Main.vue
import Main from '../components/Main.vue'
// 导入 Music.vue
import Music from '../components/Music.vue'

/* 这里和java的导包类似，先导入，后引用 */

// 安装路由
Vue.use(VueRouter);

// 导出配置路由，供其他文件使用
export default new VueRouter({
    // 类似后端的 RequestMapping
    routes:[
        {
            // 路由路径
            path:'/content',
            // 路由名字：
            name: 'content',
            // 跳转的组件
            component:Content
        },
        {
            // 同上
            path: '/main',
            name: 'main',
            component: Main
        },{
            // 同上
            path: '/music',
            name: 'music',
            component: Music
        }
    ]

});
```

5、在`main.js`中配置路由

```javascript
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import App from './App'

// router组件可以在route文件夹下的index.js里配置， main.js要尽量简洁
/* import VueRouter from 'vue-router' */
// 导入路由配置
import router from './router'  //会自动寻找index.js(有点小智能了)

/* // 显示声明使用VueRouter
Vue.use(VueRouter);
Vue.config.productionTip = false */

/* eslint-disable no-new */
new Vue({
    el: '#app',
    // 配置路由
    router,
    components: { App },
    template: '<App/>'
})

```

6、在`App.vue`中使用路由

```vue
<template>
<div id="app">
    <!--   <img src="./assets/logo.png">
<HelloWorld/> -->
    <h1>可爱发</h1>
    <!-- 跳转链接 -->
    <router-link to="/main">跳转到首页</router-link>
    <router-link to="/content">跳转到内容页</router-link>
    <router-link to="/music">跳转到音乐页面</router-link>
    <!-- 展示视图,显示上面的视图模块的 -->
    <router-view></router-view>
    </div>
</template>

<script>
    // import HelloWorld from './components/HelloWorld'

    export default {
        name: 'App',
        /* components: {
    HelloWorld
  } */
    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>

```

> 最后输入 ==npm run dev== 运行，访问8080进行测试

![image-20210923203921267](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210923203921.png)

## 9、实战快速上手

### 9.1、创建工程

注意：命令行都要使用管理员模式运行
1、创建一个名为hello-vue的工程`vue init webpack hello-vue`
2、安装依赖， 我们需要安装vue-router、element-ui、sass-loader和node-sass四个插件

```cmd
#进入工程目录
cd hello-vue
#安装vue-routern 
npm install vue-router --save-dev
#安装element-ui
npm i element-ui -S
#安装依赖
npm install
# 安装SASS加载器
cnpm install sass-loader node-sass --save-dev
#启功测试
npm run dev
```

3、Npm命令解释：

- npm install moduleName：安装模块到项目目录下
- npm install -g moduleName：-g的意思是将模块安装到全局，具体安装到磁盘哪个位置要看npm config prefix的位置
- npm install -save moduleName：–save的意思是将模块安装到项目目录下， 并在package文件的dependencies节点写入依赖，-S为该命令的缩写
- npm install -save-dev moduleName:–save-dev的意思是将模块安装到项目目录下，并在package文件的devDependencies节点写入依赖，-D为该命令的缩写

### 9.2、创建登录页面

把没有用的初始化东西删掉！
  在源码目录中创建如下结构：

- assets：用于存放资源文件
- components：用于存放Vue功能组件
- views：用于存放Vue视图组件
- router：用于存放vue-router配置

![image-20210926004224431](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210926004226.png)

**创建首页视图，在views目录下创建一个名为Main.vue的视图组件：**

```vue
<template>
	<div>首页</div>
</template>
<script>
	export default {
			name:"Main"
	}
</script>
<style scoped>
</style>

```

创建登录页视图在views目录下创建名为Login.vue的视图组件，其中el-*的元素为ElementUI组件；

```vue
<template>
  <div>
    <el-form ref="loginForm" :model="form" :rules="rules" label-width="80px" class="login-box">
      <h3 class="login-title">欢迎登录</h3>
      <el-form-item label="账号" prop="username">
        <el-input type="text" placeholder="请输入账号" v-model="form.username"/>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input type="password" placeholder="请输入密码" v-model="form.password"/>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" v-on:click="onSubmit('loginForm')">登录</el-button>
      </el-form-item>
    </el-form>

    <el-dialog title="温馨提示" :visible.sync="dialogVisiable" width="30%" :before-close="handleClose">
      <span>请输入账号和密码</span>
      <span slot="footer" class="dialog-footer">
          <el-button type="primary" @click="dialogVisible = false">确定</el-button>
        </span>
    </el-dialog>
  </div>
</template>

<script>
    export default {
        name: "Login",
      data(){
          return{
            form:{
              username:'',
              password:''
            },
            //表单验证，需要在 el-form-item 元素中增加prop属性
            rules:{
              username:[
                {required:true,message:"账号不可为空",trigger:"blur"}
              ],
              password:[
                {required:true,message:"密码不可为空",tigger:"blur"}
              ]
            },

            //对话框显示和隐藏
            dialogVisible:false
          }
      },
      methods:{
          onSubmit(formName){
            //为表单绑定验证功能
            this.$refs[formName].validate((valid)=>{
              if(valid){
                //使用vue-router路由到指定界面，该方式称为编程式导航
                this.$router.push('/main');
              }else{
                this.dialogVisible=true;
                return false;
              }
            });
          }
      }
    }
</script>

<style lang="scss" scoped>
  .login-box{
    border:1px solid #DCDFE6;
    width: 350px;
    margin:180px auto;
    padding: 35px 35px 15px 35px;
    border-radius: 5px;
    -webkit-border-radius: 5px;
    -moz-border-radius: 5px;
    box-shadow: 0 0 25px #909399;
  }
  .login-title{
    text-align:center;
    margin: 0 auto 40px auto;
    color: #303133;
  }
</style>

```

创建路由，在router目录下创建一个名为`index.js`的vue-router路由配置文件

```javascript
//导入vue
import Vue from 'vue';
import VueRouter from 'vue-router';
//导入组件
import Main from "../views/Main";
import Login from "../views/Login";
//使用
Vue.use(VueRouter);
//导出
export default new VueRouter({
  routes: [
    {
      //登录页
      path: '/main',
      component: Main
    },
    //首页
    {
      path: '/login',
      component: Login
    },
  ]

})

```

APP.vue

```vue
<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>


export default {
  name: 'App',

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

```

main.js

```javascript
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import App from './App'
import router from "./router"

import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'

Vue.use(router)
Vue.use(ElementUI)

/* eslint-disable no-new */
new Vue({
    el: '#app',
    router,
    render:h=>h(App)
})

```

测试：在浏览器打开 http://localhost:8080/#/login
如果出现错误: 可能是因为sass-loader的版本过高导致的编译错误，当前最高版本是8.0.2，需要退回到7.3.1 ；
去package.json文件里面的 "sass-loader"的版本更换成7.3.1，然后重新cnpm install就可以了；

### 9.3、路由嵌套

嵌套路由又称子路由，在实际应用中，通常由多层嵌套的组件组合而成。
demo

1、 创建用户信息组件，在 views/user 目录下创建一个名为 Profile.vue 的视图组件；
Profile.vue

```vue
<template>
  <h1>个人信息</h1>
</template>
<script>
  export default {
    name: "UserProfile"
  }
</script>
<style scoped>
</style>

```

2、在用户列表组件在 views/user 目录下创建一个名为 List.vue 的视图组件；
List.vue

```vue
<template>
  <h1>用户列表</h1>
</template>
<script>
  export default {
    name: "UserList"
  }
</script>
<style scoped>
</style>
```

3、 修改首页视图，我们修改 Main.vue 视图组件，此处使用了 ElementUI 布局容器组件，代码如下：
Main.vue

```vue
<template>
    <div>
      <el-container>
        <el-aside width="200px">
          <el-menu :default-openeds="['1']">
            <el-submenu index="1">
              <template slot="title"><i class="el-icon-caret-right"></i>用户管理</template>
              <el-menu-item-group>
                <el-menu-item index="1-1">
                <!--插入的地方-->
                  <router-link to="/user/profile">个人信息</router-link>
                </el-menu-item>
                <el-menu-item index="1-2">
                <!--插入的地方-->
                  <router-link to="/user/list">用户列表</router-link>
                </el-menu-item>
              </el-menu-item-group>
            </el-submenu>
            <el-submenu index="2">
              <template slot="title"><i class="el-icon-caret-right"></i>内容管理</template>
              <el-menu-item-group>
                <el-menu-item index="2-1">分类管理</el-menu-item>
                <el-menu-item index="2-2">内容列表</el-menu-item>
              </el-menu-item-group>
            </el-submenu>
          </el-menu>
        </el-aside>

        <el-container>
          <el-header style="text-align: right; font-size: 12px">
            <el-dropdown>
              <i class="el-icon-setting" style="margin-right: 15px"></i>
              <el-dropdown-menu slot="dropdown">
                <el-dropdown-item>个人信息</el-dropdown-item>
                <el-dropdown-item>退出登录</el-dropdown-item>
              </el-dropdown-menu>
            </el-dropdown>
          </el-header>
          <el-main>
          <!--在这里展示视图-->
            <router-view />
          </el-main>
        </el-container>
      </el-container>
    </div>
</template>
<script>
    export default {
        name: "Main"
    }
</script>
<style scoped lang="scss">
  .el-header {
    background-color: #B3C0D1;
    color: #333;
    line-height: 60px;
  }
  .el-aside {
    color: #333;
  }
</style>

```

4、 配置嵌套路由修改 router 目录下的 index.js 路由配置文件，使用children放入main中写入子模块，代码如下
index.js

```javascript
//导入vue
import Vue from 'vue';
import VueRouter from 'vue-router';
//导入组件
import Main from "../views/Main";
import Login from "../views/Login";
//导入子模块
import UserList from "../views/user/List";
import UserProfile from "../views/user/Profile";

//使用
Vue.use(VueRouter);
//导出
export default new VueRouter({
  routes: [
    {
      //登录页
      path: '/main',
      component: Main,
      //  写入子模块
      children: [
        {
          path: '/user/profile',
          component: UserProfile,
        }, {
          path: '/user/list',
          component: UserList,
        },
      ]
    },
    //首页
    {
      path: '/login',
      component: Login

    },
  ]
})
```

### 9.4、参数传递

这里演示如果请求带有参数该怎么传递
demo
 用的还是上述例子的代码 修改一些代码 这里不放重复的代码了
第一种取值方式

1、 修改路由配置, 主要是router下的index.js中的 path 属性中增加了 :id 这样的占位符

```javascript
{
	path: '/user/profile/:id', 
	name:'UserProfile', 
	component: UserProfile
}

```

2、传递参数
 此时我们在Main.vue中的route-link位置处 to 改为了 :to，是为了将这一属性当成对象使用，注意 router-link 中的 name 属性名称 一定要和 路由中的 name 属性名称 匹配，因为这样 Vue 才能找到对应的路由路径；

```vue
<!--name是组件的名字 params是传的参数 如果要传参数的话就需要用v:bind:来绑定-->
<router-link :to="{name:'UserProfile',params:{id:1}}">个人信息</router-link>
```

3、在要展示的组件Profile.vue中接收参数 使用 {{$route.params.id}}来接收
Profile.vue 部分代码

```vue
<template>
  <!--  所有的元素必须在根节点下-->
  <div>
    <h1>个人信息</h1>
    {{$route.params.id}}
  </div>
</template>

```

第二种取值方式 使用props 减少耦合

1、修改路由配置 , 主要在router下的index.js中的路由属性中增加了 props: true 属性

```javascript
{
	path: '/user/profile/:id', 
	name:'UserProfile', 
	component: UserProfile, 
	props: true
}

```

2、传递参数和之前一样 在Main.vue中修改route-link地址

```vue
<!--name是组件的名字 params是传的参数 如果要传参数的话就需要用v:bind:来绑定-->
<router-link :to="{name:'UserProfile',params:{id:1}}">个人信息</router-link>

```

3、在Profile.vue接收参数为目标组件增加 props 属性
Profile.vue

```vue
<template>
  <div>
    个人信息
    {{ id }}
  </div>
</template>
<script>
    export default {
      props: ['id'],
      name: "UserProfile"
    }
</script>
<style scoped>
</style>

```

### 9.5、组件重定向

重定向的意思大家都明白，但 Vue 中的重定向是作用在路径不同但组件相同的情况下，比如：
在router下面index.js的配置

```javascript
{
  path: '/main',
  name: 'Main',
  component: Main
},
{
  path: '/goHome',
  redirect: '/main'
}

```

说明：这里定义了两个路径，一个是 /main ，一个是 /goHome，其中 /goHome 重定向到了 /main 路径，由此可以看出重定向不需要定义组件；

使用的话，只需要在Main.vue设置对应路径即可；

```vue
<el-menu-item index="1-3">
    <router-link to="/goHome">回到首页</router-link>
</el-menu-item>

```

### 9.6、路由模式

路由模式有两种

- hash：路径带 # 符号，如 http://localhost/#/login
- history：路径不带 # 符号，如 http://localhost/login

修改路由配置，代码如下：

```javascript
export default new Router({
    mode: 'history',
    routes: [
    ]
});

```

**路由钩子与异步请求**

beforeRouteEnter：在进入路由前执行
beforeRouteLeave：在离开路由前执行

在Profile.vue中写

```javascript
  export default {
    name: "UserProfile",
    beforeRouteEnter: (to, from, next) => {
      console.log("准备进入个人信息页");
      next();
    },
    beforeRouteLeave: (to, from, next) => {
      console.log("准备离开个人信息页");
      next();
    }
  }

```

参数说明：
to：路由将要跳转的路径信息
from：路径跳转前的路径信息
next：路由的控制参数
next() 跳入下一个页面
next(’/path’) 改变路由的跳转方向，使其跳到另一个路由
next(false) 返回原来的页面
next((vm)=>{}) 仅在 beforeRouteEnter 中可用，vm 是组件实例

**在钩子函数中使用异步请求**

1、安装 Axios

```cmd
cnpm install --save vue-axios
```

2、main.js引用 Axios

```javascript
import axios from 'axios'
import VueAxios from 'vue-axios'
Vue.use(VueAxios, axios)
```

3、准备数据 ： 只有我们的 static 目录下的文件是可以被访问到的，所以我们就把静态文件放入该目录下。

数据和之前用的json数据一样 需要的去上述axios例子里

```txt
// 静态数据存放的位置
static/mock/data.json
```

4.在 beforeRouteEnter 中进行异步请求

Profile.vue

```javascript
  export default {
    //第二种取值方式
    // props:['id'],
    name: "UserProfile",
    //钩子函数 过滤器
    beforeRouteEnter: (to, from, next) => {
      //加载数据
      console.log("进入路由之前")
      next(vm => {
        //进入路由之前执行getData方法
        vm.getData()
      });
    },
    beforeRouteLeave: (to, from, next) => {
      console.log("离开路由之前")
      next();
    },
    //axios
    methods: {
      getData: function () {
        this.axios({
          method: 'get',
          url: 'http://localhost:8080/static/mock/data.json'
        }).then(function (response) {
          console.log(response)
        })
      }
    }
  }

```

5.路由钩子和axios结合图

![image-20210926005914331](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210926005914.png)



