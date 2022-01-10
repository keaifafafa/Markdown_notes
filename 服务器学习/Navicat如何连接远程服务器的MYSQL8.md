## 前言：

> ==运行环境及工具==

1. Navicat for Mysql

2. 腾讯云轻量级服务器一台（Centos 7）

3. Mysql 8.0.24（远程服务器内安装的）

4. Xshell7（连接操作远程服务器）

   

## 一、修改mysql的远程授权登录设置

### 1、登录远程服务器的数据库（使用Xshell）

```bash
mysql -uroot -p    ## 以root登录数据库 
```

输入root的登录密码，成功后会看到以下信息：

 ![image-20220110215436712](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220110215446.png)

### 2、查看mysql服务当前的默认端口

```bash
use mysql;    ## 选择mysql数据库
select user,host from user;    ## 查看用户访问端口
```

 ![image-20220110215606429](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220110215606.png)

> ==**说明**：root用户默认的是localhost，说明只允许从本地登录mysql服务。而我们要从远程以root用户连接数据库，就必须修改host的值，改为**'%'**：允许任何ip访问。==

### 3.修改host允许任何ip访问

继续在命令面板输入以下指令：

```bash
update user set host = '%' where user = 'root';
```

 ![image-20220110215750876](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220110215750.png)

看到以上信息说明修改成功！

这时再使用之前的命令：

```bash
select user,host from user;    ## 查看用户访问端口
```

会看到：root用户的host已经修改为'%'！

 ![image-20220110215828349](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220110215828.png)

> ==**注意**：**修改完成后 还需要刷新一下服务配置，不然修改不会生效，并且第4步会执行失败。**==

接着在命令面板输入：

```bash
mysql> FLUSH PRIVILEGES;    ## 刷新服务配置项
```

显示**Query OK**,表示刷新完成。现在就可以配置我们想要远程登录的用户权限了。

### 4.授权root用户进行远程登录

输入命令：

```bash
mysql> ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'root_pwd'; ## 授权root远程登录 后面的root_pwd代表登录密码
```

输入完之后，看到**Query OK**，说明执行成功！

> ==**说明**：此命令可以授权任何在mysql数据库user表中的用户以远程登录的方式访问数据库，本例中以'root'作为举例，若想授权其他用户，只需修改'root'的值为指定用户即可，'root_pwd'为'root'用户对应的登录密码，可以修改为你想要授权用户的登录密码。==

### 5.启动本地Navicat连接

打开Navicat客户端，新建mysql连接

 ![image-20220110220134967](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220110220135.png)

输入相关信息：

 ![image-20220110220302976](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220110220303.png)

如果显示连接成功了，那么恭喜你，可以进行远程操作数据库了



> ==如果显示2003错误，无法连接上数据库，请继续看下面的操作==

## 二、解决无法连接问题（2003）

### 1、首先确定防火墙放行3306端口

 ![image-20220110221904630](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220110221904.png)

### 2、确定防火请是否启动

> ==未启动==

```bash
[root@centos7 ~]#  firewall-cmd  --zone=public  --add-port=3306/tcp      --permanent
FirewallD is not running

[root@centos7 ~]# systemctl status firewalld 
● firewalld.service - firewalld - dynamic firewall daemon
Loaded: loaded (/usr/lib/systemd/system/firewalld.service; disabled; vendor preset: enabled)
Active: inactive (dead) #表示防火强未启动
Docs: man:firewalld(1)
```

> ==已启动==

```bash
[root@centos7 ~]# systemctl start firewalld 

[root@centos7 ~]# systemctl  status  firewalld 
● firewalld.service - firewalld - dynamic firewall daemon
Loaded: loaded (/usr/lib/systemd/system/firewalld.service; disabled; vendor preset: enabled)
Active: active (running) since Sun 2021-03-07 20:57:40 CST; 9s ago #active (running)表示防火墙已启动
Docs: man:firewalld(1)
Main PID: 29918 (firewalld)
CGroup: /system.slice/firewalld.service
└─29918 /usr/bin/python2 -Es /usr/sbin/firewalld --nofork --nopid
```



 ![image-20220110222142822](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220110222142.png)

### 3、放通防火墙

```bash
[root@centos7 ~]#  firewall-cmd  --zone=public  --add-port=3306/tcp      --permanent
success
```

### 4、重新添加防火墙规则

```bash
[root@centos7 ~]# firewall-cmd --permanent --add-port=3305/tcp
success
[root@centos7 ~]# firewall-cmd --reload 
success
```

> ==然后继续使用Navicat来连接即可==

