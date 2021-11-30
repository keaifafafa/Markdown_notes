## <font color='blue'>问题出现的原因</font>

本人原本是想更改 <font color='red'>**cmd**</font> 里的那个用户名的名称的

![image-20210827120407366](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210827120414.png)

结果改完就成了图中的结果了(说实话更改这个名字就够头疼的了，结果还出现这个问题。。。。)

## <font color='red'>解决办法</font>

1. 首先进入“本地策略组编辑器”

   - WIN + R ——> 输入 “gpedit.msc”  然后回车

   - 若显示无法找到，请进行如下操作，如果找到了，那就直接进行第二部即可

     - 首先创建批处理文件

       1. 由于这种情况桌面是无法创建txt文件的，所以可以在其他的文件夹，或者D盘里创建txt文件，创建完再复制到桌面（反正我是这样做的=_=）

       2. 创建完 将以下内容复制到文档中<font color='red'>(注意保存的时候，字符编码设置为ANSI格式，不然程序无法执行！！！)</font>

          ```bat
          @echo off
          
          　　pushd "%~dp0"
          
          　　dir /b %systemroot%\Windows\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientExtensions-Package~3*.mum >gp.txt
          
          　　dir /b  %systemroot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientTools-Package~3*.mum >>gp.txt
          
          　　for /f %%i in ('findstr /i . gp.txt 2^>nul') do dism /online /norestart /add-package:"%systemroot%\servicing\Packages\%%i"
          
          　　pause
          ```

          ![image-20210827122033842](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210827122033.png)

       3. 将文件重命名为"gpedit.bat" 

          ![image-20210827121817408](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210827121817.png)

       4. 然后右键 以管理员身份运行

          ![image-20210827121913447](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210827121913.png)

       5. 重新执行"gpedit.msc"
          Win+R → 输入"gpedit.msc" → Enter 则出现"本地组策略"

          ![image-20210827122217261](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210827122217.png)

2. 进入本地策略编辑器,对如下两个策略进行 "**禁用**" 

   ![H@9ME7M9YXSJ@T}@PHFOSAH](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210827121358.png)

3. 最后重启即可！