# Ajax和Json学习

## Ajax

**Ajax = Asynchronous JavaScript And XML（异步的JavaScript 和 XML）**

**异步无刷新技术**

### 1.$.ajax

​	**jquery调用ajax方法：**

​				格式： $.ajax({});

​					参数：

​							type:请求方式GET/POST

​							url:请求地址

​							async：是否同步，默认是true表示异步

​							data：发送到服务器的数据

​							dataType：预期服务器返回的数据类型

​							contentType：设置请求头

​							successs：请求成功时调用此函数

​							error：请求失败时调用此函数

**get请求**

```javascript
$.ajax({
    type: "get",
    url: "data/data.txt",
    async: true,
    data: {

    },
    dataType: "json", //返回预期数据类型，如果是json格式，在接受到返回值时会自动封装成json对象
    success: function(data) {
        console.log(data);
        //将字符串转换成json对象(如果本身是json对象的话，就不要转了，会报错)
        /*var Object = JSON.parse(data);
console.log(Object);*/
        //先把ul 转化成 jQuery对象 然后才可以使用append方法
        var ul = $("<ul></ul>");
        //遍历元素
        for(i = 0; i < data.length; i++) {
            var user = data[i];
            //创建li元素
            var li = "<li>" + user.userName + "</li>";
            //将li元素设置到ul元素中
            ul.append(li);
            //将ul设置到body标签中
            $('body').append(ul);
        }
    }
});
```

### 2. $.get  和 $.post

这是一个简单的GET请求功能以取代复杂的 $.ajax.

请求成功时可调用函数，如果需要在出错时执行函数，请使用 $.ajax.

```javascript
//1.请求json文件，忽略返回值
$.get('js/data.json');
```

```javascript
//2.请求json文件，传递参数，忽略返回值
$.get('js/data.json',{name:'tom',age:20});
```

```javascript
//3.请求json文件，拿到返回值(这个最常用)
$.get('js/data.json',function(data){
    console.log(data);
});
```

```javascript
//3.请求json文件,传递参数，拿到返回值
$.get('js/data.json',{name:'tom',age:20},function(data){
    console.log(data);
});
```

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>$.get()</title>
    </head>
    <!--
        $.get();
        语法：
        $.get("请求地址","请求参数",function(形参){

        });
        $.post();    这种是需要有服务器才可以使用
        语法：
        $.post("请求地址","请求参数",function(形参){

        });
 
	-->
    <body>
    </body>
    <script src="../lib/jQuery.js"></script>
    <script type="text/javascript">
        $.get('data/data.txt',{},function(data){
            console.log(data);
        });
    </script>
</html>
```



### 3. $.getJSON

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>$.getJSON</title>
    </head>
    <!--
        $.getJSON
        语法:
        $.getJSON('请求地址'，"请求参数",function(形参){

        });
        注：getJSON方式要求返回的数据格式满足json格式（json字符串  文件名字可以不是json 但内容一定要是json格式）
-->
    <body>
    </body>
    <script src="../lib/jQuery.js"></script>
    <script type="text/javascript">
        //虽然 data.txt 和 test.txt 都是txt文件   但是data.txt的内容是json格式，所以可以获取并显示
        $.getJSON('data/test.txt',{},function(data){
            console.log(data);
        });
    </script>
</html>
```



​				

​							



