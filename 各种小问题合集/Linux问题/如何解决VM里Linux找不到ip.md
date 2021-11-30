# 如何解决VM里Linux找不到ip

## 1、概述

- 由于最近在学习网络安全，所以在VM虚拟机里下载并安装了Kali(攻击机)和OWASP（靶机）

- 本来一切都很好，用来一个星期没有任何问题

- 突然有一天就不行了，结果如下图，而且无法上网，这是OWASP的图，Kali里也是一样的结果

  ![20190304211534787](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210903175246.png)

## 2、解决办法

> ==打开任务管理器（ctrl + shift + esc）==

![image-20210903175710014](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210903175710.png)

> ==打开服务==

![image-20210903175818611](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210903175818.png)

> ==把启动类型改为自动==

![image-20210903175951815](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210903175951.png)

目前这个问题算是暂时解决了，可以查到ip并上网了，不过我发现重启以后，那四个中的其中两个就又会自动关闭

> ==解决重启DHCP服务自动关闭的问题==

- 首先打开cmd

- 然后我们先后输入两条修复指令

  netsh winsock reset按回车

  netsh winhttp reset proxy按回车

  ![efb861bd4c7c34b35b92cd085841037de037316a](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210903180437.jpg)

然后重启电脑即可！