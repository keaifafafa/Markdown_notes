# IO流学习

## 1. IO_File

### 1.1 快速入门

- 将客户的需求转换成代码 更多的去关注功能
- 一切以程序为中心
- 5个类和三个接口
- 文件拷贝(视频上传，下载)
- 字节流，字符流
- 学习方法：二八法则，量变到质变

### 1.2 File类

工具类里的方法一般都是静态的

```java
//1.建议这样写，便于跨平台 比如Linux
// path 建议用 "/"  比如 path = "D:/soft/workspace/IO_Study01/io.jpg"
//2.常量拼接
// path = "D:"+File.separator+"soft"+File.separator+"workspace"+File.separator+
```

### 1.3 名称或路径

部分File方法   更多方法请查看API

```java
String path = "D:/soft/workspace/IO_Study01/io.jpg";   //这是绝对路径
String path2 = "io.jpg";   //这是相对路径
System.out.println(System.getProperty("user.dir")); //获取当前文件的路径
File src = new File(path);
System.out.println(src.getAbsolutePath());   //获取绝对路径的方法
System.out.println("名称："+src.getName()); //获取名字
System.out.println("路径："+src.getPath()); //获取路径
System.out.println("绝对路径："+src.getAbsolutePath()); //获取绝对路径
System.out.println("父路径："+src.getParent()); //返回父路径，也就是"/"前面的
System.out.println("父对象："+src.getParentFile().getName()); //返回父对象
```

### 1.4 文件状态

- 不存在：exists

- 存在：1.文件：isFile

  ​			2.目录：isDirectory

```java
System.out.println("是否存在"+src.exists());
System.out.println("是否是文件"+src.isFile());
System.out.println("是否是文件夹"+src.isDirectory());
```

### 1.5 文件大小(长度)

关键字 length 

```java
System.out.println(src.length());  //可以查看文件的大小   文件夹的大小可以用递归实现
```

### 1.6 创建和删除文件

```java
boolean flag = src.createNewFile();  //创建原来不存在的文件(*.mp3等等)   不能创建文件夹
System.out.println(flag);
flag = src.delete();  //删除已经创建好的文件
System.out.println(flag);
//补充：con con3.....这种是操作系统的设备名字，不可以创建
```

### 1.7 创建文件夹

- mkdir：必须确保上级目录存在
- mkdirs：上级目录可以不存在，不存在的话，就把上级目录一起创建

### 1.8 列出下一级

1. list()：可以列出下级名称

   ```java
   String[] subNames = dir.list();   //数组
   //数组的遍历
   for(String s:subNames) {
       System.out.println(s);
   }
   ```

2. listFiles():列出下级File对象

   ```java
   //下级对象
   File[] subFiles = dir.listFiles();
   for(File n:subFiles) {
       System.out.println(n);
   }
   ```

3. listRoots(): 列出计算机所有盘符(了解)

   ```java
   //所有盘符(了解)
   File[] subroot = dir.listRoots();
   for(File r:subroot) {
       System.out.println(r.getAbsolutePath());
   }
   ```

### 1.9 递归打印文件夹目录(也就是 树 )

```java
//递归方法
public static void result(File dir,int level) {
    for(int i = 0; i < level; i++) {
        System.out.print("-");
    }
    //		level++;  //level是用来增加"-"数量的
    System.out.println(dir.getName());
    if(dir.isDirectory()) {		//递归体
        //			foreach循环
        File[] subNames = dir.listFiles();
        for(File s:subNames) {
            result(s,level+1);
        }
    }else if(null == dir || !dir.isDirectory()) {   //递归头
        return ;
    }
}
```

### 1.10 文件编码和解码

1. 编码（encode）：字符串 ---> 字节
2. 解码（decode）：字节--->字符串

```java
//编码
String src = "生命性命使命a";  //这里默认用的"GBK" 每个字占用两个字节  英文占用一个字节
System.out.println(src.length());
byte []s = src.getBytes();  //编码 对其进行转型，byte（字节）
//解码
String sss = new String(s,0,s.length,"gbk");
System.out.println(sss);
//出现乱码的情况
//1、字节数不够
sss = new String(s,0,s.length-2,"gbk");
System.out.println(sss);
//2.字符集不统一
sss = new String(s,0,s.length-2,"utf-8");
System.out.println(sss);
```

## 2.  IO流输入输出

 ![image-20220415115553433](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220416212558.png)

### 2.1 节点流 和 处理流

- <font color='red'>节点流</font>
  可以从或向一个特定的地方（节点）读写数据。
  如：FileReader、FileWriter、FileInputStream、FileOutputStream等文件进行处理的节点流。
- <font color='red'>处理流</font>
  是对一个已存在的流的连接和封装，通过所封装的流的功能调用实现数据读写。
  如BufferedReader。
  处理流的构造方法总是要带一个其他的流对象做参数。
  一个流对象经过其他流的多次包装，称为流的链接。
  BufferedImputStrean
  BufferedOutputStream
  BufferedReader
  BufferedWriter
-  ![image-20220415114511341](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220415114518.png)
-  ![image-20220415120102866](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220415120103.png)

### 2.2 节点流：四大抽象类

#### 2.2.0 概述

![1618146916886](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224549.png)

#### 2.2.1 InputStream(字节输入流)

```java
//1、创建源
File src = new File("abc.txt");
//2、选择流
InputStream is = null;
try {
    int temp = 0;
    is = new FileInputStream(src); //这里需要抛出下异常
    //3、读写操作
    while((temp = is.read()) != -1) {
        System.out.print((char)temp);
    }
} catch (Exception e) {
    // TODO: handle exception
    System.out.println("捕捉异常！");
}finally {
    try {
        //4.释放资源
        if (is == null) { //用到is在关闭，避免出现空指针现象
            is.close();
        } 
    } catch (Exception e2) {
        // TODO: handle exception
    }
}
```

#### 2.2.2 OutputStream(字节输出流)

```java
//1、创建源
File src = new File("target.txt");
//2、选择流
OutputStream target = null;
try {
    target = new FileOutputStream(src);
    String text = "IO Study is very easy!!!";
    //进行编码  因为是对字节流输出
    byte[] data = text.getBytes();
    //3、读写操作
    try {
        target.write(data,0,text.length());  //可以在后面加一个true 这样会追加内容  不然会默认覆盖
        //清除缓存
        target.flush();
    } catch (FileNotFoundException e) {
        // TODO Auto-generated catch block
        System.out.println("捕捉异常 FileNotFoundException e");
    }
} catch (IOException e) {
    // TODO: handle exception
    e.printStackTrace();
}finally {
    if(target != null) {
        try {//4、关闭资源
            target.close();
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }
}
```

#### 2.2.3 Reader （字符输入流）

```java
//2、选择流
Reader reader = null;
try {
    reader = new FileReader(src);
    char [] flush = new char[1024];
    int len = -1;
    //3、读写操作
    try {
        while((len = reader.read(flush)) != -1) {
            System.out.println(flush);
        }
    } catch (IOException e) {
        // TODO Auto-generated catch block
        e.printStackTrace();
    }
} 
```

#### 2.2.4 Writer（字符输出流）

```java
//2、选择源
Writer writer = null;
try {
    writer = new FileWriter(src);
    String content = "我是发发，我是孩子王！！！abc+++";
    //char datas[] = content.toCharArray(); //字符串---->字符数组
    //3、读写操作
    //writer.write(datas,0,datas.length); //方式一
    writer.write(content,0,content.length()); //方式二
    writer.flush();//清理缓存

}
```

### 2.3 处理流

#### 2.3.1     具体装饰流 字节缓冲流Buffered

```java
// 就是装饰FileInputStream  可以调高近五倍的效率
InputStream is = new BufferedInputStream(new FileInputStream(inPath));
```

![1618319388140](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224545.png)

 ![image-20220415120734513](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220415120734.png)

#### 2.3.1字符缓冲流

- BufferedReader

  ```java
   /* 字符缓冲流(只适用于纯文本的操作)
   * 尽量不要发生多态  因为子类新方法用不了 readline 读取一行文字(字符流)
   */
  BufferedReader reader = new BufferedReader(new FileReader(src));
  ```

- BufferedWriter

  ```java
  /**
   * 字符缓冲流(只适用于纯文本的操作)
   * 尽量不要发生多态  因为子类新方法用不了newLine() 写一行分隔符
   */
  BufferedWriter writer = new BufferedWriter(new FileWriter(src));
  ```

### 2.4 转换流(convert)

> 简介

- 转换流提供了在字节流和字符流之间的转换
- Java API提供了两个转换流：
- InputStreamReader：将InputStream转换为Reader
- OutputStreamWriter：将Writer转换为OutputStream
- 字节流中的数据都是字符时，转成字符流操作更高效。
- 很多时候我们使用转换流来处理文件乱码问题。实现编码和
- 解码的功能。

> 用法

 ![image-20220416172256522](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220416172303.png)

 ![image-20220416172309926](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220416172310.png)

 ![image-20220416172329697](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220416172329.png)

以字符流的形式 操作字节流(纯文本的)

指定字符集

```java
//案例一  操作System.in和System.out 
try(BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
    BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(System.out));){
    //从键盘循环输入获取  输入(exit) 就退出 
    String msg = "";
    while(!msg.equals("exit")) {
        msg = reader.readLine();//循环读取
        writer.write(msg); //循环写入
        writer.newLine(); //换行
        writer.flush();//强制刷新一下  
    } 	
}catch(IOException e) {
    System.out.println("输出异常！");
}
//案例二  读取百度源代码，并下载下来
try (    BufferedReader reader = 
     new BufferedReader(
         new InputStreamReader(
             new URL("https://www.baidu.com").openStream(), "UTF-8"));
     BufferedWriter writer =
     new BufferedWriter(
         new OutputStreamWriter(
             new FileOutputStream("baidu.txt"),"UTF-8"));){
    //读写操作
    String msg;
    while((msg=reader.readLine())!= null) {
        writer.write(msg);
    }
    writer.flush();//清除缓存·
}
```

### 2.5 数据流（了解）

 ![image-20220416175825978](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220416175826.png)

```java
//先写输入流   字节数组流不用处理异常
ByteArrayOutputStream baos = new ByteArrayOutputStream();
DataOutputStream dos = new DataOutputStream(new BufferedOutputStream(baos));
//DataOutputStream dos = new DataOutputStream(new BufferedOutputStream(new ByteArrayOutputStream()));//不要这样写，这样就无法操作字符数组了
//操作数据类型+数据
dos.writeUTF("编程辛酸泪");//写入字符串
dos.writeInt(18);//写入整型数据
dos.writeBoolean(true);//写入布尔型数据
dos.writeChar('S');//写入字符
dos.flush();//强制刷新一下
byte [] datas = baos.toByteArray(); //接收数据
System.out.println(datas.length);//可以查看字节数组的大小
//读取
DataInputStream dis = new DataInputStream(new BufferedInputStream(new ByteArrayInputStream(datas)));
//读取的顺序要和写入的顺序保持一致
String msg = dis.readUTF();
int age = dis.readInt();
Boolean flag = dis.readBoolean();
char Char = dis.readChar();
System.out.println(age);
```

### 2.6 对象流

   ![1618583711294](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224527.png)

> 简介

 ![image-20220416181417689](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220416181452.png)

> java对象的序列化

 ![image-20220416181452134](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220416181452.png)

 ![image-20220416181929636](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220416181929.png)

 ![image-20220418155419982](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220418155420.png)

> 思考

 ![image-20220418155403503](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220418155412.png)

> 代码演示

```java
/* 对象流 ObjectInputStream ObjectOutputStream
 * 和数据流操作很相似(可用于引用数据类型)
 * 先写入后读取   Serializable 序列化 Deserializable 反序列化
 * 不是所有的对象都可以进行序列化(需要实现 Serializable 序列化接口)*/
ObjectOutputStream oos = new ObjectOutputStream(new BufferedOutputStream(new FileOutputStream("obj.txt")));
//操作数据类型+数据
oos.writeUTF("编程辛酸泪");//写入字符串
oos.writeInt(18);//写入整型数据
oos.writeBoolean(true);//写入布尔型数据
oos.writeChar('S');//写入字符
///////////////////////////////////////////////////////////////
oos.writeObject("谁解其中味");
oos.writeObject(new Date());
oos.writeObject(new Employee("比尔盖茨",1000));
oos.flush();//强制刷新一下
oos.close();
//读取
ObjectInputStream ois = new ObjectInputStream(new BufferedInputStream(new FileInputStream("obj.txt")));
//读取的顺序要和写入的顺序保持一致
String msg = ois.readUTF();
int age = ois.readInt();
Boolean flag = ois.readBoolean();
char Char = ois.readChar();
System.out.println(age);
///////////////////////////////////
//数据还原
Object str = ois.readObject();
Object date = ois.readObject();
Object emp = ois.readObject();
ois.close();
//进行比较
if(str instanceof String) {
    //进行强制转化
    String strObj = (String)str;
    System.out.println(strObj);
}
if(date instanceof Date) {
    //进行强制转化
    Date dateObj = (Date)date;
    System.out.println(dateObj);
}
if(emp instanceof Employee) {
    //进行强制转化
    Employee empObj = (Employee)emp;
    System.out.println(empObj.getName()+"-------->"+empObj.getSalary()+"亿元");
}
```



