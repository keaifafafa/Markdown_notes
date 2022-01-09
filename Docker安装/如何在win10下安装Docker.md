## 一、什么是Docker？

 ![image-20211226115907177](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226115914.png)

Docker 是一个开源的应用容器引擎，基于 [Go 语言](https://www.runoob.com/go/go-tutorial.html) 并遵从 Apache2.0 协议开源。

Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。

容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）,更重要的是容器性能开销极低。

Docker 从 17.03 版本之后分为 CE（Community Edition: 社区版） 和 EE（Enterprise Edition: 企业版），我们用社区版就可以了

## 二、Docker的优点？

Docker 是一个用于开发，交付和运行应用程序的开放平台。Docker 使您能够将应用程序与基础架构分开，从而可以快速交付软件。借助 Docker，您可以与管理应用程序相同的方式来管理基础架构。通过利用 Docker 的方法来快速交付，测试和部署代码，您可以大大减少编写代码和在生产环境中运行代码之间的延迟。

### 1、快速，一致地交付您的应用程序

Docker 允许开发人员使用您提供的应用程序或服务的本地容器在标准化环境中工作，从而简化了开发的生命周期。

容器非常适合持续集成和持续交付（CI / CD）工作流程，请考虑以下示例方案：

- 您的开发人员在本地编写代码，并使用 Docker 容器与同事共享他们的工作。
- 他们使用 Docker 将其应用程序推送到测试环境中，并执行自动或手动测试。
- 当开发人员发现错误时，他们可以在开发环境中对其进行修复，然后将其重新部署到测试环境中，以进行测试和验证。
- 测试完成后，将修补程序推送给生产环境，就像将更新的镜像推送到生产环境一样简单。

### 2、响应式部署和扩展

Docker 是基于容器的平台，允许高度可移植的工作负载。Docker 容器可以在开发人员的本机上，数据中心的物理或虚拟机上，云服务上或混合环境中运行。

Docker 的可移植性和轻量级的特性，还可以使您轻松地完成动态管理的工作负担，并根据业务需求指示，实时扩展或拆除应用程序和服务。

### 3、在同一硬件上运行更多工作负载

Docker 轻巧快速。它为基于虚拟机管理程序的虚拟机提供了可行、经济、高效的替代方案，因此您可以利用更多的计算能力来实现业务目标。Docker 非常适合于高密度环境以及中小型部署，而您可以用更少的资源做更多的事情。

## 三、如何在Win10下安装Docker？

> ==建议直接升级为专业版（淘宝花几块钱买激活码即可）==

Docker Desktop 是 Docker 在 Windows 10 和 macOS 操作系统上的官方安装方式，这个方法依然属于先在虚拟机中安装 Linux 然后再安装 Docker 的方法。

Docker Desktop 官方下载地址： https://hub.docker.com/editions/community/docker-ce-desktop-windows

**注意：**此方法仅适用于 Windows 10 操作系统专业版、企业版、教育版和部分家庭版！

### 1、安装 Hyper-V

Hyper-V 是微软开发的虚拟机，类似于 VMWare 或 VirtualBox，仅适用于 Windows 10。这是 Docker Desktop for Windows 所使用的虚拟机。

但是，这个虚拟机一旦启用，QEMU、VirtualBox 或 VMWare Workstation 15 及以下版本将无法使用！如果你必须在电脑上使用其他虚拟机（例如开发 Android 应用必须使用的模拟器），请不要使用 Hyper-V！

### 2、开启 Hyper-V

 ![img](https://www.runoob.com/wp-content/uploads/2017/12/1513668234-4363-20171206211136409-1609350099.png)

程序和功能

 ![img](https://www.runoob.com/wp-content/uploads/2017/12/1513668234-4368-20171206211345066-1430601107.png)

启用或关闭Windows功能

 ![img](https://www.runoob.com/wp-content/uploads/2017/12/1513668234-9748-20171206211435534-1499766232.png)

选中Hyper-V

 ![img](https://www.runoob.com/wp-content/uploads/2017/12/1513668234-6433-20171206211858191-1177002365.png)

最后重启电脑即可！

### 3、安装 Docker Desktop for Windows

Docker下载地址为：https://store.docker.com/editions/community/docker-ce-desktop-windows 点击如图处即可下载安装包：

 ![image-20211226120847551](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226120847.png)

下载完成后运行安装包，安装完成后界面如图：

 ![image-20211226121022481](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226121022.png)

单击Close and log out，这个时候我们重启一次电脑

### 4、安装Docker Desktop报错WSL 2 installation is incomplete.

> ==如果你安装的时候会有这个错误的话，需要作如下操作，没有的话直接跳过此步骤即可==

 ![image-20211226121503259](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226121503.png)

根据报错提示,猜测可能是我们使用的wsl2版本老了,需要我们自己手动更新一下,我们根据提示去微软官网下载最新版的wsl2安装后即可正常打开。
[更新包下载链接](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)。

## 四、启动Docker

1、在桌面找到Docker for Windows快捷方式，双击启动即可！启动成功后托盘处会有一个小鲸鱼的图标。打开命令行输入命令：docker version可以查看当前docker版本号，如图：

 ![image-20211226121201748](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226121202.png)

2、更换镜像源地址
中国官方镜像源地址为：https://registry.docker-cn.com、http://f1361db2.m.daocloud.io

 ![image-20211226121602530](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226121602.png)

 添加如下内容

```json
{
    "builder": {
        "gc": {
            "defaultKeepStorage": "20GB",
            "enabled": true
        }
    },
    "experimental": false,
    "features": {
        "buildkit": true
    },
    "registry-mirrors": [
        "https://registry.docker-cn.com"
    ]
}
```



![image-20211226121700846](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226121700.png)

点击Apply后会重启Docker。

3、载入测试镜像测试

输入命名“docker run hello-world”可以加载测试镜像来测试。如图：

 ![image-20211226121910450](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211226121910.png)

恭喜，这样即表示安装成功了！

## 写在最后

当然有可能会造成15.5版本以下的VMware无法启动，所以如果想继续使用VMware的话，需要更新自己的版本！具体如何卸载更新VMware   

可以参考这篇博客

**[Win10下如何正确卸载VMware](https://blog.csdn.net/a648119398/article/details/122154085)**

