# CSS 3.0学习

##  1.CSS的表现

- 美化网页，字体，颜色，边距，高度，宽度，背景图片等等

## 2.CSS优势

- 内容和表现分离
- 网页结构表现统一
- 样式十分的丰富
- 建议使用独立于html的css文件
- 利用SEO，容易被搜索引擎收录

##  3.CSS的导入方式

1. 行内样式：![1616468910092](C:\Users\64811\AppData\Roaming\Typora\typora-user-images\1616468910092.png)
2. 内部样式：![1616468945398](C:\Users\64811\AppData\Roaming\Typora\typora-user-images\1616468945398.png)
3. 外部链接样式：![1616469022810](C:\Users\64811\AppData\Roaming\Typora\typora-user-images\1616469022810.png)
4. 外部导入样式:![1616469177933](C:\Users\64811\AppData\Roaming\Typora\typora-user-images\1616469177933.png)

##  4.基本选择器

1. 标签选择器：![1616469329890](C:\Users\64811\AppData\Roaming\Typora\typora-user-images\1616469329890.png)

2. 类选择器：![1616478454905](C:\Users\64811\AppData\Roaming\Typora\typora-user-images\1616478454905.png)

3. id选择器:

   ![1616478545404](C:\Users\64811\AppData\Roaming\Typora\typora-user-images\1616478545404.png)

## 5.高级选择器

### 1.层次选择器

1. 后代选择器：在某个元素的后面的所有元素  你爷爷，你爸爸，你       元素名  元素名{}

   ```css
   /*用到的body 和 p 只是举个例子，并不唯一*/
   body p{
       color :red;
   }
   ```

2. 子选择器：一代    元素名   >   元素名{}

   ```css
   body > p{
       color:red;
   }
   ```

3. 相邻兄弟选择器：只有一个，相邻且向下的同类元素       .类名 + 元素名{ }

   ```css
   .Class + p{
       color:red;
   }
   ```

   

4. 通用选择器:选择下面所有的同类元素    .类名 ~ 元素名{ }

   ```css
   .Class ~ p{
       color:red;
   }
   ```

### 2.结构伪类选择器

![1616746001246](C:\Users\64811\AppData\Roaming\Typora\typora-user-images\1616746001246.png)

### 3.属性选择器( 重点 id和类的结合)

1. 选中含有ID的元素

   ```css
   a[id]{
   	background: deeppink;
   }
   ```

2. 选中 含有一部分的元素

   ```css
   a[href *= "http"]{
   	background: yellow;
   }
   ```

3. 选中 id 等于某个具体值的元素

   ```css
   a[id = "first"]{
   	background: yellow;
   }
   ```

4. 选中以某些字符开头的元素

   ```css
   a[href ^= "img"]{
   	background: deeppink;
   }
   ```

5. 选中以某些字符结尾的元素

   ```css
   a[href $= "img"]{
   	background: deeppink;
   }
   ```

   

## 6.美化网页

### 1.字体设置

```css
/*font-family设置字体
font-weight设置粗细
font-size设置大小
color设置颜色*/
			
body p{
    font-family: "仿宋";
    color: red;
    font-weight: lighter;
    font-size: 50px;

}
```

### 2.文本样式

1. RGB颜色：Red Green Blue(0 ~ 256)

   ```css
   .H1{
   	color: rgb(256,256,256);
   }
   ```

2. RGBA :多了一个可以设置透明度的参数A（0~1）

   ```css
   .H1{
       color:rgba(0,256,256,1);
   }
   ```

3. 首行缩进：text-indent

   ```css
   .p1{
       /*首行缩进  
       1 em = 一个字*/
       text-indent: 2em;
   
   }
   ```

4. 块的高度：line-height 行高 上下居中用它（height = line-height）

   ```css
   .p1{
       /* 块的高度 */
       height: 50px;
       /*行高*/
       line-height: 50px; 
   }   
   ```

5. 修饰用的： text-decoration(了解)

   ```css
   text-decoration:underline 下划线
   text-decoration:line-through 中划线
   text-decoration:overline 上划线
   text-decoration:none 超链接去掉下划线
   ```
### 3.超链接伪类   

```css
/*去掉下划线*/
#baidu{
    text-decoration: none;
}

/*鼠标悬停时出现的效果（这个最常用）*/
a:hover{
    color:deeppink;
    /*可以变大*/
    font-size:75px;
}
/*鼠标按住未释放*/
a:active{
    color:purple;
    /*可以变大*/
    font-size:150px;
}
/*未访问时的状态*/
a:link{
    yellow:red;
}

/*已访问时的状态*/
a:visited{
    color:yellow;
}
```

### 4.列表样式

```css
/*id 选择器*/
#duv{
	/*设置宽度*/
	width:250px;
	/*设置背景*/
	/*background: url(../images/2.jpg);*/
	
	/*默认背景是灰色  便于连接*/
	background: gainsboro;
}

/*类选择器*/
.tittle{
	/*缩进两个字符*/
	text-indent: 2em;
	background: #0000FF;
	line-height: 80px;
}


/*使用一个后代选择器*/
ul li{
	/*背景来个灰色*/
	background: gainsboro;
	/*把小圆点去掉*/
	list-style: none;
	
}

```



### 5.背景

```css
div{
    width: 1000px;
    height:700px;
    border:1px solid red;

    /*默认图片是 水平 和 垂直 均平铺的*/
    background-image:url(images/WeChat.png) ;
}
/*水平平铺*/
.div1{
    background-repeat: repeat-x;
}
/*垂直平铺*/
.div2{
    background-repeat: repeat-y;
}
/*不平铺（就一张）*/
.div3{
    background-repeat: no-repeat;
}
```
## 7.盒子模型 (重点)



###  1.边框

- margin：外边距       padding：内边距       border：边框

- border：粗细(px)  样式( solid[实线] dashed[虚线] )  颜色 

  ```css
  input[name = "username"]{
  	border:2px solid #0000FF;
  }
  ```

- body,a,h1,ul,li等标签都会有默认的边距  可以自己默认设置下

  ```css
  /*让 body 下的外边框 内边框 修饰 等于0  常规操作*/
  h1,ul,a,li,body{
      margin: 0px;
      padding: 0;
      text-decoration: none;
  }
  ```

### 2. 圆角边框

border-radius

```css
/*圆形*/
.div1{
    width:100px;
    height: 100px;
    border:5px solid deeppink;
    /*圆角边框  border-radius: 左上 右上 右下 左下  顺时针方向
    超过100px就不会再有反应了*/
    border-radius: 100px;
    /*居中*/
    margin: auto auto;
    /*padding: auto auto;*/

}
```



   ## 8.浮动

### 1.display（不能控制方向）

```css
div{
	/*div里面的元素都不会去显示*/
	/*display:none;*/
	/*行内元素*/
	/*display: inline;*/
	/*块元素*/
	/*display:block;*/
	/*是块元素，但是可以内联在一行  常用*/
	display: inline-block;
				
}
```

### 2.float

```css
.img1{
	/*可以控制方向 display不行   向左浮动*/
	float: left;
}
```

### 3.解决父级边框塌陷问题

1. 增加父类元素高度

2. 增加一个空的div，清除浮动

   ```css
   /*两侧不允许有浮动*/
   clear:both;
   ```

3. overflow（第二推荐）

   ```css
   div{
   	height: 300px;
   	border: 1px solid red;
   	/*解决方法一：overflow  
   	* hidden会将多余部分隐藏   
   	* scroll 滚动条*/
   	overflow: scroll;
   }
   ```

4. div：after（首推）

   ```css
   div:after{
       content: '';
       display: block;
       clear: both;
   }
   ```

## 9.定位

### 1.相对定位

相对于自己原来的位置 position：relative   top，left等

相对定位会保留原有的位置

```css
.div1{
	background-color: orangered;
	border: 1px solid #008099;
	/*相对定位*/
	position: relative;
	/*相对向上20px*/
	top: -20px;
}
```

### 2.绝对定位

- 绝对定位不会保留原有的位置  position：absolute


- 默认状态下是相对于浏览器进行定位的

  ```css
  .div1{
  	/*绝对位置  默认是相对于浏览器定位*/
  	position:absolute;
  	/*移动方向距离*/
  	right:20px;
  }
  ```

- 如果父级元素有相对定位，那就是相对于父级元素进行定位的

  ```css
  #father{
      position:relative;
  }
  .div1{
      position:absolute;
  }
  ```

### 3.固定定位

- 顾名思义就是固定不动的位置  position：fixed   

- 默认相对于浏览器的

- ```css
  /*固定定位*/
  div:nth-of-type(2){
      width:50px;
      height: 50px;
      background: deeppink;
      position: fixed;
      right: 0;
      bottom: 0;
  }
  ```

### 4.z-index定位

- 相当于穿墙术

  ```css
  .tipText{
  	color: greenyellow;
  	/*方法一  相当于穿墙术 数值越大可穿层数越多*/
  	/*z-index: 999;*/
  }
  ```

  



