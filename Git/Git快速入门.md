## 1、为什么要使用Git

学习git之前，我们需要先明白一个概念

**版本控制！**

> ==什么是版本控制==

版本控制（Revision control）是一种在开发的过程中用于管理我们对文件、目录或工程等内容的修改历史，方便查看更改历史记录，备份以便恢复以前的版本的软件工程技术。

- 实现跨区域多人协同开发
- 追踪和记载一个或者多个文件的历史记录
- 组织和保护你的源代码和文档
- 统计工作量
- 并行开发、提高开发效率
- 跟踪记录整个软件的开发过程
- 减轻开发人员的负担，节省时间，同时降低人为错误

简单说就是用于管理多人协同开发项目的技术。

没有进行版本控制或者版本控制本身缺乏正确的流程管理，在软件开发过程中将会引入很多问题，如软件代码的一致性、软件内容的冗余、软件过程的事物性、软件开发过程中的并发性、软件源代码的安全性，以及软件的整合等问题。

无论是工作还是学习，或者是自己做笔记，都经历过这样一个阶段！我们就迫切需要一个版本控制工具！

**多人开发就必须要使用版本控制！**

## 2、Git环境配置

> ==软件下载==

打开 [git官网] https://git-scm.com/，下载git对应操作系统的版本。

所有东西下载慢的话就可以去找镜像！

官网下载太慢，我们可以使用淘宝镜像下载：http://npm.taobao.org/mirrors/git-for-windows/

![image-20210927203559783](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927203607.png)

下载对应的版本即可安装！

安装：无脑下一步即可！安装完毕就可以使用了！

> ==启动Git==

安装成功后在开始菜单中会有Git的三个程序！

![image-20210927203658409](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927203658.png)

**Git Bash：**Unix与Linux风格的命令行，使用最多，推荐最多

**Git CMD：**Windows风格的命令行

**Git GUI**：图形界面的Git，不建议初学者使用，尽量先熟悉常用命令



> ==常用LInux命令==

平时一定要多使用这些基础的命令！

1）、cd : 改变目录。

2）、cd . . 回退到上一个目录，直接cd进入默认目录

3）、pwd : 显示当前所在的目录路径。

4）、ls(ll):  都是列出当前目录中的所有文件，只不过ll(两个ll)列出的内容更为详细。

5）、touch : 新建一个文件 如 touch index.js 就会在当前目录下新建一个index.js文件。

6）、rm:  删除一个文件, rm index.js 就会把index.js文件删除。

7）、mkdir:  新建一个目录,就是新建一个文件夹。

8）、rm -r :  删除一个文件夹, rm -r src 删除src目录

```linux
rm -rf / 切勿在Linux中尝试！删除电脑中全部文件！
```

9）、mv 移动文件, mv index.html src index.html 是我们要移动的文件, src 是目标文件夹,当然, 这样写,必须保证文件和目标文件夹在同一目录下。

10）、reset 重新初始化终端/清屏。

11）、clear 清屏。

12）、history 查看命令历史。

13）、help 帮助。

14）、exit 退出。

15）、#表示注释

> ==Git配置==

所有的配置文件，其实都保存在本地！

查看配置 git config -l

![image-20210927204121887](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927204121.png)

查看不同级别的配置文件：

```cmd
#查看系统config
git config --system --list
　　
#查看当前用户（global）配置
git config --global  --list
```

**Git相关的配置文件：**

1）、Git\etc\gitconfig  ：Git 安装目录下的 gitconfig   --system 系统级

2）、C:\Users\Administrator\ .gitconfig   只适用于当前登录用户的配置  --global 全局

![image-20210927204354106](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927204354.png)

这里可以直接编辑配置文件，通过命令设置后会响应到这里。

> ==设置用户名和邮箱（用户标识，必要）==

当你安装Git后首先要做的事情是设置你的用户名称和e-mail地址。这是非常重要的，因为每次Git提交都会使用该信息。它被永远的嵌入到了你的提交中：

```cmd
git config --global user.name "Sire"  #名称
git config --global user.email 648119398@qq.com   #邮箱
```

只需要做一次这个设置，如果你传递了--global 选项，因为Git将总是会使用该信息来处理你在系统中所做的一切操作。如果你希望在一个特定的项目中使用不同的名称或e-mail地址，你可以在该项目中运行该命令而不要--global选项。总之--global为全局配置，不加为某个项目的特定配置。

![image-20210927212553049](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927212554.png)

## 3、Git的基本理论（重点）

> ==三个区域==

Git本地有三个工作区域：工作目录（Working Directory）、暂存区(Stage/Index)、资源库(Repository或Git Directory)。如果在加上远程的git仓库(Remote Directory)就可以分为四个工作区域。文件在这四个区域之间的转换关系如下：

![image-20210927212700493](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927212700.png)

- Workspace：工作区，就是你平时存放项目代码的地方
- Index / Stage：暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列表信息
- Repository：仓库区（或本地仓库），就是安全存放数据的位置，这里面有你提交到所有版本的数据。其中HEAD指向最新放入仓库的版本
- Remote：远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据交换

本地的三个区域确切的说应该是git仓库中HEAD指向的版本：

![image-20210927212901565](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927212901.png)

- Directory：使用Git管理的一个目录，也就是一个仓库，包含我们的工作空间和Git的管理空间。
- WorkSpace：需要通过Git进行版本控制的目录和文件，这些目录和文件组成了工作空间。
- .git：存放Git管理信息的目录，初始化仓库的时候自动创建。
- Index/Stage：暂存区，或者叫待提交更新区，在提交进入repo之前，我们可以把所有的更新放在暂存区。
- Local Repo：本地仓库，一个存放在本地的版本库；HEAD会只是当前的开发分支（branch）。
- Stash：隐藏，是一个工作状态保存栈，用于保存/恢复WorkSpace中的临时状态。

> ==工作流程==

git的工作流程一般是这样的：

１、在工作目录中添加、修改文件；

２、将需要进行版本管理的文件放入暂存区域；

３、将暂存区域的文件提交到git仓库。

因此，git管理的文件有三种状态：已修改（modified）,已暂存（staged）,已提交(committed)

![image-20210927213041575](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927213041.png)

## 4、Git项目搭建

> ==创建工作目录与常用指令==

工作目录（WorkSpace)一般就是你希望Git帮助你管理的文件夹，可以是你项目的目录，也可以是一个空目录，建议不要有中文。

日常使用只要记住下图6个命令：

![image-20210927213139622](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927213139.png)

> ==本地仓库搭建==

创建本地仓库的方法有两种：一种是创建全新的仓库，另一种是克隆远程仓库。

1、创建全新的仓库，需要用GIT管理的项目的根目录执行：

 ```cmd
 # 在当前目录新建一个Git代码库
 $ git init
 ```

2、执行后可以看到，仅仅在项目目录多出了一个.git目录，关于版本等的所有信息都在这个目录里面。

![image-20210927213346325](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927213346.png)

> ==克隆远程仓库==

1、另一种方式是克隆远程目录，由于是将远程服务器上的仓库完全镜像一份至本地！

```cmd
# 克隆一个项目和它的整个代码历史(版本信息)
$ git clone [url]  # https://gitee.com/kuangstudy/openclass.git
```

2、去 gitee 或者 github 上克隆一个测试！

## 5、Git文件操作

> ==文件的四种状态==

版本控制就是对文件的版本控制，要对文件进行修改、提交等操作，首先要知道文件当前在什么状态，不然可能会提交了现在还不想提交的文件，或者要提交的文件没提交上。

- Untracked: 未跟踪, 此文件在文件夹中, 但并没有加入到git库, 不参与版本控制. 通过git add 状态变为Staged.
- Unmodify: 文件已经入库, 未修改, 即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为Modified. 如果使用git rm移出版本库, 则成为Untracked文件
- Modified: 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过git add可进入暂存staged状态, 使用git checkout 则丢弃修改过, 返回到unmodify状态, 这个git checkout即从库中取出文件, 覆盖当前修改 !
- Staged: 暂存状态. 执行git commit则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为Unmodify状态. 执行git reset HEAD filename取消暂存, 文件状态为Modified

> ==查看文件的状态==

上面说文件有4种状态，通过如下命令可以查看到文件的状态：

```cmd
#查看指定文件状态
git status [filename]

#查看所有文件状态
git status

# git add .                  添加所有文件到暂存区
# git commit -m "消息内容"    提交暂存区中的内容到本地仓库 -m 提交信息
```

> ==忽略文件==

有些时候我们不想把某些文件纳入版本控制中，比如数据库文件，临时文件，设计文件等

在主目录下建立".gitignore"文件，此文件有如下规则：

1. 忽略文件中的空行或以井号（#）开始的行将会被忽略。
2. 可以使用Linux通配符。例如：星号（*）代表任意多个字符，问号（？）代表一个字符，方括号（[abc]）代表可选字符范围，大括号（{string1,string2,...}）代表可选的字符串等。
3. 如果名称的最前面有一个感叹号（!），表示例外规则，将不被忽略。
4. 如果名称的最前面是一个路径分隔符（/），表示要忽略的文件在此目录下，而子目录中的文件不忽略。
5. 如果名称的最后面是一个路径分隔符（/），表示要忽略的是此目录下该名称的子目录，而非文件（默认文件或目录都忽略）。

```cmd
#为注释
*.txt        #忽略所有 .txt结尾的文件,这样的话上传就不会被选中！
!lib.txt     #但lib.txt除外
/temp        #仅忽略项目根目录下的TODO文件,不包括其它目录temp
build/       #忽略build/目录下的所有文件
doc/*.txt    #会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```

> ==.gitignore文件配置参考==

![gitidea的导入](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927214427.png)

![gitidea的导入2](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927214432.png)

## 6、使用Gitee(码云)测试

> ==github 是有墙的，比较慢，在国内的话，我们一般使用 gitee ，公司中有时候会搭建自己的gitlab服务器==

这个其实可以作为大家未来找工作的一个重要信息！

1、注册登录码云，完善个人信息

![image-20210927214719217](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927214719.png)

2、设置本机绑定SSH公钥，实现免密码登录！（免密码登录，这一步挺重要的，码云是远程仓库，我们是平时工作在本地仓库！)

- 进入 *C:\Users\Administrator\.ssh 目录* （）如果没有这个目录，请打开显示隐藏文件，如果还是没有，那就自己创建一个

- 生成公钥 ssh-keygen (在当前文件夹下打开git，输入如下命令)

  ```cmd
  ssh-keygen -t rsa
  ```

  ![23-3](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927215033.png)

- 打开并复制公钥

  ![image-20210927215250843](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927215250.png)

3、将公钥信息public key 添加到码云账户中即可！

![image-20210927215654791](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927215654.png)

4、使用码云创建一个自己的仓库！

![image-20210927215811432](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927215811.png)

> ==许可证：开源是否可以随意转载，开源但是不能商业使用，不能转载，...  限制！==

![image-20210927220236193](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927220236.png)

> ==克隆到本地！==

![image-20210927220405812](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927220405.png)

然后再本地的一个文件夹打开**Git**（随便一个文件夹就行）

![image-20210927220746164](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927220746.png)

打开克隆的远程仓库文件（检查下文件有没有错）

![image-20210927220833389](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927220833.png)

没错，可以进行下一步了！

## 7、IDEA中集成Git

1、新建项目，绑定git。

![image-20210927221009247](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927221009.png)

然后把复制的文件，粘贴到需要被托管的idea文件工程里（如下操作，仅供参考）

![image-20210927221346390](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927221346.png)

然后打开IDEA，观察项目的变化

![image-20210927221909889](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927221910.png)

2、修改文件，使用IDEA操作git。

- 添加到暂存区

  ![image-20210927222604308](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927222604.png)

- commit 提交

  点击 右边git 旁边 那个绿色 **对钩** 就会出现如下界面

  ![image-20210927222613006](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927222613.png)

- push到远程仓库

![image-20210927223257784](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927223257.png)

然后选择需要push的版本

![image-20210927223525658](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927223525.png)

最后看下结果

![image-20210927223639287](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927223639.png)

> ==温馨提示==

以上 这些 都是单个人的操作！

可能你照着我的做，你会遇到一些问题，因为有个别问题，我可能没讲解到位，毕竟环境变量这个东西，每个人的都不太一样，如果遇到问题，请自行百度。

## 8、Git分支(浅谈)

分支在GIT中相对较难，分支就是科幻电影里面的平行宇宙，如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过，在某个时间点，两个平行宇宙合并了，我们就需要处理一些问题了！

![image-20210927224034004](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927224034.png)

![image-20210927224047414](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927224047.png)

git分支中常用指令：

 ```cmd
 # 列出所有本地分支
 git branch
 
 # 列出所有远程分支
 git branch -r
 
 # 新建一个分支，但依然停留在当前分支
 git branch [branch-name]
 
 # 新建一个分支，并切换到该分支
 git checkout -b [branch]
 
 # 合并指定分支到当前分支
 $ git merge [branch]
 
 # 删除分支
 $ git branch -d [branch-name]
 
 # 删除远程分支
 $ git push origin --delete [branch-name]
 $ git branch -dr [remote/branch]
 ```

IDEA中操作

![image-20210927224230493](https://gitee.com/lovely-hair/blog-img/raw/master/img/20210927224230.png)



如果同一个文件在合并分支时都被修改了则会引起冲突：解决的办法是我们可以修改冲突文件后重新提交！选择要保留他的代码还是你的代码！

master主分支应该非常稳定，用来发布新版本，一般情况下不允许在上面工作，工作一般情况下在新建的dev分支上工作，工作完后，比如上要发布，或者说dev分支代码稳定后可以合并到主分支master上来。

