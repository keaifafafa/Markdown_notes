## EL表达式显示错误expression expected问题：

![1622824211398](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210827124210.png)

  这段代码在MyEclipse中没有问题，因为idea的严格代码检查，这里会显示expression expected的错误，原因是因为js的函数无法识别参数是什么类型的值，El表达式得到的值有可能是数字，也有可能是字符串，我们需要**用单引号将EL表达式包起来**就可以了。 

