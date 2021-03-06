# MySql免安装版及其配置

> ==概述==

　MySQL关是一种关系数据库管理系统，所使用的 SQL 语言是用于访问[数据库](https://baike.baidu.com/item/数据库/103728)的最常用的

标准化语言，其特点为体积小、速度快、总体拥有成本低，尤其是[开放源码](https://baike.baidu.com/item/开放源码/7176422)这一特点，在 Web

应用方面 MySQL 是最好的 RDBMS(Relational Database Management System：关系数据

库管理系统)应用软件之一。



首先：要先进入mysql官网里（Mysql的官网-->https://www.mysql.com/），下面是详细步骤：↓

　　(为了方便大家的操作，我的网盘里有安装包：

　　　 链接：https://pan.baidu.com/s/1Bk6OVk-F6rlastyMW0hozA 
					提取码：twnn

　　)

## 一、下载安装包：

①进入官网后，点击"Dowload"，然后页面往下拉

![image-20211003002335074](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003002342.png)

②接下来看到的页面是这样的，红色框框的链接就是mysql社区版，是免费的mysql版本，然后我们点击这个框框的链接：↓

![image-20211003002514296](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003002514.png)

③接下来跳转到这个页面，在这里，我们只要下载社区版的Server就可以了：↓

![image-20211003002559151](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003002559.png)

④下载免安装版(windows以外的其他系统除外)

![image-20211003002712330](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003002712.png)





> **==注意，安装的目录应当放在指定位置，，其次，绝对路径中避免出现中文，推荐首选英文为命名条件！！！！(我的为参考)==**

![image-20211003003056574](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003003056.png)

## 二、Mysql配置

以管理员身份打开如下命令

![image-20211003003335913](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003003336.png)

　①下转到mysql的bin目录下：

![image-20211003003527866](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003003527.png)

②安装mysql的服务：mysqld --install

![image-20211003003631896](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003003631.png)

③初始化mysql，在这里，初始化会产生一个随机密码,如下图框框所示，记住这个密码，后面会用到(mysqld --initialize --console)

![image-20211003003747760](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003003747.png)

④开启mysql的服务(net start mysql)

![image-20211003003849625](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003003849.png)

　⑤登录验证，mysql是否安装成功！(要注意上面产生的随机密码，不包括前面符号前面的空格，否则会登陆失败)，如果和下图所示一样，则说明你的mysql已经安装成功！注意，，一定要先开启服务，不然会登陆失败，出现拒绝访问的提示符！！！

 ![image-20211003004022489](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003004022.png)

>  ==修改密码：==

　　　　由于初始化产生的随机密码太复杂，，不便于我们登录mysql，因此，我们应当修改一个自己能记住的密码！！

![image-20211003004159159](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003004159.png)

再次登录验证新密码：

![image-20211003004305305](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003004305.png)

　**设置系统的全局变量：**

　　　　为了方便登录操作mysql，在这里我们设置一个全局变量：↓

 

　　　　①点击"我的电脑"-->"属性"-->''高级系统设置''-->''环境变量'',接下来如下图所操作

> ==win 7==

![image-20211003004638765](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003004638.png)

> ==win 10==

![image-20211003004959707](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211003004959.png)

配置完成之后，每当我们想要用命令行使用mysql时，只需要win+R，-->输入"cmd"打开命令行，之后输入登录sql语句即可。

> **==在mysql目录下创建一个ini或cnf配置文件，在这里我创建的是ini配置文件，里面写的代码是mysql的一些基本配置==**

具体内容如下

```cmd

# For advice on how to change settings please see
# http://dev.mysql.com/doc/refman/5.6/en/server-configuration-defaults.html
# *** DO NOT EDIT THIS FILE. It's a template which will be copied to the
# *** default location during install, and will be replaced if you
# *** upgrade to a newer version of MySQL.
[client]
default-character-set = utf8mb4
[mysql]
default-character-set = utf8mb4
[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_bin
init_connect='SET NAMES utf8mb4'
# Remove leading # and set to the amount of RAM for the most important data
# cache in MySQL. Start at 70% of total RAM for dedicated server, else 10%.
innodb_buffer_pool_size = 128M
# Remove leading # to turn on a very important data integrity option: logging
# changes to the binary log between backups.
# log_bin
# These are commonly set, remove the # and set as required.
# 记得把下面的两个路径替换成自己的安装路径
basedir = D:\mysql-8.0.21-winx64\mysql-8.0.21-winx64
datadir = D:\mysql-8.0.21-winx64\mysql-8.0.21-winx64\data
port = 3306
# server_id = .....
# Remove leading # to set options mainly useful for reporting servers.
# The server defaults are faster for transactions and fast SELECTs.
# Adjust sizes as needed, experiment to find the optimal values.
join_buffer_size = 128M
sort_buffer_size = 16M
read_rnd_buffer_size = 16M 
sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES
```

