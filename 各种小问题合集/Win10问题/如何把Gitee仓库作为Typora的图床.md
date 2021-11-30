> ==为什么要使用Gitee仓库作为Typora的图床==

本人原来一直是使用**Github仓库**作为图床，但是有很多弊端**在国内**，首先图片上传完以后需要**翻墙**才能在**博客**内显示，传到**CSDN或者博客园**，大部分图片是无法正常显示的，这就很麻烦，毕竟博客写了就是**为了给其他人看**的嘛，总不能让读者**翻墙**去看吧=_=，故此我便开始换成**Gitee（码云）**了，容量大，而且不用翻墙，图片就可以正常显示。

> ==需要准备的资源==

- 一个Gitee的账号
- PicGo
- Typora

## 1、Pic安装和配置

PicGo简单点说就是一个图床上传工具，我们主要就是借助这个软件进行上传

这一点非常重要！

下载地址给大家：

https://github.com/Molunerfinn/PicGo/releases/tag/v2.3.0-beta.4

![image-20210926145121582](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210926145128.png)

对应于你的操作系统来安装。

安装完成后启动，mac的需要注意，打开后会自动最小化在状态栏，右击就可以进主窗口。

![image-20210926145218624](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210926145218.png)

根据我下面的指示做，安装gitee的插件，记住一定要按照成功，不然无法进行下面的操作。

![image-20210926145336096](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210926145336.png)

安装成功后，我们可以看到如下界面

![image-20210926145438066](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210926145438.png)

## 2、创建Gitee仓库

前往gitee，然后按照我下方的照片进行创建，记住一定要初始化项目(生成readme)

官方网址：https://gitee.com/

> ==新建仓库==

![image-20210926145715131](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210926145715.png)

![image-20210926150059175](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210926150059.png)

> ==创建完成后，点击头像然后进入设置，进入私密令牌==

![image-20210926150251340](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210926150251.png)

> ==右上角生成一个令牌，然后将令牌的密钥复制好！待会我们需要用到配置，最好保存在txt文本，防止丢失。==

![image-20210926150430438](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210926150430.png)

## 3、配置秘钥

> ==前往picGo，点击Gitee图床，进行配置==

![image-20210926150943590](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210926150943.png)

## 4、配置Typora

进入Typora偏好设置->图像，对其进行下面图片的配置。

![image-20210926151303954](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210926151304.png)

点击验证图片上传选项，显示成功的话就成功啦！！！

![image-20210926151315624](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210926151315.png)