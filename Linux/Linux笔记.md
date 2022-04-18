## Linux命令

### 查询进程和结束进程

 1、ps -ef |grep redis

​		ps:将某个进程显示出来
​				-A 　显示所有程序。
​				-e 　此参数的效果和指定"A"参数相同。
​				-f 　显示[UID](https://www.baidu.com/s?wd=UID&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1dBm1uBmvF9uADYuAfzPHTY0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPW6sPjmLPWR1njDsrjRsn1Tz),PPIP,C与S[TIME](https://www.baidu.com/s?wd=TIME&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1dBm1uBmvF9uADYuAfzPHTY0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPW6sPjmLPWR1njDsrjRsn1Tz)栏位。
​				grep命令是查找	
​				中间的|是管道命令 是指ps命令与grep同时执行

​		这条命令的意思是显示有关redis有关的进程

2、kill [参数] [进程号]

 		 kill -9 4394 

​			kill就是给某个进程id发送了一个信号。默认发送的信号是SIGTERM，而kill -9发送的信号是SIGKILL，即exit。

​			exit信号不会被系统阻塞，所以kill -9能顺利杀掉进程。当然你也可以使用kill发送其他信号给进程

> 命令名

命令名严格区分大小写

**cd != CD**

> 回退到上一个用户

ctrl + D

> 强制删除文件夹

rm -rf 文件名 

r 代表递归删除【删除具体文件的时候，可以不带r】

 f 是强制的意思

> 区分大小写

> 隐藏文件

以 "."开头的为隐藏文件

查看命令

```bash
ll -a
ls -la
```

   ![image-20220314203152443](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220314203201.png)



> 查看大文件

more 

less是more的升级版

> 统计并输出文件的行数、单词数和字节数

可同时统计多个文件

wc

> 创建新文件或者修改文件时间戳

touch [-acmt] 文件名

> 查看文件的尾部

```bash
# -f 是刷新的意思，flush
tail -f /var/log/messages
```

## 文件所有者和属组

R【4】、W【2】、X【1】

## Vim

vim 用于文本编辑，而非文字排版

**vim工作模式可分为三种，即——命令模式，编辑模式，末行模式**

**1. 命令模式：**可以用vim加上任意一个已经存在或是想创建的文件名，如果系统还不存在该文件，就意味着创建文件，如果系统存在该文件，就意味着编辑该文件。此时就可以进入vim的默认模式—命令模式。此时vim等待输入正确的命令，键入的每一个字符都会当作命令来处理**。**

**2. 插入****模式：**在进入命令模式之后，按下a， i o等键可进入插入模式。进入插入模式后可以对文件进行编辑，左下角出现INSERT

a 在光标所在字符后插入

A在光标所在行尾插入

i 在光标所在字符前插入

I 在光标所在行行首插入

o 在光标下插入新行

O在光标上插入新行



**3.常用快捷键**

```bash
vim file1 file2 file3            可同时打开多个文件

【Esc】   从编辑模式退出到命令模式

 ：vsplit     显示多个文件    ctrl+w+方向键 切换窗口

 /关键字     匹配内容关键字

：行号     光标跳到指定行行首

：$             光标跳到最后一行行首

G              光标移动到最后一行

gg            光标移动到首行

：set un      在每行前加入行号

：wq          在命令模式下退出并保存

：q             文件 未做修改时退出

：q!            强制退出 ，不保存

y                  复制

yl                 复制一个字母

yw               复制一个单词

yy                复制一行

Y                 复制一行

c                 剪切（用法与y复制类似）

d                 删除  (用法与y复制类似）

p                 粘贴

u                 撤销

ctrl + r         恢复

2.字符的替换 （s行，g列）
:%s/源字符/替换字符                将每行出现的第一个源字符替换为目标字符
:%s/源字符/替换后字符/g         将全文源字符替换为目标字符
:8,10s/源字符/替换后字符/g     替换第八行到第十行的字符
：set nu       在每行前加入行号

： set nonu    取消行号

：set mouse=a  开启鼠标控制

：set hls    设置搜索高亮

： set guifont=monaco\10    设置字体

：set sursorline  标记当前所在行


```



## Shell的Test条件测试

```bash
# 查看是否存在
fname=`test -a a1b.txt && echo "Exists" || echo "Not"`
# 查看文件是否由内容
fname=`test -s a1b.txt && echo "Exists" || echo "Not"`
# 执行
echo $fname
```

## Shell的流程语句

> shell程序中的操作默认都是字符串操作，在要运行数学运算符的时候可能得到意想不到的答案

$ 是取变量值的符号

- Shell (( ))双小括号：

  1、Shell(())是专门用来运算整数且**只能进行整数运算**，不能对小数、[浮点数](https://so.csdn.net/so/search?q=浮点数&spm=1001.2101.3001.7020)或字符串进行运算。

  2、**其是let "num++" 的简写， 可以简写为 ((num++)), 所以 while 后面跟的是 (()), for 也是同样的道理**

  

- ***Shell [[ ]] 双中括号：***
  1、[[ ]]不是一个命令，是bash里面的一个关键字。
  2、支持[字符串](https://so.csdn.net/so/search?q=字符串&spm=1001.2101.3001.7020)的模式匹配。

    ![image-20220401171319564](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220401171327.png)

  3、使用[[…]]作为条件判断结构。&&、||、<、>等都可以正常存在于[[]]中，但是，出现在[ ]中，会报错。

   ![image-20220401171347901](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220401171347.png)

### 选择语句

需要注意空格，严格识别空格的

" [ $a == $b ] "里是需要加空格的，开头和结尾， " （( $a == $b )）" 也是一样的

```bash
#!/bin/bash
# 输出最大
a=10
b=20
if [ $a == $b ]
then
  echo "a 等于 b"
elif [ $a -gt $b ]
then
  echo "a 大于 b"
elif [ $a -lt $b ]
then
  echo "a 小于 b"
else
  echo "没有符合的条件"
fi
```



### 循环语句

作业：做个菱形脚本

> ==中间含空格的菱形==

```bash
#!/bin/bash
# 打印菱形
`stty erase '^H'`
# -p prompt:设置提示信息
# -t timeout 设置输入等待时间，单位默认为秒
read -p "请输入层数：" num
# 先打印正半部分
for (( i=1; i<=$num; i++ ))
do
    # 打印空格
    for (( j=$num; j>=i; j-- ))
    do
        # -n 代表不换行
	echo -n " "
    done
    for (( k=1; k<=i; k++ ))
    do
        # -n 代表不换行，在同一行
        echo -n " *"
    done
    # 换行
    echo
done
# 打印下半部分，思想同上
for (( i=1; i<$num; i++ ))
do
    for (( j=0; j<=i; j++))
    do
        echo -n " "
    done
    for (( k=$num-1; k>=i; k--))
    do
	echo -n " *"
    done
    echo
done

```

 ![image-20220401171912854](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220401171912.png)

> ==中间没有空格的菱形==

```bash
# !/bin/bash
# 打印菱形
`stty erase '^H'`
read -p "请输入层数：" num 
# 先打印正半部分
for (( i=0; i<num; i++ ))
do
    # 打印空格
    for (( j=num-1; j>=i; j-- ))
    do  
        # -n 代表不换行
        echo -n " "
    done
    # 算法核心公式：每行的星号数 =  2 * i + 1
    for (( k=1; k<=(2*i+1); k++ ))
    do  
        # -n 代表不换行，在同一行
        echo -n "*"
    done
    # 换行
    echo
done
# 打印下半部分，思想同上
for (( i=num-2; i>=0; i-- ))
do
    for (( j=num-1; j>=i; j--))
    do  
        echo -n " "
    done
    for (( k=1; k<=(2*i+1); k++))
    do  
        echo -n "*"
    done
    echo
done
```

 ![image-20220401171951057](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220401171951.png)

## Shell的函数



## 网络配置

图形化

```bash
# 先安装
systemctl start NetworkManager
# 网络编辑界面
nmtui
# 该命令可以完成网卡上所有的配置工作，并且可以写入配置文件，永久生效。
nmcli
# 查看firewalld状态
firewall-cmd --state
# 添加服务
firewall-cmd --add-service=http

```

- 桥接模式下的虚拟机是独立于主机的【也就是暴露在互联网中】
- NAT是在，主机可访问虚拟机
- 仅主机，主机不可访问虚拟机

## Hadoop

