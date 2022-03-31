## 写在前面

前端请求后端数据的时候，总是会**超时**，有时候使用**Navicat**刷新**远程数据库**的时候，也会卡很久，就是卡在一个空白界面，

于是我就怀疑是数据库（**Mysql**）的问题

果然在我的一番百度下，终于找到了答案【嘻嘻】

 ![image-20220208113918350](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220208113927.png)

## 如何解决

> ==方式一：使用命令行==

linux服务器环境下 

修改 /etc/my.cnf 文件

在 [mysqld]下面加入 下面这句配置

 ![image-20220208121443279](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220208121443.png)

==skip-name-resolve==

> ==方式二：使用宝塔==

在 [mysqld]下面加入 下面这句配置

==skip-name-resolve==

 ![image-20220208114402366](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220208114402.png)

**两种方式没区别，只不过宝塔对于小白更加友好些**

## 这样做的影响

skip-name-resolve 

选项就能禁用DNS解析，连接速度会快很多。不过，这样的话就不能在MySQL的授权表中使用主机名了而只能用ip格式。

若使用–skip-grant-tables系统将对任何用户的访问不做任何访问控制，但可以用 mysqladmin flush-privileges或mysqladmin reload来开启访问控制;默认情况是

show databases语句对所有用户开放，

如果mysql服务器没有开远程帐户，就在my.ini里面加上skip-grant-tables

附,请根据情况开放

skip-name-resolve  一般我们只要这一项便可以 
