## 写在前面

一般Linux系统都会自带JDK，只不过是Open JDk，而我们开发一般使用的是Oracle JDK，所以我们需要写在Open JDK，进而安装Oracle JDK

 ![image-20220418232100848](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220418232100.png)

## 一、卸载Open JDK

> ==一下操作需要在root权限下进行==

1、建议切换到root 账户

```bash
# 切换到root账户
su -
```

2、**查询系统是否以安装jdk**

```bash
rpm -qa|grep java
```

 ![image-20220418224602797](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220418224603.png)

3、**卸载已安装的jdk**

```bash
# 温馨提示，文件名仅供参考，具体以自己的为准
rpm -e --nodeps java-1.8.0-openjdk-1.8.0.161-2.b14.el7.x86_64
rpm -e --nodeps java-1.8.0-openjdk-headless-1.8.0.161-2.b14.el7.x86_64
```

4、验证一下是还有jdk

```bash
rpm -qa|grep java
java -version
```

 ![image-20220418224800793](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220418224800.png)



## 二、安装Oracle JDK

1. 首先下载一个Linux版本的JDK，建议下载JDK8，这里推荐一个可以快速下载的[镜像网站](http://www.codebaoku.com/jdk/jdk-index.html)，比在官网的龟速好太多了，建议收藏哦！！！

2. 首先将安装包复制到 Centos里，这里建议使用 Xftp，如果不懂使用，可以看我的另一篇博客 [传送门](https://blog.csdn.net/a648119398/article/details/123406682?spm=1001.2014.3001.5501)

    ![image-20220418225937811](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220418225939.png)

3. 然后解压 jdk压缩包

   ```bash
   # 小Tips：0jdk敲完 直接按tab就会自动补全了哦^_^
   tar -zxvf jdk-8u202-linux-x64.tar.gz
   ```

    ![image-20220418230449743](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220418230449.png)

4. 编辑/etc/profile文件，配置环境变量

   直接放最后即可

   ```bash
   # Set Java Envieonment
   # 只需要注意JAVA_HOME的路径改成自己的，剩下的就可以照着抄了
   export JAVA_HOME=/home/jsj/jdk1.8.0_202
   export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
   export PATH=$PATH:$JAVA_HOME/bin
   ```

    ![image-20220418231648587](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220418231648.png)

5. 生效profile

    ```bash
    source /etc/profile
    java -version
    ```

     ![image-20220418231437526](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220418231437.png)

## 结语

   创作不易，如果觉得对您有帮助的话，来个免费的赞呗！！！

 ![image-20220418231916802](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220418231916.png)