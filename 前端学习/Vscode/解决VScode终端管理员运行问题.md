> ==问题==

就是在vscode里打开终端，输入命令会报错，如下图

![475401-20200119161713685-1043413891](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210922232524.png)



> ==解决方法==

- 以管理员身份打开PowerShell（按住shift不要松 然后右击桌面空白区域， 就可以看到打开PowerShell的选择项了）
- 打开后，输入get-ExecutionPolicy，回复Restricted，表示状态是禁止的
- 然后执行：set-ExecutionPolicy RemoteSigned
- 选择Y

注意：一定要以管理员的身份运行PowerShell，不是cmd窗口！

最后上过程图和效果图

![22-1](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210922232910.png)

![QQ截图20210922233311](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210922233506.png)
