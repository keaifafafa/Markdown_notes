# JavaWeb

## 1、基本概念

### 1.1、前言

web开发：

- web，网页的意思 ， www.baidu.com
- 静态web
  - html，css
  - 提供给所有人看的数据始终不会发生变化！
- 动态web
  - 淘宝，几乎是所有的网站；
  - 提供给所有人看的数据始终会发生变化，每个人在不同的时间，不同的地点看到的信息各不相同！
  - 技术栈：Servlet/JSP，ASP，PHP

在Java中，动态web资源开发的技术统称为JavaWeb；

### 1.2、web应用程序

web应用程序：可以提供浏览器访问的程序；

- a.html、b.html…多个web资源，这些web资源可以被外界访问，对外界提供服务；
- 你们能访问到的任何一个页面或者资源，都存在于这个世界的某一个角落的计算机上。
- URL
- 这个统一的web资源会被放在同一个文件夹下，web应用程序–>Tomcat：服务器

- 一个web应用由多部分组成 （静态web，动态web）
  - html，css，js
  - jsp，servlet
  - Java程序
  - jar包
  - 配置文件 （Properties）

web应用程序编写完毕后，若想提供给外界访问：需要一个服务器来统一管理；

### 1.3、静态web

- *.htm, *.html,这些都是网页的后缀，如果服务器上一直存在这些东西，我们就可以直接进行读取。通络；

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200517145610480.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

静态web存在的缺点

- Web页面无法动态更新，所有用户看到都是同一个页面
  - 轮播图，点击特效：伪动态
  - JavaScript [实际开发中，它用的最多]
  - VBScript
- 它无法和数据库交互（数据无法持久化，用户无法交互）

### 1.4、动态web

页面会动态展示： “Web的页面展示的效果因人而异”；

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200517145638566.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

缺点：

- 加入服务器的动态web资源出现了错误，我们需要重新编写我们的

  后台程序

  ,重新发布；

  - 停机维护

优点：

- Web页面可以动态更新，所有用户看到都不是同一个页面
- 它可以与数据库交互 （数据持久化：注册，商品信息，用户信息…）

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200517145733386.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

## 2、web服务器

### 2.1、技术讲解

**ASP:**

- 微软：国内最早流行的就是ASP；

- 在HTML中嵌入了VB的脚本， ASP + COM；

- 在ASP开发中，基本一个页面都有几千行的业务代码，页面极其混乱

- 维护成本高！

- C#

- IIS

  ```html
  <h1>
      <h1><h1>
          <h1>
              <h1>
                  <h1>
          <h1>
              <%
              System.out.println("hello")
              %>
              <h1>
                  <h1>
     <h1><h1>
  <h1>
  ```

**php：**

- PHP开发速度很快，功能很强大，跨平台，代码很简单 （70% , WP）
- 无法承载大访问量的情况（局限性）

**JSP/Servlet : **

B/S：浏览和服务器

C/S: 客户端和服务器

- sun公司主推的B/S架构
- 基于Java语言的 (所有的大公司，或者一些开源的组件，都是用Java写的)
- 可以承载三高问题带来的影响；
- 语法像ASP ， ASP–>JSP , 加强市场强度；

### 2.2、web服务器

服务器是一种被动的操作，用来处理用户的一些请求和给用户一些响应信息；

**IIS**

微软的； ASP…,Windows中自带的

 **Tomcat** 

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200517145921499.png) 

 面向百度编程； 

 Tomcat是Apache 软件基金会（Apache Software Foundation）的Jakarta 项目中的一个核心项目，最新的Servlet 和JSP 规范总是能在Tomcat 中得到体现，因为Tomcat 技术先进、性能稳定，而且**免费**，  因而深受Java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的Web 应用服务器。 

 Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用[服务器](https://baike.baidu.com/item/服务器)， 在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选。对于一个Java初学web的人来说，它是最佳的选择

Tomcat 实际上运行JSP 页面和Servlet。Tomcat最新版本为**9.0。**

 **工作3-5年之后，可以尝试手写Tomcat服务器；** 

下载tomcat：

1. 安装 or 解压
2. 了解配置文件及目录结构
3. 这个东西的作用

## 3、Tomcat

### 3.1、 安装tomcat

tomcat官网：http://tomcat.apache.org/

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200517150026375.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![img](https://img-blog.csdnimg.cn/20200517150042598.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

### 3.2、Tomcat启动和配置

文件夹作用：

 ![img](https://img-blog.csdnimg.cn/20200517150516571.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 **启动。关闭Tomcat** 

 ![img](https://img-blog.csdnimg.cn/20200517150548429.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

访问测试：http://localhost:8080/

可能遇到的问题：

1. Java环境变量没有配置
2. 闪退问题：需要配置兼容性
3. 乱码问题：配置文件中设置

### 3.3、配置

 ![img](https://img-blog.csdnimg.cn/2020051715062347.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

可以配置启动的端口号

- tomcat的默认端口号为：8080
- mysql：3306
- http：80
- https：443

```
<Connector port="8081" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />
```

可以配置主机的名称

- 默认的主机名为：localhost->127.0.0.1

- 默认网站应用存放的位置为：webapps

  ```
  <Host name="www.qinjiang.com"  appBase="webapps"
          unpackWARs="true" autoDeploy="true">
  ```

  

#### 高难度面试题：

请你谈谈网站是如何进行访问的！

1. 输入一个域名；回车
2. 检查本机的 C:\Windows\System32\drivers\etc\hosts配置文件下有没有这个域名映射；

1. 有：直接返回对应的ip地址，这个地址中，有我们需要访问的web程序，可以直接访问

   ```java
   127.0.0.1       www.qinjiang.com
   1
   ```

2. 没有：去DNS服务器找，找到的话就返回，找不到就返回找不到；

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(20200517150736566.png)(JavaWeb.assets/1567827057913.png)]](https://img-blog.csdnimg.cn/20200517150736566.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

3. 可以配置一下环境变量（可选性） 

### 3.4、发布一个web网站

不会就先模仿

- 将自己写的网站，放到服务器(Tomcat)中指定的web应用的文件夹（webapps）下，就可以访问了

 网站应该有的结构 

```
--webapps ：Tomcat服务器的web目录
	-ROOT
	-kuangstudy ：网站的目录名
		- WEB-INF
			-classes : java程序
			-lib：web应用所依赖的jar包
			-web.xml ：网站配置文件
		- index.html 默认的首页
		- static 
            -css
            	-style.css
            -js
            -img
         -.....
```

 HTTP协议 ： 面试 

 Maven：构建工具 

- Maven安装包

Servlet 入门

- HelloWorld！
- Servlet配置
- 原理

## 4、Http

### 4.1、什么是HTTP

HTTP（超文本传输协议）是一个简单的请求-响应协议，它通常运行在TCP之上。

- 文本：html，字符串，~ ….
- 超文本：图片，音乐，视频，定位，地图…….
- 80

Https：安全的

- 443

### 4.2、两个时代

- http1.0
  - HTTP/1.0：客户端可以与web服务器连接后，只能获得一个web资源，断开连接
- http2.0
  - HTTP/1.1：客户端可以与web服务器连接后，可以获得多个web资源。‘

### 4.3、Http请求

- 客户端—发请求（Request）—服务器

 百度： 

```
Request URL:https://www.baidu.com/   请求地址
Request Method:GET    get方法/post方法
Status Code:200 OK    状态码：200
Remote（远程） Address:14.215.177.39:443
```

```
Accept:text/html  
Accept-Encoding:gzip, deflate, br
Accept-Language:zh-CN,zh;q=0.9    语言
Cache-Control:max-age=0
Connection:keep-alive
```

#### 1、请求行

- 请求行中的请求方式：GET

请求方式：**Get，Post**

- get：请求能够携带的参数比较少，大小有限制，会在浏览器的URL地址栏显示数据内容，不安全，但高效

- post：请求能够携带的参数没有限制，大小没有限制，不会在浏览器的URL地址栏显示数据内容，安全，但不高效。

#### 2、消息头

```
Accept：告诉浏览器，它所支持的数据类型
Accept-Encoding：支持哪种编码格式  GBK   UTF-8   GB2312  ISO8859-1
Accept-Language：告诉浏览器，它的语言环境
Cache-Control：缓存控制
Connection：告诉浏览器，请求完成是断开还是保持连接
HOST：主机..../.
```

### 4.4、Http响应

- 服务器—响应-----客户端

 百度： 

```
Cache-Control:private    缓存控制
Connection:Keep-Alive    连接
Content-Encoding:gzip    编码
Content-Type:text/html   类型
```

#### 1.响应体

```
Accept：告诉浏览器，它所支持的数据类型
Accept-Encoding：支持哪种编码格式  GBK   UTF-8   GB2312  ISO8859-1
Accept-Language：告诉浏览器，它的语言环境
Cache-Control：缓存控制
Connection：告诉浏览器，请求完成是断开还是保持连接
HOST：主机..../.
Refresh：告诉客户端，多久刷新一次；
Location：让网页重新定位；
```

#### 2、响应状态码

200：请求响应成功 200

3xx：请求重定向

- 重定向：你重新到我给你新位置去；

4xx：找不到资源 404

- 资源不存在；

5xx：服务器代码错误 500 502:网关错误

**常见面试题：**

当你的浏览器中地址栏输入地址并回车的一瞬间到页面能够展示回来，经历了什么？

## 5、 Maven

**我为什么要学习这个技术？**

1. 在Javaweb开发中，需要使用大量的jar包，我们手动去导入；

2. 如何能够让一个东西自动帮我导入和配置这个jar包。

   由此，Maven诞生了！

### 5.1 Maven项目架构管理工具

我们目前用来就是方便导入jar包的！

Maven的核心思想：**约定大于配置**

- 有约束，不要去违反。

 Maven会规定好你该如何去编写我们的Java代码，必须要按照这个规范来； 

### 5.2 下载安装Maven

官网;https://maven.apache.org/

 ![1567842350606.png](https://img-blog.csdnimg.cn/20200517150821356.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

下载完成后，解压即可；

友情建议：电脑上的所有环境都放在一个文件夹下，方便管理；

### 5.3 配置环境变量

在我们的系统环境变量中

配置如下配置：

- M2_HOME maven目录下的bin目录
- MAVEN_HOME maven的目录
- 在系统的path中配置 %MAVEN_HOME%\bin

 ![1567842882993.png](https://img-blog.csdnimg.cn/20200517150856266.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 测试Maven是否安装成功，保证必须配置完毕！ 

### 5.4 阿里云镜像

maven文件夹下conf/settings.xml

```
<mirror>
      <id>nexus-aliyun</id>
	  <mirrorOf>central</mirrorOf>
	  <name>Nexus aliyun</name>
	  <url>http://maven.aliyun.com/nexus/content/repositories/central/</url>
 </mirror>
```

### 5.5 本地仓库

maven有本地仓库和远程仓库；
**建立一个本地仓库**（同样在settings.xml）

```
<localRepository>E:\maven\apache-maven-3.6.3\maven-repo</localRepository>
```

### 5.6、在IDEA中使用Maven

1. 启动IDEA
2. 创建一个MavenWeb项目

 ![1567844785602.png](https://img-blog.csdnimg.cn/2020051715092913.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![img](https://img-blog.csdnimg.cn/20200517151018731.png) 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-xGmf4fAh-1589699013798)(JavaWeb.assets/1567844917185.png)]](https://img-blog.csdnimg.cn/20200517151042646.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-ycRMS61O-1589699013799)(JavaWeb.assets/1567844956177.png)]](https://img-blog.csdnimg.cn/20200517151106318.png) 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-df7cEval-1589699013799)(JavaWeb.assets/1567845029864.png)]](https://img-blog.csdnimg.cn/20200517151139194.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

3.等待项目初始化完毕 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-7YjYqWMI-1589699013800)(JavaWeb.assets/1567845105970.png)]](https://img-blog.csdnimg.cn/20200517151202868.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-7bL5fNUH-1589699013801)(JavaWeb.assets/1567845137978.png)]](https://img-blog.csdnimg.cn/20200517151219667.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

4. 观察maven仓库中多了什么东西？ 

5. IDEA中的Maven设置

   注意：IDEA项目创建成功后，看一眼Maven的配置

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-KIvQxMcI-1589699013802)(JavaWeb.assets/1567845341956.png)]](https://img-blog.csdnimg.cn/20200517151244408.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-wD1b7VJu-1589699013803)(JavaWeb.assets/1567845413672.png)]](https://img-blog.csdnimg.cn/20200517151259570.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 6.到这里，Maven在IDEA中的配置和使用就OK了! 

### 5.7、创建一个普通的Maven项目

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-QOhUhthW-1589699013804)(JavaWeb.assets/1567845557744.png)]](https://img-blog.csdnimg.cn/20200517151320910.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-eaSz8VOW-1589699013805)(JavaWeb.assets/1567845717377.png)]](https://img-blog.csdnimg.cn/20200517151347191.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 这个只有在Web应用下才会有！ 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-b010Tvy5-1589699013806)(JavaWeb.assets/1567845782034.png)]](https://img-blog.csdnimg.cn/20200517151404360.png) 

### 5.8 标记文件夹功能

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-lW860qjA-1589699013807)(JavaWeb.assets/1567845910728.png)]](https://img-blog.csdnimg.cn/20200517151420677.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-ntnkuofI-1589699013808)(JavaWeb.assets/1567845957139.png)]](https://img-blog.csdnimg.cn/20200517151438765.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![1567846034906.png](https://img-blog.csdnimg.cn/20200517151450119.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![1567846073511.png](https://img-blog.csdnimg.cn/20200517151515673.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

### 5.9 在 IDEA中配置Tomcat

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-K22Inlfp-1589699013810)(JavaWeb.assets/1567846140348.png)]](https://img-blog.csdnimg.cn/2020051715155548.png) 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-iI5YyUs8-1589699013810)(JavaWeb.assets/1567846179573.png)]](https://img-blog.csdnimg.cn/20200517151611112.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-SIVSb4Pr-1589699013811)(JavaWeb.assets/1567846234175.png)]](https://img-blog.csdnimg.cn/20200517151623509.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-mCzVoJxr-1589699013812)(JavaWeb.assets/1567846369751.png)]](https://img-blog.csdnimg.cn/20200517151636624.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

解决警告问题

必须要的配置：**为什么会有这个问题：我们访问一个网站，需要指定一个文件夹名字；**

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-MjYaIf65-1589699013812)(JavaWeb.assets/1567846421963.png)]](https://img-blog.csdnimg.cn/20200517151657895.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-M7YVUqqd-1589699013813)(JavaWeb.assets/1567846546465.png)]](https://img-blog.csdnimg.cn/2020051715171370.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-eci1Ycd1-1589699013813)(JavaWeb.assets/1567846559111.png)]](https://img-blog.csdnimg.cn/20200517151732961.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

### 5.10 pom文件

pom.xml 是Maven的核心配置文件

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-2BbRob8f-1589699013815)(JavaWeb.assets/1567846784849.png)]](https://img-blog.csdnimg.cn/20200517151820925.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!--Maven版本和头文件-->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!--这里就是我们刚才配置的GAV-->
    <groupId>com.kuang</groupId>
    <artifactId>javaweb-01-maven</artifactId>
    <version>1.0-SNAPSHOT</version>
    <!--Package：项目的打包方式
  jar：java应用
  war：JavaWeb应用
  -->
    <packaging>war</packaging>


    <!--配置-->
    <properties>
        <!--项目的默认构建编码-->
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <!--编码版本-->
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <!--项目依赖-->
    <dependencies>
        <!--具体依赖的jar包配置文件-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
        </dependency>
    </dependencies>

    <!--项目构建用的东西-->
    <build>
        <finalName>javaweb-01-maven</finalName>
        <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
            <plugins>
                <plugin>
                    <artifactId>maven-clean-plugin</artifactId>
                    <version>3.1.0</version>
                </plugin>
                <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
                <plugin>
                    <artifactId>maven-resources-plugin</artifactId>
                    <version>3.0.2</version>
                </plugin>
                <plugin>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.8.0</version>
                </plugin>
                <plugin>
                    <artifactId>maven-surefire-plugin</artifactId>
                    <version>2.22.1</version>
                </plugin>
                <plugin>
                    <artifactId>maven-war-plugin</artifactId>
                    <version>3.2.2</version>
                </plugin>
                <plugin>
                    <artifactId>maven-install-plugin</artifactId>
                    <version>2.5.2</version>
                </plugin>
                <plugin>
                    <artifactId>maven-deploy-plugin</artifactId>
                    <version>2.8.2</version>
                </plugin>
            </plugins>
        </pluginManagement>
    </build>
</project>
```

 maven由于他的约定大于配置，我们之后可以能遇到我们写的配置文件，无法被导出或者生效的问题，解决方案： 

```xml
<!--在build中配置resources，来防止我们资源导出失败的问题-->
<build>
    <resources>
        <resource>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>true</filtering>
        </resource>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>true</filtering>
        </resource>
    </resources>
</build>
```

### 5.12 IDEA操作

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-0Tw48WvY-1589699013816)(JavaWeb.assets/1567847630808.png)]](https://img-blog.csdnimg.cn/20200517151952315.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-ttjYAwqN-1589699013816)(JavaWeb.assets/1567847662429.png)]](https://img-blog.csdnimg.cn/20200517152031212.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

## 6、Servlet

### 6.1 Servlet简介

- Servlet是sun公司开发的动态web的一项技术

- Sun在API中提供一个接口叫做：Servlet，开发一个Servlet程序需要完成两个小步骤：


1. 编写一个类，实现servlet接口；
2. 把开发好的Java类部署到web服务器上。

 **把实现了Servlet接口的Java程序叫做，Servlet** 

### 6.2 编写HelloServlet程序

 Serlvet接口Sun公司有两个默认的实现类：HttpServlet，GenericServlet 

1. 构建一个普通的Maven项目，删掉里面的src目录,在这个项目里面建立Moudel(模块)，这个空的工程就是Maven主工程；
2. 在Maven父子工程中

- 父项目的pom.xml中自动生成

```xml
<modules>
    <module>servlet-01</module>
    <module>servlet-02</module>
</modules>
//告诉编译器，在读取主pom时，去找两个子pom
```

- 子项目的pom.xml生成的

```xml
<parent>
    <artifactId>javaweb-02servlet</artifactId>
    <groupId>com.fafa</groupId>
    <version>1.0-SNAPSHOT</version>
</parent>
//使子项目继承父项目的设置，避免重复导入依赖
```

 父项目中的java,子项目可以直接使用 （相当于继承）

```java
son extends father
```

 3.Maven环境优化
1.修改web.xml为最新（去tomca文件夹下的webapps下去取）；
2.将maven结构搭建完整，，main下建java文件夹，resources文件夹 

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429120520900.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

4. 编写一个Servlet程序 

    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429121134795.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

    1.编写一个普通类
   2.实现Servlet接口，这里我们直接继承HttpServlet（`HttpServlet实现了Servlet接口`） 

   ```java
   public class HelloServlet extends HttpServlet {
   
       //get post只是请求实现的不同方式，所有这里两个方法可以相互调用，业务逻辑是相同的
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           System.out.println("doget");
           PrintWriter writer = resp.getWriter();//响应流
           writer.print("hello,servlet");
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           super.doPost(req, resp);
       }
   }
   ```

5.编写Servlet的映射
   为什么需要映射？
   我们写的是Java程序，但是需要通过浏览器访问，而浏览器需要连接web服务器，所以我们需要在web服务中注册我们写的Servlet，还需要给它一个浏览器能够访问的路径；

```xml
<!--注册Servlet-->
<servlet>
    <servlet-name>hello</servlet-name>
    <servlet-class>com.fafa.servlet.HelloServlet</servlet-class>
</servlet>
<!--Servlet的请求路径-->
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

6.配置Tomcat
注意配置项目发布路径即可。

7.启动项目
启动后通过请求路径访问程序。
— 域名/发布路径/请求路径

### 6.3 Servlet原理

 Servlet是由Web服务器调用的，web服务器收到浏览器请求后： 

![servlet原理](servlet原理.png)

### 6.4 Mapping问题

1. 一个Servlet可以指定一个映射路径 

   ```xml
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/hello</url-pattern>
   </servlet-mapping>
   ```

2.  一个Servlet可以指定多个映射路径 

   ```xml
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/hello</url-pattern>
   </servlet-mapping>
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/hello2</url-pattern>
   </servlet-mapping>
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/hello3</url-pattern>
   </servlet-mapping>
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/hello4</url-pattern>
   </servlet-mapping>
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/hello5</url-pattern>
   </servlet-mapping>
   ```

3.  一个Servlet可以指定通用映射路径 

   ```xml
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/hello/*</url-pattern>
   </servlet-mapping>
   ```

4.  默认请求路径 （会干掉默认的index.jsp）

   ```xml
   <!--默认请求路径-->
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>/*</url-pattern>
   </servlet-mapping>
   ```

5.  指定一些后缀或者前缀等等…. 

   ```xml
   <!--可以自定义后缀实现请求映射
       注意点，*前面不能加项目映射的路径
       hello/sajdlkajda.qinjiang
       -->
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>*.cxd</url-pattern>
   </servlet-mapping>
   ```

6.  优先级问题
   指定了固有的映射路径优先级最高，如果找不到就会走默认的处理请求； 

```xml
<!--404-->
<servlet>
    <servlet-name>error</servlet-name>
    <servlet-class>com.fafa.servlet.ErrorServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>error</servlet-name>
    <url-pattern>/*</url-pattern>
</servlet-mapping>

```

### 6.5 ServletContext

#### 1. 数据共享 Attribute

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    //this.getInitParameter(); 初始化参数
    //this.getServletConfig(); Servlet配置
    //this.getServletContext(); Servlet上下文
    ServletContext context = this.getServletContext();

    String username = "可爱发";//数据
    context.setAttribute("username",username);//将一个数据保存在了ServletContext中，名字为"username" 值为 username
}
```

存完后其他类也可以调用context里的已有数据

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    ServletContext context = this.getServletContext();//获取上下文对象
    String username = (String)context.getAttribute("username");//默认是 Object 对象，强制转化为 String

    //设置编码 和 文本格式
    resp.setContentType("text/html");
    resp.setCharacterEncoding("utf-8");
    //打印
    resp.getWriter().print("名字"+username);
}
```

#### 2. 初始化数据 InitParameter

写在web.xml里的

```xml
<!--配置一些web应用初始化参数-->
<context-param>
    <param-name>url</param-name>
    <param-value>jdbc:mysql://localhost:3306/mybatis</param-value>
</context-param>
```

```java
//java程序可以进行调用
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    ServletContext context = this.getServletContext();
    String url = context.getInitParameter("url");//获取初始化参数
    resp.getWriter().print(url);
}
```

#### 3.  请求转发(转发和重定向不同)RequestDispatcher

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    ServletContext context = this.getServletContext();
    System.out.println("进入gs4");
    RequestDispatcher requestDispatcher = context.getRequestDispatcher("/gs3");//转发的请求的路径
    requestDispatcher.forward(req,resp);//调用forward 实现转发请求

}
```

图片上面的一行是转发

图片下面的一行是重定向

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200517144308725.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 



#### 4. 读取资源文件 Properties

Properties

- 在java目录下新建properties
- 在resources目录下新建properties

 发现：都被打包到了同一个路径下：classes，我们俗称这个路径为classpath: 

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200517144950788.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 思路：需要一个文件流； 

```Pro
username=root12312
password=zxczxczxc
```

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    ServletContext context = this.getServletContext();
    System.out.println("进入gs5");
    //利用字节输入流读取 资源文件
    InputStream is = context.getResourceAsStream("/WEB-INF/classes/db.properties");

    Properties prop = new Properties();
    prop.load(is);//读取
    String user = prop.getProperty("username");
    String pwd = prop.getProperty("password");

    resp.getWriter().print(user+":"+pwd);

}

@Override
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    doGet(req, resp);
}
```

### 6.6 HttpServletResponse

 web服务器接收到客户端的http请求，针对这个请求，分别创建一个代表请求的HttpServletRequest对象，代表响应的一个HttpServletResponse； 

- 如果要获取客户端请求过来的参数：找HttpServletRequest
- 如果要给客户端响应一些信息：找HttpServletResponse

#### 1、简单分类

 负责向浏览器发送数据的方法 

```java
ServletOutputStream getOutputStream() throws IOException;
PrintWriter getWriter() throws IOException;
```

 负责向浏览器发送响应头的方法 

```java
void setCharacterEncoding(String var1);

void setContentLength(int var1);

void setContentLengthLong(long var1);

void setContentType(String var1);

void setDateHeader(String var1, long var2);

void addDateHeader(String var1, long var2);

void setHeader(String var1, String var2);

void addHeader(String var1, String var2);

void setIntHeader(String var1, int var2);

void addIntHeader(String var1, int var2);
```

响应的状态吗

```java
int SC_CONTINUE = 100;
int SC_SWITCHING_PROTOCOLS = 101;
int SC_OK = 200;
int SC_CREATED = 201;
int SC_ACCEPTED = 202;
int SC_NON_AUTHORITATIVE_INFORMATION = 203;
int SC_NO_CONTENT = 204;
int SC_RESET_CONTENT = 205;
int SC_PARTIAL_CONTENT = 206;
int SC_MULTIPLE_CHOICES = 300;
int SC_MOVED_PERMANENTLY = 301;
int SC_MOVED_TEMPORARILY = 302;
int SC_FOUND = 302;
int SC_SEE_OTHER = 303;
int SC_NOT_MODIFIED = 304;
int SC_USE_PROXY = 305;
int SC_TEMPORARY_REDIRECT = 307;
int SC_BAD_REQUEST = 400;
int SC_UNAUTHORIZED = 401;
int SC_PAYMENT_REQUIRED = 402;
int SC_FORBIDDEN = 403;
int SC_NOT_FOUND = 404;
int SC_METHOD_NOT_ALLOWED = 405;
int SC_NOT_ACCEPTABLE = 406;
int SC_PROXY_AUTHENTICATION_REQUIRED = 407;
int SC_REQUEST_TIMEOUT = 408;
int SC_CONFLICT = 409;
int SC_GONE = 410;
int SC_LENGTH_REQUIRED = 411;
int SC_PRECONDITION_FAILED = 412;
int SC_REQUEST_ENTITY_TOO_LARGE = 413;
int SC_REQUEST_URI_TOO_LONG = 414;
int SC_UNSUPPORTED_MEDIA_TYPE = 415;
int SC_REQUESTED_RANGE_NOT_SATISFIABLE = 416;
int SC_EXPECTATION_FAILED = 417;
int SC_INTERNAL_SERVER_ERROR = 500;
int SC_NOT_IMPLEMENTED = 501;
int SC_BAD_GATEWAY = 502;
int SC_SERVICE_UNAVAILABLE = 503;
int SC_GATEWAY_TIMEOUT = 504;
int SC_HTTP_VERSION_NOT_SUPPORTED = 505;
```

#### 2、下载文件

1. 向浏览器输出消息 （一直在讲，就不说了）

2. 下载文件
   1.要获取下载文件的路径
   2.下载的文件名是啥？
   3.设置想办法让浏览器能够支持下载我们需要的东西
   4.获取下载文件的输入流
   5.创建缓冲区
   6.获取OutputStream对象
   7.将FileOutputStream流写入到buffer缓冲区
   8.使用OutputStream将缓冲区中的数据输出到客户端！

   ```java
   @Override
   protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
       //1.要获取下载的文件路径
       /*String realPath = this.getServletContext().getRealPath("/1.jpg");//这样写是默认从tomcat文件夹下找*/
       //所以建议写死
       String realPath = "D:\\java_all_projects\\idea_java_projects\\JavaWeb\\javaweb-02-servlet02\\response\\src\\main\\rescourse\\1.jpg";
       System.out.println("下载的文件的路径"+realPath);
       //2.下载的文件名是啥
       String fileName = realPath.substring(realPath.lastIndexOf("\\") + 1);
       //3.设置想办法让浏览器能够支持（Content-disposition）下载我们需要的东西
       resp.setHeader("Content-disposition","attachment;filename"+fileName);//不要去记，用的时候百度就行
       //4.获取下载文件的输入流
       FileInputStream in = new FileInputStream(realPath);
       //5.创建缓冲区
       int len = -1;
       byte[] buffer = new byte[1024];
       //6.获取OutputStream对象
       ServletOutputStream out = resp.getOutputStream();
       //7.将FileOutputStream流 写到buffer缓冲区中
       while((len = in.read(buffer)) != -1){
           // 8.使用OutputStream将缓冲区的数据输出到客户端
           out.write(buffer,0,len);
       }
       //9.关闭资源
       out.close();
       in.close();
   }
   ```

   

#### 3、验证码功能

 验证怎么来的？ 

- 前端实现

- 后端实现，需要用到 Java 的图片类，生产一个图片

  ```java
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
      //如何让浏览器每3秒自动刷新
      resp.setHeader("refresh","3");
  
      //在内存中创建一个图片
      BufferedImage image = new BufferedImage(80,20,BufferedImage.TYPE_INT_BGR);
  
      //得到图片
      Graphics2D g = (Graphics2D) image.getGraphics();//2D笔
  
      //设置图片的背景颜色
      g.setBackground(Color.white);
      g.fillRect(0,0,80,20);
  
      //给图片写数据
      g.setColor(Color.blue);
      g.setFont(new Font(null,Font.BOLD,20));
      g.drawString(makeNum(),0,20);
  
      //告诉浏览器，请求用图片的方式打开
      resp.setContentType("image/jpg");
      //网站存在缓存，不让浏览器缓存
      resp.setDateHeader("expires",-1);
      resp.setHeader("Cache-Control","no-cache");
      resp.setHeader("Pragma","no-cache");
  
      //把图片写给浏览器
      ImageIO.write(image,"jpg",resp.getOutputStream());
  }
  //生成随机数
  private String makeNum(){
      Random random = new Random();
      String num = random.nextInt(9999999) + ""; //强转为 String 类型
      StringBuffer sb = new StringBuffer();
      for (int i = 0;i < 7 - num.length(); i++ ){//可以将省略掉的0 在末尾自动加上 保证是7位数
          sb.append("0");
      }
      num = sb.toString() + num; //不足7位 用 0 填充
      return num;
  }
  ```
#### 4、实现重定向

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-9NJ2vj90-1589707801677)(JavaWeb.assets/1567931587955.png)]](https://img-blog.csdnimg.cn/20200517173048836.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 B一个web资源收到客户端A请求后，B他会通知A客户端去访问另外一个web资源C，这个过程叫重定向 

常见场景：

- 用户登录

  ```java
  void sendRedirect(String var1) throws IOException;
  ```

测试:

```java
//重定向
public class RedirectServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.sendRedirect("/down1/img");//重定向
        //重定向原理
        /*resp.setHeader("Location","/down1/img");
        resp.setStatus(302);*/
    }

```

 面试题：请你聊聊重定向和转发的区别？ 

- 相同点:
  - ​	页面都会实现跳转
- 不同点:
  - 请求转发的时候，url不会产生变化
  - 重定向时候，url地址栏会发生变化；

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-xJgrIcLc-1589707801679)(JavaWeb.assets/1567932163430.png)]](https://img-blog.csdnimg.cn/20200517173027847.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

#### 5、简单实现用户登录重定向

写在index.jsp里

```jsp
<%--这里提交的路径，需要寻找到项目的路径--%>
<%--${pageContext.request.contextPath}代表当前的项目--%>
<form action="${pageContext.request.contextPath}/login" method="get">
    用户名：<input type="text" name="username"> <br/>
    密码：<input type="password" name="password"> <br/>
    <input type="submit">
</form>
```

java源程序代码

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    //处理请求
    String username = req.getParameter("username");
    String password = req.getParameter("password");

    System.out.println(username+":"+password);

    //重定向
    resp.sendRedirect("/down1/success.jsp");//一定要注意路径问题  否则404
}

```

### 6.7HttpServletRequest

 HttpServletRequest代表客户端的请求，用户通过Http协议访问服务器，HTTP请求中的所有信息会被封装到HttpServletRequest，通过这个HttpServletRequest的方法，获得客户端的所有信息； 

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-hfcvtn9l-1589707801681)(JavaWeb.assets/1567933996830.png)]](https://img-blog.csdnimg.cn/20200517173128566.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

 ![1567934023106.png](https://img-blog.csdnimg.cn/20200517173143988.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjM5MDQzMw==,size_16,color_FFFFFF,t_70) 

#### 1.获取参数，请求转发

 ![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-4WNj9b9h-1589707801684)(JavaWeb.assets/1567934110794.png)]](https://img-blog.csdnimg.cn/20200517173205122.png) 

java代码

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    //        设置编码（后期会用过滤器来代替）
    req.setCharacterEncoding("UTF-8");
    resp.setCharacterEncoding("UTF-8");
    //获取请求的数值 并在后台打印
    String username = req.getParameter("username");
    String password = req.getParameter("password");
    String[] hobbys = req.getParameterValues("hobbys");
    System.out.println("==================");
    System.out.println("用户名："+username);
    System.out.println("==================");
    System.out.println("密码"+password);
    System.out.println("==================");
    System.out.println("爱好"+Arrays.toString(hobbys));
    System.out.println("==================");

    //通过请求转发
    //这里的 / 代表当前的web应用 和重定向有区别
    req.getRequestDispatcher("/success.jsp").forward(req,resp);
}

```

#### 2.**面试题：请你聊聊重定向和转发的区别？**

相同点

- 页面都会实现跳转

不同点

- 请求转发的时候，url不会产生变化; 307
- 重定向时候，url地址栏会发生变化； 302

## 7、Cookie、Session

### 7.1、会话

**会话**：用户打开一个浏览器，点击很多超链接，访问多个web资源，关闭浏览器，这个过程可以称之为会话

- **有状态会话**：

  **你怎么证明你是某某学校的学生？**

  1. 发票
  2. 学校登记

  **一个网站怎么证明你来过？**

  客户端   服务端

  1. 服务端给客户端发送一个信件，客户端下次访问服务端带上信件就可以，cookie
  2. 服务器登记你来过，下次你来的时候我来匹配你 ，session。

### 7.2 、保存会话的两种技术

**cookie**：

- 客户端技术（响应，请求）

**session**

- 服务端技术，利用这个技术，可以保存用户的会话信息，我们可以把信息或者数据放在Session中！



常见应用：网站登陆之后，你下次不用在登陆了，第二次访问直接就上去了。

### 7.3、Cookie

![1620961189421](1620961189421.png)

1. 从请求中拿到cookie信息

2. 服务器响应给客户端cookie

   ```java
   Cookie[] cookies = req.getCookies();//Cookie，服务端从客户端获取
   cookie.getName();//获得cookie的key
   cookie .getValue();//获得cookie的value
   new Cookie("lastLoginTime",System.currentTimeMillis()+"");//新建一个cookie
   cookie.setMaxAge(20*60*60);//设置cookie有效期 为 一天
   resp.addCookie(cookie);//响应给客户端一个cookie
   ```

   **cookie：一般会保存在本地的 用户目录下 appdata；**

一个网站cookie是否存在上限 **聊聊细节问题**

- 一个cookie只能保存一个信息；
- 一个web站点可以给浏览器发送多个cookie，最多存放20个cookie；
- cookie大小有限制 4kb；
- 300个cookie 浏览器上限



删除cookie：

1. 不设置有效期，关闭浏览器，Session自动失效；
2. 设置有效期 时间  如果设置为 0 ，就会被秒删除

编码解码：

```java
//编码
Cookie cookie = new Cookie("name",URLEncoder.encode("发发", "UTF-8"));
//解码                   
out.write(URLDecoder.decode(cookie.getValue(),"UTF-8"));
```

### 7.4 、Session（重点）

什么是Session:

- 服务器会给每一个用户(浏览器)创建一个Session对象
- 一个Session独占一个浏览器，只要浏览器没有关闭，这个Session就存在；
- 用户登录之后，整个网站他都可以访问！ -->保存用户信息

Session和Cookie的区别：

- ​	Cookie把用户的数据写给用户的浏览器，浏览器保存(可以有多个)
- ​    Session把用户的数据写到用户独占的Session中，服务器端保存（保存重要信息，减少服务器资源的浪费  ）
- ​    Session对象由服务器创建

使用场景：

- 保存一个登录用户的信息；
- 购物车信息；
- 在整个网站中经常会使用的数据，我们将它保存在Session中

会话自动过期：web.xml

```xml
<!--设置session默认的失效时间-->
<session-config>
    <!--以分钟单位  一般设置几个小时就够了-->
    <session-timeout>20</session-timeout>
</session-config>
```

使用session

```java
package com.fafa.servlet;

import com.fafa.pojo.Person;

import javax.servlet.ServletException;
import javax.servlet.http.*;
import java.io.IOException;

public class SessionDemo01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决乱码问题
        req.setCharacterEncoding("UTF-8");
        resp.setContentType("text/html");
        resp.setCharacterEncoding("UTF-8");

        //得到Session
        HttpSession session = req.getSession();

        //给Session中存东西
        session.setAttribute("name","发发");
        //可以传对象
        session.setAttribute("person",new Person("可爱发",21));

        //获取session的id
        String sessionId = session.getId();

        //判断Session是不是新创建的
        if(session.isNew()){
            resp.getWriter().write("session创建成功，ID"+session);
        }else{
            resp.getWriter().write("session已经在服务器中存在了，ID："+sessionId);
        }
        //session创建的时候做了什么事情
        Cookie cookie = new Cookie("JSESSIONID",sessionId);
        resp.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}


//得到session
HttpSession session = req.getSession();
//数据共享 和 ServletContext 类似  但是比他要好
/*String name = (String)session.getAttribute("name");
System.out.println("名字是"+name);
resp.getWriter().write(name);*/
//同时也可以接收对象的值
Person person = (Person)session.getAttribute("person");
resp.getWriter().write(person.toString());  //换行 对 前台页面显示 不起作用
System.out.println(person.toString());

HttpSession session = req.getSession();
//移除
session.removeAttribute("name");
//手动注销session
session.invalidate();
```

## 8、JSP

### 8.1、什么是JSP

Java Server Pages:java服务端页面，也和Servlet一样，用于动态web技术！

最大的特点；

- 写JSP就像是在写html
- JSP页面中可以嵌入java代码，为用户提供动态数据

### 8.2、JSP原理

 思路：JSP到底怎么执行的！ 

- 代码层面没有任何问题

- 服务器内部工作

  tomcat中有一个work目录；

  IDEA中使用Tomcat的会在IDEA的tomcat中产生一个work目录；

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506184154282.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 

我电脑的地址：

**C:\Users\Administrator.IntelliJIdea2018.1\system\tomcat\Unnamed_javaweb-session-cookie\work\Catalina\localhost\ROOT\org\apache\jsp**

 发现页面转变成了Java程序！ 

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506184204931.png) 

**浏览器向服务器发送请求，不管访问什么资源，其实都是在访问Servlet！**

JSP最终也会被转换成一个JAVA类！

**JSP本质上就是一个Servlet**

```java
//初始化
public void _jspInit() {
}
//销毁
public void _jspDestroy() {
}
//JSPService
public void _jspService(.HttpServletRequest request, .HttpServletResponse response)
```

1. 判断请求

2. 内置一些对象

   ```java
   final javax.servlet.jsp.PageContext pageContext;//页面上下文
   javax.servlet.http.HttpSession session = null;//session
   final javax.servlet.ServletContext application;//applicationContext
   final javax.servlet.ServletConfig config;//config
   javax.servlet.jsp.JspWriter out = null;//out
   final java.lang.Object page = this;//page：当前
   HttpServletRequest request;//请求
   HttpServletResponse response ;//响应
   ```

3. 输出页面前增加的代码

   ```java
   response.setContentType("text/html");       //设置响应的页面类型
   pageContext = _jspxFactory.getPageContext(this, request, response,null, true, 8192, true);
   _jspx_page_context = pageContext;
   application = pageContext.getServletContext();
   config = pageContext.getServletConfig();
   session = pageContext.getSession();
   out = pageContext.getOut();
   _jspx_out = out;
   ```

4. 以上的这些对象我们可以在JSP页面里直接使用

    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200506183804973.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 

在JSP页面中；

只要是 JAVA代码就会原封不动的输出；

如果是HTML代码，就会被转换为：

```jsp
out.write("<html>\r\n");
```

 这样的格式，输出到前端！ 

### 8.3、JSP基础语法

 任何语言都有自己的语法，JAVA中有,。 JSP 作为java技术的一种应用，它拥有一些自己扩充的语法（了解，知道即可！），Java所有语法都支持！ 

#### JSP表达式

```jsp
<%--JSP表达式
    作用：用来将程序的输出，输出到客户端
    <%= 变量或者表达式%>
--%>
<%= new java.util.Date()%>
```

#### jsp脚本片段

```jsp
<%--jsp脚本片段--%>
<%
int sum = 0;
for (int i = 1; i <=100 ; i++) {
    sum+=i;
}
out.println("<h1>Sum="+sum+"</h1>");
%>
```

 **脚本片段的再实现** 

```jsp
<%
int x = 10;
out.println(x);
%>
<p>这是一个JSP文档</p>
<%
int y = 2;
out.println(y);
%>

<hr>


<%--在代码嵌入HTML元素--%>
<%
for (int i = 0; i < 5; i++) {
    %>
<h1>Hello,World  <%=i%> </h1>
<%
}
%>
```

#### JSP声明

```jsp
<%!
    static {
    System.out.println("Loading Servlet!");
}

private int globalVar = 0;

public void kuang(){
    System.out.println("进入了方法Kuang！");
}
%>
```

JSP声明：会被编译到JSP生成Java的类中！其他的，就会被生成到_jspService方法中！

在JSP，嵌入Java代码即可！

```jsp
<%%>
<%=%>
<%!%>

<%--注释--%>
```

 **JSP的注释，不会在客户端显示，HTML就会！** 

### 8.4、JSP指令

```jsp
<%@page args.... %>
<%@include file=""%>

<%--@include会将两个页面合二为一--%>

<%@include file="common/header.jsp"%>
<h1>网页主体</h1>

<%@include file="common/footer.jsp"%>

<hr>


<%--jSP标签
    jsp:include：拼接页面，本质还是三个
        --%>
<jsp:include page="/common/header.jsp"/>
<h1>网页主体</h1>
<jsp:include page="/common/footer.jsp"/>
```

### 8.5、9大内置对象

- PageContext 存东西
- Request  存东西
- Response
- Session   存东西
- Application  【ServletContext】存东西
- config 【ServletConfig】
- out
- page   几乎不用了已经
- exception

```jsp
pageContext.setAttribute("name1","发发1");//保存的数据只在一个页面中有效
request.setAttribute("name2","发发2");//保存的数据指在一次请求中有效，请求转发会携带这个数据
session.setAttribute("name3","发发3");//保存的数据只在一次会话中有效，从打开浏览器到关闭浏览器
application.setAttribute("name4","发发4");//保存的数据只在服务器中有效，从打开服务器到关闭服务器
```

request：客户端向服务器发送请求，产生的数据，用户看完就没用了，比如:新闻，用户看完没用的!

session：客户端向服务器发送的请求，产生的数据，用户用完一会还有用，比如：购物车；

application：客户端向服务器发送请求，产生数据，一个用户用完了，其他用户还可能使用，比如:聊天数据

### 8.6 、JSP标签、JSL标签、EL表达式

```xml
<!-- JSTL表达式的依赖 -->
<dependency>
    <groupId>javax.servlet.jsp.jstl</groupId>
    <artifactId>jstl-api</artifactId>
    <version>1.2</version>
</dependency>
<!-- standard标签库 -->
<dependency>
    <groupId>taglibs</groupId>
    <artifactId>standard</artifactId>
    <version>1.1.2</version>
</dependency>
```

EL表达式：${}

- **获取数据**
- **执行运算**
- **获取web开发的常用对象**

**JSP标签**

```jsp
<%--jsp:include--%>
<%--
    http：//localhost:8080/jsp1/jsptag.jsp?name=keaifa&age=21
    可以把参数传过去
    --%>
<jsp:forward page="/jsptag2.jsp">
    <jsp:param name="name" value="keaifa"></jsp:param>
    <jsp:param name="age" value="21"></jsp:param>
</jsp:forward>

```

**JSTL表达式**

 **JSTL标签库的使用就是为了弥补HTML标签的不足；它自定义许多标签，可以供我们使用，标签的功能和Java代码一样！** 

**格式化标签**

**SQL标签**

**XML 标签**

**核心标签** （掌握部分）

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508152235704.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 

 **JSTL标签库使用步骤** 

- **引入对应的 taglib**
- **使用其中的方法**
- **在Tomcat 也需要引入 jstl的包，否则会报错：JSTL解析错误**

 **c：if** 

```jsp
<h4>if测试</h4>
<form action="coreif.jsp" method="get">
    <%--
    EL表达式获取表单中的数据
    ${param.参数名}
    --%>
    <input type="text" name="username" value="${param.username}">
    <input type="submit" value="登录">
</form>

<%--判断如果提交的用户名是管理员则登陆成功--%>
<%--<%
    if(request.getParameter("username").equals("admin"))
        out.println("Success");
%>--%>
<c:if test="${param.username == 'admin'}" var = "isAdmin">
    <c:out value="管理员欢迎您！"/>
</c:if>

<%--自闭合标签--%>
<c:out value="${isAdmin}"/>
```

 **c:choose c:when** 

```jsp
<body>

    <%--定义一个变量score，值为85--%>
    <c:set var="score" value="55"/>

    <c:choose>
        <c:when test="${score>=90}">
            你的成绩为优秀
        </c:when>
        <c:when test="${score>=80}">
            你的成绩为一般
        </c:when>
        <c:when test="${score>=70}">
            你的成绩为良好
        </c:when>
        <c:when test="${score<=60}">
            你的成绩为不及格
        </c:when>
    </c:choose>

</body>
```

 **c:forEach** 

```jsp
<%--
    var,每一次遍历出来的变量
    iteams,要遍历的对象
    begin， 哪里开始
    end ，哪里结束
    step， 步长
--%>
<c:forEach var="people" items="${list}">
    <c:out value="${people}"/>
    <br/>
</c:forEach>

<hr/>

<c:forEach var="people" items="${list}" begin="0" end="4" step="1">
    <c:out value="${people}"/>
    <br/>
</c:forEach>
```

### 8.7 [JSP中out.write()和out.print()的区别](https://www.cnblogs.com/kabi/p/5182890.html)

 **out对象的类型是JspWriter。JspWriter继承了java.io.Writer类。**

**1）print方法是子类JspWriter，write是Writer类中定义的方法；**

**2）重载的print方法可将各种类型的数据转换成字符串的形式输出，而重载的write方法只能输出字符、字符数组和字符串等与字符相关的数据；**

**3）JspWriter类型的out对象使用print方法和write方法都可以输出字符串，但是，如果字符串对象的值为null时，print方法将输出内容为“null”的字符串，而write方法则是抛出NullPointerException异常。例如：**

下面的test.jsp文件：

```jsp
<% String str=null;

out.print(str);

//out.write(str); 
```

## 9、JavaBean

实体类

JavaBean有特定的写法：

- 必须要有一个无参构造
- 属性必须私有化
- 必须要对应的get/set方法；

一般用来和数据库的字段做映射 ORM；

ORM：对象关系映射

- 表--->类
- 字段--->属性
- 行记录--->类的对象

**people类**

| id   | name    | age  | address |
| ---- | ------- | ---- | ------- |
| 1    | 发发1号 | 18   | 北京    |
| 2    | 发发2号 | 19   | 北京    |
| 3    | 发发3号 | 20   | 北京    |

```java
class People{
    private int id;
    private String name;
    private String address;
}

class A{
    new People(1,"发发1号",18，"北京");
    new People(2,"发发2号",19，"北京");
    new People(3,"发发3号",20，"北京");
}
```

## 10.MVC三层架构(微服务之前一直用的)

MVC:  Model View Controller 模型 视图 控制器

### 10.1 以前的架构

 ![(img-NGdCSHqw-1588757845418)(JavaWeb.assets/1568423664332.png)](https://img-blog.csdnimg.cn/20200508154442187.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 



 用户直接访问控制层，控制层就可以直接操作数据库； 

```txt
servlet--CRUD-->数据库
弊端：程序十分臃肿，不利于维护  
servlet的代码中：处理请求、响应、视图跳转、处理JDBC、处理业务代码、处理逻辑代码

架构：没有什么是加一层解决不了的！
程序猿调用
↑
JDBC （实现该接口）
↑
Mysql Oracle SqlServer ....（不同厂商）
```

### 10.2、MVC三层架构

 ![[(img-BWDJGUCN-1588757845419)(JavaWeb.assets/1568424227281.png)]](https://img-blog.csdnimg.cn/20200508154512751.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 

Model

- 业务处理 ：业务逻辑（Service）
- 数据持久层：CRUD （Dao - 数据持久化对象）

View

- 展示数据
- 提供链接发起Servlet请求 （a，form，img…）

Controller （Servlet）

- 接收用户的请求 ：（req：请求参数、Session信息….）
- 交给业务层处理对应的代码
- 控制视图的跳转

```txt
登录--->接收用户的登录请求--->处理用户的请求（获取用户登录的参数，username，password）---->交给业务层处理登录业务（判断用户名密码是否正确：事务）--->Dao层查询用户名和密码是否正确-->数据库
```

## 11.Filter(重点)

 比如 Shiro安全框架技术就是用Filter来实现的 

 **Filter：过滤器 ，用来过滤网站的数据；** 

- 处理中文乱码
- 登录验证….

 （比如用来过滤网上骂人的话，我***我自己 0-0） 

 ![(img-QEq74VyV-1588757845420)(JavaWeb.assets/1568424858708.png)](https://img-blog.csdnimg.cn/20200508154536177.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 

Filter开发步骤：

1. 导包

2. 编写过滤器

   1.导包不要错 **（注意）**

 ![[(img-HHsC3JBD-1588757845420)(JavaWeb.assets/1568425162525.png)]](https://img-blog.csdnimg.cn/20200508154555952.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 

 实现Filter接口，重写对应的方法即可 

```java
package com.fafa.filter;

import javax.servlet.*;
import java.io.IOException;

public class CharacterEncodingFilter implements Filter {
    // 初始化  web服务器启动时 就已经初始化了
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("CharacterEncodingFilter初始化");
    }
    //Chain ：链
    /*
1.过滤中的所有代码，在过滤特定的请求的时候都会执行
2.必须要让过滤器继续通行
chain.doFilter(request,response);
* */
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        request.setCharacterEncoding("utf-8");
        response.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=UTF-8");

        System.out.println("CharacterEncodingFilter执行前。。。。。");
        chain.doFilter(request,response);//让我们的请求继续走，如果不写，程序到这里就会被拦截
        System.out.println("CharacterEncodingFilter执行后。。。。。");
    }
    //销毁   服务器关闭的时候被销毁
    public void destroy() {
        System.out.println("CharacterEncodingFilter被销毁");
    }
}

```

3. 在web.xml中配置 Filter 

```xml
<!--过滤器-->
<filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>com.fafa.filter.CharacterEncodingFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <!--servlet文件夹下的所有都会进行过滤-->
    <url-pattern>/servlet/*</url-pattern>
    <!--这种是整个网页都会被过滤-->
    <!--<url-pattern>/*</url-pattern>-->
</filter-mapping>
```

## 12、监听器

实现一个监听器的接口；（有n种监听器）

1. 编写一个监听器

   实现监听器的接口…

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020050820562995.png) 

依赖的jar包

```java
//统计网站在线人数 ： 统计session
public class OnlineCountListener implements HttpSessionListener {

    //创建session监听： 看你的一举一动
    //一旦创建Session就会触发一次这个事件！
    public void sessionCreated(HttpSessionEvent se) {
        ServletContext ctx = se.getSession().getServletContext();

        System.out.println(se.getSession().getId());

        Integer onlineCount = (Integer) ctx.getAttribute("OnlineCount");

        if (onlineCount==null){
            onlineCount = new Integer(1);
        }else {
            int count = onlineCount.intValue();
            onlineCount = new Integer(count+1);
        }

        ctx.setAttribute("OnlineCount",onlineCount);

    }

    //销毁session监听
    //一旦销毁Session就会触发一次这个事件！
    public void sessionDestroyed(HttpSessionEvent se) {
        ServletContext ctx = se.getSession().getServletContext();

        Integer onlineCount = (Integer) ctx.getAttribute("OnlineCount");

        if (onlineCount==null){
            onlineCount = new Integer(0);
        }else {
            int count = onlineCount.intValue();
            onlineCount = new Integer(count-1);
        }

        ctx.setAttribute("OnlineCount",onlineCount);

    }


    /*
    Session销毁：
    1. 手动销毁  getSession().invalidate();
    2. 自动销毁
     */
}

```

 2.web.xml中注册监听器 

```xml
<!--注册监听器-->
<listener>
    <listener-class>com.kuang.listener.OnlineCountListener</listener-class>
</listener>
```

3.看情况使用

## 13、过滤器、监听器常见应用

 **监听器：GUI编程中经常使用；** 

```java
public class TestPanel {
    public static void main(String[] args) {
        Frame frame = new Frame("中秋节快乐");  //新建一个窗体
        Panel panel = new Panel(null); //面板
        frame.setLayout(null); //设置窗体的布局

        frame.setBounds(300,300,500,500);
        frame.setBackground(new Color(0,0,255)); //设置背景颜色

        panel.setBounds(50,50,300,300);
        panel.setBackground(new Color(0,255,0)); //设置背景颜色

        frame.add(panel);

        frame.setVisible(true);

        //监听事件，监听关闭事件
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                super.windowClosing(e);
            }
        });

    }
}
```

**Filter登录小应用；**

 用户登录之后才能进入主页！用户注销后就不能进入主页了！ 

1. 用户登录之后，向Sesison中放入用户的数据
2.  进入主页的时候要判断用户是否已经登录；要求：在过滤器中实现！ 

```java
HttpServletRequest request = (HttpServletRequest) req;
HttpServletResponse response = (HttpServletResponse) resp;

if (request.getSession().getAttribute(Constant.USER_SESSION)==null){
    response.sendRedirect("/error.jsp");
}

chain.doFilter(request,response);
```

## 14、JDBC

###  什么是JDBC ： Java连接数据库！ 

 ![img](https://img-blog.csdnimg.cn/20200508154620734.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 

需要jar包的支持：

- java.sql
- javax.sql
- mysql-conneter-java… 连接驱动（必须要导入）

 **实验环境搭建** 

```mysql
CREATE TABLE users(
    id INT PRIMARY KEY,
    `name` VARCHAR(40),
    `password` VARCHAR(40),
    email VARCHAR(60),
    birthday DATE
);

INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(1,'张三','123456','zs@qq.com','2000-01-01');
INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(2,'李四','123456','ls@qq.com','2000-01-01');
INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(3,'王五','123456','ww@qq.com','2000-01-01');


SELECT	* FROM users;
```

 导入数据库依赖 

```xml
<!--mysql的驱动-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.47</version>
</dependency>
```

 IDEA中连接数据库： 

 ![[(img-XErw4ElS-1588757845423)(JavaWeb.assets/1568440926845.png)]](https://img-blog.csdnimg.cn/20200508154638633.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 

### **JDBC 固定步骤：**

1. 加载驱动
2. 连接数据库,代表数据库
3. 创建向数据库发送SQL的对象Statement : CRUD
4. 编写SQL （根据业务，不同的SQL）
5. 执行SQL
6. 关闭连接（先开的后关）

```java
import java.sql.*;

public class TestJdbc {
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        //配置信息
        //useUnicode=true&characterEncoding=UTF-8 解决中文乱码
        String url = "jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=UTF-8";
        String username = "root";
        String password = "root";

        //1.加载驱动
        Class.forName("com.mysql.jdbc.Driver");
        //2.连接数据库
        Connection connection = DriverManager.getConnection(url, username, password);
        //3.向数据库发送SQL的对象Statement preparedStatement：CRUD
        Statement st = connection.createStatement();
        //        connection.prepareStatement(sql);  //预编译类型
        //4.编写SQL语句
        String sql = "select * from users";

        //5.执行SQL，返回一个ResultSet：结果集
        ResultSet rs = st.executeQuery(sql);
        //增删改查操作语句
        int i = st.executeUpdate(sql);//返回的是影响的行数

        //循环遍历结果
        while (rs.next()){
            System.out.println("id="+rs.getObject("id"));
            System.out.println("name="+rs.getObject("name"));
            System.out.println("password="+rs.getObject("password"));
            System.out.println("email="+rs.getObject("email"));
            System.out.println("birthday="+rs.getObject("birthday"));
        }

        //6.关闭连接 释放资源  先打开的后关闭（和IO流一样）
        rs.close();
        st.close();
        connection.close();
    }
}

```

 **预编译SQL** 

```java
import java.sql.*;

public class TestJdbc2 {
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        //配置信息
        //useUnicode=true&characterEncoding=UTF-8 解决中文乱码
        String url = "jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=UTF-8";
        String username = "root";
        String password = "root";

        //1.加载驱动
        Class.forName("com.mysql.jdbc.Driver");
        //2.连接数据库
        Connection connection = DriverManager.getConnection(url, username, password);

        //3.编写SQL语句
        String sql = "insert into users(id,name,password,email,birthday) values(?,?,?,?,?)";

        //4.预编译 preparedStatement：CRUD
        PreparedStatement preparedStatement = connection.prepareStatement(sql);

        preparedStatement.setInt(1,15);//给第一个占位符？ 的值赋值为15
        preparedStatement.setString(2,"可爱发学JAVA");//给第二个占位符？ 的值赋值为 可爱发学JAVA
        preparedStatement.setString(3,"741888");//给第三个占位符？ 的值赋值为 741888
        preparedStatement.setString(4,"648119398@qq.com");//给第四个占位符？ 的值赋值为 648119398@qq.com
        preparedStatement.setDate(5,new Date(new java.util.Date().getTime()));//给第五个占位符？ 的值赋值为 new Date(new java.util.Date().getTime())

        //增删改查操作语句
        int i = preparedStatement.executeUpdate();//返回的是影响的行数
        if (i > 0){
            System.out.println("插入成功@");
        }

        //6.关闭连接 释放资源  先打开的后关闭（和IO流一样）
        preparedStatement.close();
        connection.close();
    }
}

```

### 事务

##### 1、**事务**：

<font color='cornflowerblue'> 在数据库中,所谓事务是指一组逻辑操作单元即一组sql语句。当这个单元中的一部分操作失败,整个事务回滚，只有全部正确才完成提交。判断事务是否配置成功的关键点在于出现异常时事务是否会回滚 </font>

<font color='red'>要么都成功，要么都失败！</font>

##### 2、**事务四大特性**

<font color='red'>AICD</font>原则：保证数据的安全

**2.1.原子性（Atomicity）**
原子性是指事务是一个不可分割的工作单位，事务中的操作要么都发生，要么都不发生。

**2.2.一致性（Consistency）**
事务必须使数据库从一个一致性状态变换到另外一个一致性状态。(数据不被破坏

**2.3.隔离性（Isolation）**
事务的隔离性是指一个事务的执行不能被其他事务干扰.

**2.4.持久性（Durability）**
持久性是指一个事务一旦被提交，它对数据库中数据的改变就是永久性的.即使系统重启也不会丢失.

```SQL
/*默认的话为自动提交，
当没执行一个update ,delete或者insert的时候都会自动提交到数据库，无法回滚事务。
设置connection.setautocommit(false);只有程序调用connection.commit()的时候才会将先前执行的语句一起提交到数据库，这样就实现了数据库的事务。*/
开启事务setAutoCommit();
事务提交 commit()
事务回滚 rollback()
关闭事务

转账：
A:1000；
B:1000；

A（900）  --100--> B（1100）
```

##### **3、事务要放在Service层**

结合事务的特点，为什么加在service层就很好解释了。如果我们的事务注解@Transactional加在dao层，那么只要与数据库做增删改，就要提交一次事务，如此做事务的特性就发挥不出来，尤其是事务的一致性，当出现并发问题是，用户从数据库查到的数据都会有所偏差。
一般的时候，我们的service层可以调用多个dao层，我们只需要在service层加一个事务注解@Transactional，这样我们就可以一个事务处理多个请求，事务的特性也会充分的发挥出来。

### Junit单元测试

依赖

```xml
<!--单元测试依赖-->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
</dependency>
```

简单使用

@Test注解只有在方法上有效，只要加了这个注解的方法，就可以直接运行！

```java
public class TestJdbc03 {

    @Test
    //    导入junit依赖 添加Test注解 这样可以直接测试方法
    // 但是不能测试static方法   有错误的也不行  比如除数为 0
    public void test(){
        System.out.println("你好");//成功案例
        System.out.println(10/0);//失败案例
    }
}

```

 ![[(img-OsUubVNQ-1588757845424)(JavaWeb.assets/1568442261610.png)]](https://img-blog.csdnimg.cn/20200508154657792.png) 

 失败的时候是红色： 

 ![[(img-qv2oTEGI-1588757845425)(JavaWeb.assets/1568442289597.png)]](https://img-blog.csdnimg.cn/20200508154708211.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 

 **搭建一个环境** 

```sql
CREATE TABLE account(
    id INT PRIMARY KEY AUTO_INCREMENT,
    `name` VARCHAR(40),
    money FLOAT
);

INSERT INTO account(`name`,money) VALUES('A',1000);
INSERT INTO account(`name`,money) VALUES('B',1000);
INSERT INTO account(`name`,money) VALUES('C',1000);
```

测试事务

```java
import org.junit.Test;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class TestJdbc04 {

    @Test
    //    这样可以直接测试方法   但是不能测试static方法   有错误的也不行  比如除数为 0
    public void test(){
        //配置信息
        //useUnicode=true&characterEncoding=UTF-8 解决中文乱码
        String url = "jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=UTF-8";
        String username = "root";
        String password = "root";

        Connection connection = null;
        Statement st = null ;
        try {
            //1.加载驱动
            Class.forName("com.mysql.jdbc.Driver");
            //2.连接数据库
            connection = DriverManager.getConnection(url, username, password);

            /*//通知开启事务 false 是开启
            connection.setAutoCommit(false);*/
            //3.向数据库发送SQL的对象Statement：CRUD
            st = connection.createStatement();
            String sql = "update account set money = money - 100 where name = 'A'";
            st.executeUpdate(sql);

            int i = 1/0; //制造一个异常

            String sql2 = "update account set money = money + 100 where name = 'B'";
            st.executeUpdate(sql2);

            connection.commit();//以上两条SQL都执行了，则提交事务
            System.out.println("success");
        } catch (Exception e) {
            //如果出现异常就回滚
            try {
                connection.rollback();
            } catch (SQLException e1) {
                e1.printStackTrace();
            }
        } finally {
            //关闭资源
            try {
                st.close();
                connection.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}

```

## 15、文件上传及下载

### 1.准备工作

下载一些组件（ common-fileupload 和  于common-io ）

对于文件上传，浏览器在上传的过程中是将文件以流的形式提交到服务器端的。

一般采用Apache的开源工具common-fileupload这个文件上传组件。

common-fileupload是依赖于common-io这个包的，所以还需要下载这个包。

 在JavaWeb项目中导入Jar包： 

创lib文件夹 然后将jar粘贴到里面  然后右击lib 点击添加到内库（图中的箭头所指位置）

![1624164781681](1624164781681.png)

### 2、实用类介绍

【文件上传注意介绍】

1. 为保证服务器的安全，上传的文件应放在外界无法访问的目录下，如WEN-INF
2. 为防止同名文件产生覆盖现象，要为文件指定一个唯一的文件名( UUID )
3. 要对上传文件的大小进行限制
4. 要限制上传文件的类型，收到的文件时，判断文件名是否合法。

【需要用到的类详解】

 **ServletFileUpload**负责处理上传的文件数据，并将表单中的每个输入项封装成一个**FileItem对象**，在使用ServletFileUpload对象解析请求时需要**DiskFileItemFactory对象**。所以，我们需要在进行解析工作前构造好DiskFileItemFactory对象，通过ServletFileItem对象的构造方法或setFileItemFactory()设置ServletFileUpload对象的**fileItemFactory**属性。 

 **FileItem类** 

 在HTML页面中必须要有name：<p><input type="file" value="文件上传" name="file"></p>

<font color='red'>  **表单中如果包含一个文件上传项的话，这个表单** </font>的<font color='cornflowerblue'>entype属性</font>必须设置为<font color='red'>multipart/form-data</font>

```jsp
<form action="${pageContext.request.contextPath}/upload.do" method="post"enctype="multipart/form-data">
    <p>用户名：<input type="text" name="username" placeholder="请填写用户名"></p>
    <p>上传文件：<input type="file" name="filename"></p>
    <p><input type="submit" value="提交"><input type="reset" value="重置"></p>
```

 **浏览器的表单类型为multipart/form-data的话，服务器想获取数据就要通过流** 

 【常用方法介绍】 

```java
//isFormFile方法用于判断FileItem类对象封装的数据是一个普通文本表单
//还是一个文件表单，如果时普通表单字段则返回true，否则返回false
boolean isField();

//getFieldName方法用于返回表单标签name属性的值
String getFieldName();
//getString方法用于将FileItem对象中保存的数据流内容以一个字符串返回
String getString();

//getName方法用于获得文件上传字段中的文件名。
String getName();

//以流的形式返回上传文件的数据内容。
InputStream getInputStream();

//delete方法用来清空FileItem类对象中存放的主体内容
//如果主体内容被保存在临时文件中，delete方法将删除该临时文件
void delete();
```

