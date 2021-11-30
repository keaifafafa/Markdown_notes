# Xshell如何通过SSH方式连接Kali

## 1、允许root用户登录sshd服务

> 输入如下代码

```linux
 vim /etc/ssh/sshd_config
```

然后会出现如下界面

修改以下内容第32行和第37行

![001](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210911180343.jpeg)

把32行的 "prohibit-password" 改为 "yes" 并把把32行 和37行前的"#"号删掉，改完效果如下图：

![002](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210911180520.jpeg)

> 重启ssh服务：

root@xuegod53:~# /etc/init.d/ssh restart

[ ok ] Restarting ssh (via systemctl): ssh.service.

配置sshd服务开机自动启动：

root@xuegod53:/etc/init.d# update-rc.d ssh enable

## 2、使用xshell连接Kali

查看kali IP地址是多少  可以使用**ifconfig** 或者 **ip a**

root@xuegod53:~# ifconfig

![003](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210911180706.jpeg)

我们回到windows上配置xshell![004](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210911180724.jpeg)

输入名称和ip地址![005](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210911180743.jpeg)

配置终端模式![006](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210911180802.jpeg)

输入用户名![008](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210911180819.png)

输入密码![009](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210911180846.jpeg)

![011](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210911180912.jpeg)

最后点击确定即可远程连接到Kali