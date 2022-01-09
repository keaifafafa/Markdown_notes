## 一、问题背景

由于学习需要，安装了Docker在win10上，导致VMware无法启动（版本15.0.5），于是卸载了VMware，重新安装最新版（16.1），但是总是失败，原因如下：

 ![image-20211226122616259](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226122616.png)

> ==问题原因==

出现上述问题的原因就是没有完全卸载掉VMware

建议安装15.5，16安装上以后，vmtools总是安装失败！

## 二、如何正确卸载VMware

### 1、下载一个比较老的VMware的安装包

清除安装信息必须使用很旧的安装包，最好是我这个VMware-workstation-full-15.0.2-10952284.exe，版本号为15.0.2的安装包，VMware-workstation-full-15.0.2-10952284.exe的下载地址：[==点此下载==](https://download3.vmware.com/software/wkst/file/VMware-workstation-full-15.0.2-10952284.exe?HashKey=db56b8c60ad82b772965fbfe7e321830&ext=.exe&params={"custnumber"%3A"JWRkcEBlQGV3dA%3D%3D"%2C"sourcefilesize"%3A"511.84+MB"%2C"dlgcode"%3A"WKST-1502-WIN"%2C"languagecode"%3A"cn"%2C"source"%3A"DOWNLOADS"%2C"downloadtype"%3A"manual"%2C"eula"%3A"Y"%2C"downloaduuid"%3A"411a51c6-9b6d-470e-9c47-73d17d8113e3"%2C"purchased"%3A"N"%2C"dlgtype"%3A"Product+Binaries"%2C"productversion"%3A"15.0.2"%2C"productfamily"%3A"VMware+Workstation+Pro"}&AuthKey=1585035857_b5b275b750f13ec18dc9d16d5dea6ae2&ext=.exe)

### 2、输入命令行清除VMware数据

1、win+x调出powershell

 ![image-20211226123733308](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226123733.png)

2、将下载的VMware-workstation-full-15.0.2-10952284.exe文件路径粘贴到命令行后面跟空格和 “/c”回车即可。格式：EXE文件路径 /c

 ![image-20211226123800667](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226123800.png)

3、点击确定即可，清理完成。

4、安装你想安装的版本吧！

## 三、安装中可能会遇到的问题

>  ==VMware Workstation-- “与 vmx86 驱动程序的版本不匹配: 预期为 390.0,实际为 360.0等等。 驱动程序“vmx86.sys...”==

解决办法：右键我的电脑->属性->控制面板主页->程序->程序和功能->找到VMware，右键更改然后会出现修复->点击修复等待完成就可以使用VMware了

 ![image-20211226124028119](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226124028.png)

 ![image-20211226124044434](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226124044.png)

如果还是不能解决问题，直接点击管理员身份运行。

## 四、VMware版本下载小技巧

vmware每次都要登录才能下载，太闹心了，一个小技巧教你绕过登录去下载

> ==例子：==

下载链接：

https://download3.vmware.com/software/wkst/file/VMware-workstation-full-15.0.4-12990004.exe

在vmware官网该位置输入希望下载的软件名称，如：vmware workstation pro，进入对应软件的搜索页

搜索页

 ![image-20211226124329870](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226124329.png)

选择希望下载的版本，进入下载页面

下载页

 ![image-20211226124418269](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226124418.png)

在下载页中点击了解更多

软件详情

 ![image-20211226124511945](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226124512.png)

复制软件详情中的name，将其替换到文章开头的链接中，将替换后的链接输入到浏览器中，即可完成下载。