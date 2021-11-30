## 温馨提示

仅供参考，不建议小白在本机测试，不然会有需要 **重装** 的风险

## 测试环境

- win10家庭版
- AMD主板

## 实验案例

将路径C:\Users\名字改为C:\Users\name。（例如将中文名称改为英文名称）
这里名字代表原名称，name代表新名称。

## 操作步骤

1、Win+R打开命令窗口，输入regedit，打开注册表，ctrl+f（搜索），找到ProfileList，或者自行定位到HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\ProfileList，在这个目录下面有几个S-1-5-的项，挨个检查每一项，找到ProfileListPath项，看它后面的数据值是不是为C:\Users\名字，若是，右键修改，将“名字”改为“name”。点击确认，关闭注册表。

![image-20210827130214695](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210827130214.png)

2、（此时去C:\Users目录下是不能修改名称的），重启电脑，注意此时重启电脑后桌面会变成第一次使用的亚子（很丑，类似刚激活的样子），许多网上教程到这一步便结束了，不用担心。我们现在去C:\Users下去修改名字，右键要修改的文件夹，这时候会出现重命名选项，将名字改为name，确认后再次重启电脑，重启后电脑就会恢复原来的亚子。

3、很多程序的配置文件路径还是原来的中文名C:\Users\名字，所以打开它们会出现路径不存在的错误，此时不用担心，我们需要在C:\Users文件夹下创建一个快捷方式，具体操作如下：找到cmd.exe（C:\Windows\System32），右键以管理员身份运行，执行命令MKLINK /J C:\Users\名字 C:\Users\name，然后回车，注意：（电脑不同，该命令的大小写不同可能会报错，多试几种，注意大小写中英文符号），/J的意思就是将路径为C:\Users\名字的链接全部赋给C:\Users\name。这时候无论访问C:\Users\名字还是C:\Users\name都将跳转到C:\Users\name。这时候就完全OK啦！!

![1](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210827130835.png)

![image-20210827130921136](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210827130921.png)

## 可能出现一些问题

当然我自己这样做了以后，还出现了一些问题，比如QQ截图无法直接保存到桌面，需要提供管理员权限，桌面无法创建txt等文件，只能创建文件夹等，具体可以参考如下链接解决https://blog.csdn.net/a648119398/article/details/119950286

