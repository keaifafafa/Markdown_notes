# MyBatis

环境：

- JDK1.8
- Mysql5.7
- Maven3.6.1
- IDEA

回顾：

- JDBC
- Mysql
- Java基础
- Maven
- Junit

SSM框架:配置文件的。最好的方式：看官网文档

## 1、简介

### 1.1什么是MyBatis

 ![mybatis](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212555.jpg) 

**官网（有时候可能需要翻墙）**:https://mybatis.org/mybatis-3/zh/index.html

-  MyBatis 是一款**优秀的持久层框架**（Dao层）
- 它支持自定义 SQL、存储过程以及高级映射。
- MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。
- MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。 
-  MyBatis 本是apache的一个[开源项目](https://baike.baidu.com/item/开源项目/3406069)iBatis, 2010年这个[项目](https://baike.baidu.com/item/项目/477803)由apache software foundation 迁移到了[google code](https://baike.baidu.com/item/google code/2346604)，并且改名为MyBatis 。
- 2013年11月迁移到[Github](https://baike.baidu.com/item/Github/10145341)。 

如何获得Mybatis？

- maven仓库

  ```xml
  <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
  <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.2</version>
  </dependency>
  ```

  

- Github:

### 1.2、持久化

数据持久化

-  持久化就是将程序的数据在持久状态和瞬时状态转化的过程
- 内存：**断电即失**
- 数据库（JDBC），IO文件持久化
- 生活中：冷藏（冰箱），罐头

**为什么需要持久化？**

- 有一些对象，不能让他们丢掉(比如**会员账号，银行账户金额**等重要信息)
- 内存太贵了

### 1.3、持久层

Dao层，Service层，Controller层

- 完成持久化工作的代码块
- 层的界限十分明显

### 1.4、为什么需要Mybatis?
- 帮助程序员将数据存储到数据库中
- 方便
- 传统的JDBC代码太复杂了。简化。框架。自动化
- 不用Mybatis也可以。更容易上手。**技术没有高低之分**
- 优点：
  - 简单易学
  - 灵活。
  - 解除sql与程序代码的耦合
  - 提供映射标签，支持对象与数据库的orm字段关系映射
  - 提供对象关系映射标签，支持对象关系组建维护
  - 提供xml标签，支持编写动态sql

**最重要的一点：使用的人多！**

Spring 			SpringMVC		SpringBoot  SpringCloud

## 2、第一个Mybatis程序

思路：搭建环境-->导入Mybatis-->编写代码-->测试！

### 2.1、搭建环境

搭建数据库（使用工具是navicat）

```mysql
mysql> create database mybatis;
Query OK, 1 row affected
mysql> use mybatis;
Database changed
mysql> create table user(
    -> id int(20) not null primary key,
    -> name varchar(30) default null,
    -> pwd varchar(30) default null
    -> )engine=innodb default charset=utf8;
Query OK, 0 rows affected
mysql> insert into user(id,name,pwd) values
    -> (1,'发发','125555'),
    -> (2,'聪聪','124444'),
    -> (3,'可爱发','123333');
Query OK, 3 rows affected
Records: 3  Duplicates: 0  Warnings: 0
```

新建项目

1. 新建一个maven项目(普通的Maven项目，不用选任何模板)

2. 删除src目录

3. 导入Maven依赖

   ```xml
   <!--父工程-->
   <groupId>com.fafa</groupId>
   <artifactId>Mybatis-Study</artifactId>
   <version>1.0-SNAPSHOT</version>
   
   <!--导入依赖-->
   <dependencies>
       <!--mysql驱动-->
       <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <version>5.1.47</version>
       </dependency>
       <!--mybatis-->
       <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
       <dependency>
           <groupId>org.mybatis</groupId>
           <artifactId>mybatis</artifactId>
           <version>3.5.2</version>
       </dependency>
       <!--junit-->
       <dependency>
           <groupId>junit</groupId>
           <artifactId>junit</artifactId>
           <version>4.12</version>
       </dependency>
   </dependencies>
   ```

   

### 2.2、创建一个模块

1. 编写mybatis核心配置文件

   ![1626498686337](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212604.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE configuration
           PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-config.dtd">
   <!--mybatis核心配置文件-->
   <configuration>
       <!--这里的环境是复数，也就是可以配置多个在里面-->
       <environments default="development">
           <environment id="development">
               <transactionManager type="JDBC"/>
               <dataSource type="POOLED">
                   <property name="driver" value="com.mysql.jdbc.Driver"/>
                   <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=utf-8"/>
                   <property name="username" value="root"/>
                   <property name="password" value="root"/>
               </dataSource>
           </environment>
       </environments>
   
       <mappers>
           <mapper resource="org/mybatis/example/BlogMapper.xml"/>
       </mappers>
   </configuration>
   ```

   

2. 编写Mybatis工具类

   ```java
   //SqlSessionFactory -- > sqlSession
   public class MybatisUtils {
       //使用全局变量
       private static SqlSessionFactory sqlSessionFactory;
       static {
           try {
               //使用Mybatis第一步，获取sqlSessionFactory对象
               String resourse = "mybatis-config.xml";
               InputStream inputStream = Resources.getResourceAsStream(resourse);//注意Resources的包
               sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
           } catch (IOException e) {
               e.printStackTrace();
           }
       }
   
       //既然有了SqlSessionFactory，顾名思义，我们就可以从中获取SqlSession的实例了
       // SqlSession 完全包含了面向数据库执行 SQL 命令的所 有方法
       public static SqlSession getSqlSession(){
           return sqlSessionFactory.openSession();
       }
   }
   ```

### 2.3、编写代码

- 实体类

  ```java
  public class User {
      private int id;
      private String name;
      private String pwd;
  
      public User(int id, String name, String pwd) {
          this.id = id;
          this.name = name;
          this.pwd = pwd;
      }
  
      public int getId() {
          return id;
      }
  
      public void setId(int id) {
          this.id = id;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public String getPwd() {
          return pwd;
      }
  
      public void setPwd(String pwd) {
          this.pwd = pwd;
      }
  
      @Override
      public String toString() {
          return "{id=" + this.getId() + "，name='" + this.getName() + "'，pwd='" + this.getPwd() + "'}";
      }
  }
  
  ```

  

- Dao接口

  ```java
  public interface UserDao {
      List<User> getUserList();
  }
  ```

  

- 接口实现类

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <!--namespace=绑定一个对应的Dao/Mapper接口 -->
  <mapper namespace="com.fafa.dao.UserDao">
      <!--select查询语句-->
      <select id="getUserList" resultType="com.fafa.pojo.User">
          select * from mybatis.user;
      </select>
  
  </mapper>
  ```

  

### 2.4、测试（Junit）

注意点：org.apache.ibatis.binding.BindingException: Type interface com.fafa.dao.UserDao is not known to the MapperRegistry.

意思是Mapper未注册

解决方法：再Mapper的配置文件中加入这个

```xml
<!--注册Mapper的
        每一个Mapper.xml都需要在Mybatis核心配置文件中注册
-->
<mappers>
        <mapper resource="org/mybatis/example/BlogMapper.xml"/>
</mappers>
```

- Junit测试

  这里建议和java文件夹里的目录层次保持一致

  ![1626510218323](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212614.png)

  ```java
  public class UserDaoTest {
      @Test
      public void Test(){
          //获取SqlSession对象   静态方法是类 同时 加载的
          SqlSession sqlSession = null;
          try{
              sqlSession = MybatisUtils.getSqlSession();
              //方式一（推荐）   获取Dao/Mapper层对象  并进行查询操作
              UserDao mapper = sqlSession.getMapper(UserDao.class);
              List<User> userList = mapper.getUserList();
  
              //方式二  了解即可
              /*List<User> userList = sqlSession.selectList("com.fafa.dao.UserDao.getUserList");*/
  
              //对返回的结果进行遍历
              for (User user : userList) {
                  System.out.println(user.toString());
              }
          }catch(Exception e){
              System.out.println("捕捉到异常！");
          }finally {
              //关闭资源  防止内存溢出
              sqlSession.close();
          }
  
      }
  }
  
  ```

  

解决问题及总结

当完成上面的步骤后发现还是有错误

![1626510782626](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212617.png)

这个错误是Maven的问题，记得前面在javaweb的时候就说过，maven的约定大于配置的问题

解决方案有两种

- 第一种（很麻烦，不推荐）

  ![1626510947386](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212623.png)

- 第二种  在父工程的pom.xml或者子工程的pom.xml中添加这样一段Java代码

  ```xml
  <!--在build中配置resources，来防止我们资源导出失败的问题-->
  <build>
      <resources>
          <resource>
              <directory>src/main/resources</directory>
              <includes>
                  <include>**/*.properties</include>
                  <include>**/*.xml</include>
              </includes>
              <filtering>true</filtering>
          </resource>
          <resource>
              <directory>src/main/java</directory>
              <includes>
                  <include>**/*.properties</include>
                  <include>**/*.xml</include>
              </includes>
              <filtering>true</filtering>
          </resource>
      </resources>
  </build>
  ```

  

## 3、CRUD（增删改查）



### 3.1、namespace

namespace中的包名要和Dao/Mapper接口的包名字保持一致

### 3.2、select

选择，查询语句；

- id：就是对应namespace中的方法名
- resultType:sql语句执行的返回值
- parameterType：参数类型

1. 编写接口

   ```java
   //查询全部用户信息
   List<User> getUserList();
   ```

   

2. 编写对应的mapper中的sql语句

   ```xml
   <!--select查询语句-->
   <select id="getUserList" resultType="com.fafa.pojo.User">
       select * from mybatis.user;
   </select>
   ```

   

3. 测试

   ```java
   //查询全部用户
   @Test
   public void Test(){
       //获取SqlSession对象   静态方法是类 同时 加载的
       SqlSession sqlSession = null;
       try{
           sqlSession = MybatisUtils.getSqlSession();
           //方式一（推荐）   获取Dao/Mapper层对象  并进行查询操作
           UserMapper mapper = sqlSession.getMapper(UserMapper.class);
           List<User> userList = mapper.getUserList();
   
           //方式二  了解即可
           /*List<User> userList = sqlSession.selectList("com.fafa.dao.UserDao.getUserList");*/
   
           //对返回的结果进行遍历
           for (User user : userList) {
               System.out.println(user);
           }
       }catch(Exception e){
           System.out.println("捕捉到异常！");
       }finally {
           //关闭资源  防止内存溢出
           sqlSession.close();
       }
   }
   ```

### 3.3、insert

```xml
<!--插入用户-->
<insert id="addUser" parameterType="com.fafa.pojo.User">
    insert into mybatis.user(id,name,pwd) values (#{id},#{name},#{pwd});
</insert>

```

### 3.4、update

```xml
<!--更新用户信息
    里面的sql语句都不用加""  字符串也不要加 不然报错
    -->
<update id="updateUser" parameterType="com.fafa.pojo.User">
    update mybatis.user set name=#{name},pwd=#{pwd} where id=#{id};
</update>

```

### 3.5、delete

```xml
<!--删除用户-->
<delete id="deleteUser" parameterType="int">
    delete from mybatis.user where id=#{id};
</delete>
```

### 3.6、万能的Map

 假设，我们的实体类，或者数据库中的表，字段或者参数过多，我们应该考虑使用Map! 

1. UserMapper接口

   ```java
   //用万能Map插入用户
   public void addUser2(Map<String,Object> map);
   ```

2. UserMapper.xml

   ```xml
   <!--对象中的属性可以直接取出来 传递map的key-->
   <insert id="addUser2" parameterType="map">
       insert into user (id,name,password) values (#{userid},#{username},#{userpassword})
   </insert>
   ```

3. 测试

   ```java
   @Test
   public void test3(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
       UserMapper mapper = sqlSession.getMapper(UserMapper.class);
       HashMap<String, Object> map = new HashMap<String, Object>();
       map.put("userid",4);
       map.put("username","王虎");
       map.put("userpassword",789);
       mapper.addUser2(map);
       //提交事务
       sqlSession.commit();
       //关闭资源
       sqlSession.close();
   }
   ```

   

Map传递参数，直接在sql中取出key即可！ 【parameter=“map”】 

对象传递参数，直接在sql中取出对象的属性即可！ 【parameter=“Object”】 

只有一个基本类型参数的情况下，可以直接在sql中提取到！

多个参数用Map，或者**注解**！

### 3.7、模糊查询

 模糊查询这么写？ 

1.  Java代码执行的时候，传递通配符% % 

   ```java
   List<User> userList = mapper.getUserLike("%李%");
   ```

   

2.  在sql拼接中使用通配符 

   ```java
   select * from user where name like "%"#{value}"%"
   ```

   

## 4、配置解析

### 4.1、核心配置文件

- mybatis-config.xml
- Mybatis的配置文件包含了会深深影响Mybatis行为的设置和属性信息![1626574122559](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212632.png)

### 4.2、环境配置 environments

mybatis 可以配置成适应多种环境

**不过要记住：尽管可以配置成多个环境，但是每个SQLSessionFactory实例只能选择一种环境**

<font color='red'>学会使用配置多套运行环境！</font>

Mybatis默认的事务管理器就是JDBC，连接池：POOLED

### 4.3、属性properties

我们可以通过properties属性来实现引用配置文件

这些属性可以在外部进行配置，并可以进行动态替换。你既可以在典型的 Java 属性文件中配置这些属性，也可以在 properties 元素的子元素中设置。【db.properties】

1. 编写一个配置文件

   db.properties

   ```properties
   driver=com.mysql.jdbc.Driver
   url=jdbc:mysql://localhost:3306/mybatis?useSSL=false&useUnicode=true&characterEncoding=utf-8
   username=root
   password=root
   ```

   

2. 在核心配置文件中引入

   ```xml
   <!--引入外部资源-->
   <properties resource="db.properties"/>
   ```

   1. 可以直接引入外部文件
   2. 可以在其中增加一些属性配置
   3. 如果两个文件里有同一个字段，优先使用外部配置文件的

### 4.4、类别名 typeAliases

- 类别名可为Java类型设置一个缩写字段名字。它仅适用于XML配置

- 意在降低冗余的完全限定类名书写

  ```xml
  <!--给实体类取别名-->
  <typeAliases>
      <typeAlias type="com.fafa.pojo.User" alias="User"/>
  </typeAliases>
  ```

   也可以指定一个包，每一个在包<font color='red'> `domain.blog`</font> 中的 Java Bean，在没有注解的情况下，会使用 Bean 的首字母小写的非限定类名来作为它的别名。 比如`domain.blog.Author` 的别名为 `author`,；若有注解，则别名为其注解值。见下面的例子： 

  ```xml
  <typeAliases>
      <package name="com.fafa.pojo"/>
  </typeAliases>
  ```

  在实体类比较少的时候，使用第一种方式。

  如果实体类十分多，建议用第二种扫描包的方式。

  第一种可以DIY别名，第二种不行，如果非要改，需要在实体上增加注解

  ```java
  @Alias("author")
  public class Author {
      ...
  }
  ```

### 4.5、设置 Settings

这是Mybatis中极为重要的调整设置，他们会改变Mybatis的运行时行为。

 ![在这里插入图片描述](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212639.png) 

### 4.6、其他配置

- [typeHandlers（类型处理器）](https://mybatis.org/mybatis-3/zh/configuration.html#typeHandlers)
- [objectFactory（对象工厂）](https://mybatis.org/mybatis-3/zh/configuration.html#objectFactory)
- plugins 插件
  - mybatis-generator-core
  - mybatis-plus
  - 通用mapper

### 4.7、映射器 mappers

 MapperRegistry：注册绑定我们的Mapper文件； 

 方式一：【推荐使用】 

```xml
<!--每一个Mapper.xml都需要在MyBatis核心配置文件中注册-->
<mappers>
    <mapper resource="com/fafa/dao/UserMapper.xml"/>
</mappers>
```

 方式二：使用class文件绑定注册 

```xml
<!--每一个Mapper.xml都需要在MyBatis核心配置文件中注册-->
<mappers>
    <mapper class="com.fafa.dao.UserMapper"/>
</mappers>
```

**注意点：**

- 接口和他的Mapper配置文件必须同名
- 接口和他的Mapper配置文件必须在同一个包下

 方式三：使用包扫描进行注入 

```xml
<mappers>
    <package name="com.fafa.dao"/>
</mappers>
```

### 4.8、生命周期和作用域

![20200623164809990](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212644.png)

 声明周期和作用域是至关重要的，因为错误的使用会导致非常严重的**并发问题**。 

 **SqlSessionFactoryBuilder:** 

- 一旦创建了SqlSessionFactory，就不再需要他了
- 局部变量

**SqlSessionFactory:**

- 说白了可以想象为：数据库连接池
- SqlSessionFactory一旦被创建就应该在应用的运行期间一直存在，**没有任何理由丢弃它或者重新创建一个实例。**
- 因此SqlSessionFactory的最佳作用域是**应用作用域（ApplicationContext）**
- 最简单的就是使用**单例模式**或者**静态单例模式**

**SqlSession：**

- 连接到连接池的一个请求

- SqlSession的实例不是线程安全的，因此是不能共享的，所以他的最佳的作用域是请求或者方法作用域

- 用完之后需要赶紧关闭，否则资源被占用。

  ![2](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212649.png)

## 5、解决属性名和字段名不一致的问题

### 5.1、问题

数据库的字段

![1626615097031](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212654.png)

新建一个项目，拷贝之前的，测试实体类字段不一致的情况

```java
public class User {
    private int id;
    private String name;
    private String password;
    //无参构造
    public User() {

    }

    //含参构造
    public User(int id, String name, String password) {
        this.id = id;
        this.name = name;
        this.password = password;
    }


    @Override
    public String toString() {
        return "User{" +
            "id=" + id +
            "，name='" + name + '\'' +
            "'，password='" + password + '\'' +
            '}';
    }
}

```

测试出现问题（password的值为null）

![1626681751607](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212658.png)

```java
//select * from mybatis.user where id = #{id};
//类处理器
//select id,name,pwd from mybatis.user where id = #{id};
//类处理器是很笨的，不晓得变通，pwd和password不一致  上面的两句sql语句相等
```

解决方法：

- 起别名(最基本的，很low)

  ```xml
  <!--查询单个用户信息-->
  <select id="getUserById" parameterType="_int" resultType="User">
      select id,name,pwd as password from mybatis.user where id = #{id};
  </select>
  ```

### 5.2、ResultMap

结果集映射

```
id name pwd
id name password
```

```xml
<!--结果集映射-->
<resultMap id="resultMap" type="User">
    <!--
        column是数据库的字段
        property是实例类中的属性
        两者一一对应，形成映射关系
        -->
    <result column="id" property="id"/>
    <result column="name" property="name"/>
    <result column="pwd" property="password"/>
</resultMap>
<!--查询单个用户信息-->
<select id="getUserById" resultMap="resultMap">
    select * from mybatis.user where id = #{id};
</select>
```

![1626683422968](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212850.png)

- resultMap元素是Mybatis中最重要最强大的元素
- ResultMap的设计思想是，对于简单的语句做到零配置，对于复杂一点的语句,只需要描述语句之间的关系就行了
- ResultMap的优秀之处——在你做够了解他之后，你完全可以不用显示的配置他们
- 如果这个时间总是这么简单就好了。

## 6、日志

### 6.1、日志工厂

如果一个数据库操作出现了异常，我们需要排错。日志就是最好的助手。

曾经：sout，debug

现在：日志工厂

![1626744306803](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212709.png)

-  SLF4J 
- LOG4J (掌握)
- LOG4J2
- JDK_LOGGING
- COMMONS_LOGGING
- STDOUT_LOGGING(掌握)
- NO_LOGGING 

使用方法：

**严格按照顺序添加**

![1626744492175](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212716.png)

运行结果：

![1626744541739](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212721.png)

### 6.2、LOG4J

 什么是Log4j？ 

- Log4j是[Apache](https://baike.baidu.com/item/Apache/8512995)的一个开源项目，通过使用Log4j，我们可以控制日志信息输送的目的地是[控制台](https://baike.baidu.com/item/控制台/2438626)、文件、[GUI](https://baike.baidu.com/item/GUI)组件；
- 我们也可以控制每一条日志的输出格式；
- 通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程；
- 最令人感兴趣的就是，这些可以通过一个[配置文件](https://baike.baidu.com/item/配置文件/286550)来灵活地进行配置，而不需要修改应用的代码。

1. 先导入log4j的包

   ```xml
   <dependency>
       <groupId>log4j</groupId>
       <artifactId>log4j</artifactId>
       <version>1.2.17</version>
   </dependency>
   ```

   

2. log4j.properties(名字一定要是这个，不然找不到）![1626762540045](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212731.png)

   ```properties
   log4j.rootLogger=DEBUG,console,file
   
   #控制台输出的相关设置
   log4j.appender.console = org.apache.log4j.ConsoleAppender
   log4j.appender.console.Target = System.out
   log4j.appender.console.Threshold=DEBUG
   log4j.appender.console.layout = org.apache.log4j.PatternLayout
   log4j.appender.console.layout.ConversionPattern=[%c]-%m%n
   
   #文件输出的相关设置
   log4j.appender.file = org.apache.log4j.RollingFileAppender
   log4j.appender.file.File=./log/fafa.log
   log4j.appender.file.MaxFileSize=10mb
   log4j.appender.file.Threshold=DEBUG
   log4j.appender.file.layout=org.apache.log4j.PatternLayout
   log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n
   
   #日志输出级别
   log4j.logger.org.mybatis=DEBUG
   log4j.logger.java.sql=DEBUG
   log4j.logger.java.sql.Statement=DEBUG
   log4j.logger.java.sql.ResultSet=DEBUG
   log4j.logger.java.sql.PreparedStatement=DEBUG
   ```

   

3. 配置settings为log4j实现     ![1626762584837](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212738.png)

4. 测试运行

 **Log4j简单使用** 

1. 在要使用Log4j的类中，导入包 import org.apache.log4j.Logger;

2. 日志对象，参数为当前类的class对象

   ```java
   private static Logger logger = Logger.getLogger(UserMapper.class);
   ```

   

3. 日志级别

   ```java
   logger.info("Info:成功进入testLog4j()！");
   logger.debug("Debug:成功进入testLog4j()！");
   logger.error("Error:成功进入testLog4j()！");
   ```

   1. info
   2. debug
   3. error

## 7、分页

**思考：为什么要使用分页？**

- 减少数据的使用量

### 7.1、使用Limit分页(掌握)

```mysql
SELECT * from user limit startIndex,pageSize;
```

使用Mybatis实现分页，核心SQL

1. 接口

   ```java
   //分页查询用户   像这种多个参数的就推荐使用map
   List<User> getUserByLimit(Map<String,Integer> map);
   ```

   

2.  Mapper.xml 文件

   ```xml
   <!--分页查询 方式一-->
   <select id="getUserByLimit" parameterType="map" resultMap="UserMap">
       select * from mybatis.user limit #{startIndex},#{pageSize};
   </select>
   ```

   

3. 测试

   ```java
   //测试分页功能(方式一)
   @Test
   public void testGetUserByLimit(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
       UserMapper mapper = sqlSession.getMapper(UserMapper.class);
       Map<String, Integer> map = new HashMap<String, Integer>();
       map.put("startIndex",0);//开始的页码下标
       map.put("pageSize",3);//每页的大小
       List<User> userByLimit = mapper.getUserByLimit(map);
       for (User user : userByLimit) {
           System.out.println(user);
       }
       sqlSession.close();
   
   }
   ```

### 7.2、RowBounds（了解）

**目的：**

为了体现java的面向对象思想，不再使用Sql实现分页

1. 接口

   ```java
   //分页方式二（RowBounds 了解即可）
   List<User> getUserByRowBounds();
   ```

   

2. Mapper.xml 文件

   ```xml
   <!--分页查询  RowBounds方式 了解即可-->
   <select id="getUserByRowBounds" resultMap="UserMap">
       select * from mybatis.user;
   </select>
   ```

   

3. 测试

   ```java
   //测试分页（方式二 RowBounds）
   @Test
   public void testLimitByRowRounds(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
       RowBounds rowBounds = new RowBounds(1,2);
       List<User> userList = sqlSession.selectList("com.fafa.dao.UserMapper.getUserByRowBounds", null, rowBounds);
       for (User user : userList) {
           System.out.println(user);
       }
       sqlSession.close();
   }
   
   ```

### 7.3、分页插件(了解)

![1](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212939.png)



## 8、使用注解开发

### 8.1、面向接口开发

- 大家之前都学过面向对象编程，也学习过接口，但在真正的开发中，很多时候我们会选择面向接口编程


- **根本原因 : 解耦 , 可拓展 , 提高复用 , 分层开发中 , 上层不用管具体的实现 , 大家都遵守共同的标准 , 使得开发变得容易 , 规范性更好**

- 在一个面向对象的系统中，系统的各种功能是由许许多多的不同对象协作完成的。在这种情况下，各个对象内部是如何实现自己的,对系统设计人员来讲就不那么重要了；


- 而各个对象之间的协作关系则成为系统设计的关键。小到不同类之间的通信，大到各模块之间的交互，在系统设计之初都是要着重考虑的，这也是系统设计的主要工作内容。面向接口编程就是指按照这种思想来编程。



### 8.2、利用注解开发

- **mybatis最初配置信息是基于 XML ,映射语句(SQL)也是定义在 XML 中的。而到MyBatis 3提供了新的基于注解的配置。不幸的是，Java 注解的的表达力和灵活性十分有限。最强大的 MyBatis 映射并不能用注解来构建**
- sql 类型主要分成 :
  - `@select ()`
  - `@update ()`
  - `@Insert ()`
  - `@delete ()`

 **注意：利用注解开发就不需要mapper.xml映射文件了 .** 

 1、我们在我们的接口中添加注解 

```java
//查询全部用户
@Select("select id,name,pwd password from user")
public List<User> getAllUser();
```

 2、在mybatis的核心配置文件中注入 

```xml
<!--使用class绑定接口-->
<mappers>
    <mapper class="com.kuang.mapper.UserMapper"/>
</mappers>
```

 3、我们去进行测试 

```java
@Test
public void testGetAllUser() {
    SqlSession session = MybatisUtils.getSession();
    //本质上利用了jvm的动态代理机制
    UserMapper mapper = session.getMapper(UserMapper.class);

    List<User> users = mapper.getAllUser();
    for (User user : users){
        System.out.println(user);
    }

    session.close();
}
```

 4、利用Debug查看本质 

![4](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723213001.png)

接口 === 架构（骨头）

注解开发：本质是主要运用反射机制

底层：动态代理模式(多线程里面讲过)

 5、本质上利用了jvm的动态代理机制 

![1](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212952.png)

 6、Mybatis详细的执行流程 

![3](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723213007.png)

### 8.3、注解方式实现CRUD

```java
//方法存在多个参数，所有的参数前面必须加上@Param("id")注解
@Delete("delete from user where id = ${uid}")
int deleteUser(@Param("uid") int id);
```

 <font color='red'>**关于@Param( )注解**</font>

- 基本类型的参数或者String类型，需要加上
- 引用类型不需要加
- 如果只有一个基本类型的话，可以忽略，但是建议大家都加上
- 我们在SQL中引用的就是我们这里的@Param()中设定的属性名

```
#{}可以防止SQl注入，${}不可以
```

 使用注解和配置文件协同开发，才是MyBatis的最佳实践！
**使用注解开发可以提高我们的开发效率，可以合理使用哦！** 

## 9、Lombok的使用

 Lombok项目是一个Java库，它会自动插入编辑器和构建工具中，Lombok提供了一组有用的注释，用来消除Java类中的大量样板代码。仅五个字符(@Data)就可以替换数百行代码从而产生干净，简洁且易于维护的Java类。 



**使用步骤:**

1. 在IDEA中安装Lombok插件(点击Settings-->Plugins)

   ![image-20210726145842401](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210726145842.png)

2. 在项目中导入lombok的jar包

   ```xml
   <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
   <dependency>
       <groupId>org.projectlombok</groupId>
       <artifactId>lombok</artifactId>
       <version>1.18.12</version>
       <scope>provided</scope>
   </dependency>
   
   ```

   

3. 在程序上加注解

   ```java
   @Getter and @Setter
   @FieldNameConstants
   @ToString
   @EqualsAndHashCode
   @AllArgsConstructor, @RequiredArgsConstructor and @NoArgsConstructor
   @Log, @Log4j, @Log4j2, @Slf4j, @XSlf4j, @CommonsLog, @JBossLog, @Flogger, @CustomLog
   @Data
   @Builder
   @SuperBuilder
   @Singular
   @Delegate
   @Value
   @Accessors
   @Wither
   @With
   @SneakyThrows
   @val
   ```

   ![1626849898457](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723213014.png)

## 10、多对一的处理

```
多个学生对应一个老师；
```

```mysql
alter table student ADD CONSTRAINT fk_tid foreign key (tid) references teacher(id)
```

### 10.1、搭建测试环境

相关mysql语句

```mysql
CREATE TABLE `teacher` (
  `id` INT(10) NOT NULL,
  `name` VARCHAR(30) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8;

INSERT INTO teacher(`id`, `name`) VALUES (1,'杨老师');

CREATE TABLE `student` (
  `id` INT(10) NOT NULL,
  `name` VARCHAR(30) DEFAULT NULL,
  `tid` INT(10) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `fktid` (`tid`),
  CONSTRAINT `fktid` FOREIGN KEY (`tid`) REFERENCES `teacher` (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8;

INSERT INTO `student` (`id`, `name`, `tid`) VALUES (1, '小明', 1);
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (2, '小红', 1);
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (3, '小张', 1);
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (4, '小李', 1);
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (5, '小王', 1);
```



1. 导入lombok
2. 新建实体类Teacher,Student
3. 建立Mapper接口
4. 建立Mapper.xml文件
5. 在核心配置文件中绑定注册我们的Mapper接口或者文件 【方式很多，随心选】
6. 测试查询是否能够成功

### 10.2、按照查询嵌套处理

```xml
<!--
    思路：
    1. 查询所有的学生信息
    2. 根据查询出来的学生的tid寻找特定的老师 (子查询)
-->
<select id="getStudent" resultMap="StudentTeacher">
    select * from student
</select>
<resultMap id="StudentTeacher" type="student">
    <result property="id" column="id"/>
    <result property="name" column="name"/>
    <!--复杂的属性，我们需要单独出来 对象：association 集合：collection-->
    <association property="teacher" column="tid" javaType="teacher" select="getTeacher"/>
</resultMap>
<select id="getTeacher" resultType="teacher">
    select * from teacher where id = #{id}
</select>
```

### 10.3、按照结果嵌套处理

```xml
<!--按照结果进行查询-->
<select id="getStudent2" resultMap="StudentTeacher2">
    select s.id sid , s.name sname, t.name tname
    from student s,teacher t
    where s.tid=t.id
</select>
<!--结果封装，将查询出来的列封装到对象属性中-->
<resultMap id="StudentTeacher2" type="student">
    <result property="id" column="sid"/>
    <result property="name" column="sname"/>
    <association property="teacher" javaType="teacher">
        <result property="name" column="tname"></result>
    </association>
</resultMap>
```

回顾Mysql多对一查询方式：

- 子查询（按照查询嵌套）
- 联表查询（按照结果嵌套）

## 11、一对多

```
一个老师对多个学生
对于老师而言，就是一对多的关系
```

### 11.1、环境搭建

和上面那个一样

实体类

```java
/**
 * 学生实体类
* */
@Data
@ToString
public class Student {
    private int id;
    private String name;
    private int tid;
}
```

```java
/**
 * 老师实体类
 * */
@Data
@ToString
public class Teacher {
    private int id;
    private String name;
    //组合
    private List<Student> students;
}
```



### 11.2、**按照结果嵌套嵌套处理**

```xml
<mapper namespace="com.fafa.dao.TeacherMapper">
    <select id="getTeacherById" resultMap="TeacherStudent">
        select t.id tid,t.name tname,s.id sid,s.name sname,s.tid stid
        from student s,teacher t
        where t.id = s.tid and t.id = #{uid};
    </select>
    <resultMap id="TeacherStudent" type="Teacher">
        <result property="id" column="tid"/>
        <result property="name" column="tname"/>
        <!--
            一对多使用 collection
            多对一使用 association
        -->
        <collection property="students" ofType="student">
            <result property="id" column="sid"/>
            <result property="name" column="sname"/>
            <result property="tid" column="stid"/>
        </collection>
    </resultMap>
</mapper>
```

### 小结

1. 关联 - association{多对一}
2. 集合 - collection{一对多}
3. JavaType & ofType
   1. JavaType 用来指定实体类中的类型
   2. ofType用来映射到List或者结合中的pojo类型，泛型中的约束类型

**注意点**

- 保证SQL的可读性，尽量保证通俗易懂
- 注意一对多和多对一，属性名和字段的问题
- 如果问题不好排查错误，可以使用日志，建议使用Log4j

**面试必考**

- Mysql引擎
- InnoDB底层原理
- 索引
- 索引优化

## 12、动态Sql

<font color='red'>**什么是动态SQL：动态SQL就是根据不同的条件生成不同的SQL语句**</font>

<font color='red'>**所谓的动态SQL，本质上还是SQL语句，只是我们可以在SQL层面，去执行一个逻辑代码**</font>

```xml
if
choose (when, otherwise)
trim (where, set)
foreach
```



### 12.1、搭建环境

相关SQL语句

```mysql
CREATE TABLE `blog`(
    `id` VARCHAR(50) NOT NULL COMMENT 博客id,
    `title` VARCHAR(100) NOT NULL COMMENT 博客标题,
    `author` VARCHAR(30) NOT NULL COMMENT 博客作者,
    `create_time` DATETIME NOT NULL COMMENT 创建时间,
    `views` INT(30) NOT NULL COMMENT 浏览量
)ENGINE=INNODB DEFAULT CHARSET=utf8;
```

创建一个工程

1. 导包

2. 编写配置文件

3. 编写实体类

   ```java
   /**
    * 博客实体类
    * */
   @Data
   @ToString
   public class Blog {
       private String id;
       private String title;
       private String author;
       private Date createTime;
       private int views;
   }
   
   ```

4. 编写实体类对应的Mapper接口和Mapper.xml文件

### 12.2、IF

 **需求：根据作者名字和博客名字来查询博客！如果作者名字为空，那么只根据博客名字查询，反之，则根据作者名来查询** 

1. 编写接口类

   ```java
   //查询博客（If）
   public List<Blog> queryBlogIf(Map<String,Object> map);
   ```

   

2. 编写Sql语句

   ```xml
   <!--需求1：
   根据作者名字和博客名字来查询博客！
   如果作者名字为空，那么只根据博客名字查询，反之，则根据作者名来查询
   select * from blog where title = #{title} and author = #{author}
   -->
   <select id="queryBlogIf" parameterType="map" resultType="Blog">
       select * from mybatis.blog where 1 = 1
       <if test="author != null">
           and author = #{author}
       </if>
       <if test="title != null">
           and title = #{title}
       </if>
   </select>
   ```

   

3. 测试

```java
//测试if功能
@Test
public void testIf(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
    HashMap<String, Object> map = new HashMap<String,Object>();
    //        map.put("author","可爱发");
    map.put("title","Mybatis如此简单！");
    List<Blog> blogs = mapper.queryBlogIf(map);
    for (Blog blog : blogs) {
        System.out.println(blog);
    }
    sqlSession.close();
}
```



### 12.3、choose (when, otherwise)

类似java里的Switch语句

 有时候，我们不想用到所有的查询条件，只想选择其中的一个，查询条件有一个满足即可，使用 choose 标签可以解决此类问题，类似于 Java 的 switch 语句 

1. 编写接口方法

   ```java
   //查询(Choose)
   public List<Blog> queryBlogChoose(Map<String,Object> map);
   ```

   

2. sql配置文件

   ```xml
   <!--
           choose语句
           和java里的Switch语法类似
           where会自动去掉多余的and
       -->
   <select id="queryBlogChoose" parameterType="map" resultType="Blog">
       select * from mybatis.blog
       <where>
           <choose>
               <when test="title != null">
                   title = #{title}
               </when>
               <when test="author != null">
                   and author = #{author}
               </when>
               <otherwise>
                   and views = #{views}
               </otherwise>
           </choose>
       </where>
   </select>
   ```

   

3. 测试类

   ```java
   //测试choose功能
   @Test
   public void testChoose(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
       BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
       HashMap<String, Object> map = new HashMap<String,Object>();
       map.put("author","可爱发");
       /*map.put("title","Mybatis如此简单！");*/
       List<Blog> blogs = mapper.queryBlogChoose(map);
       for (Blog blog : blogs) {
           System.out.println(blog);
       }
       sqlSession.close();
   }
   ```

### 12.4、 Where&trim

 **修改上面的SQL语句；** 

```xml
<select id="queryBlogIf" parameterType="map" resultType="blog">
    select * from blog
    <where>
        <if test="title != null">
            title = #{title}
        </if>
        <if test="author != null">
            and author = #{author}
        </if>
    </where>
</select>
```

 这个“`where`”标签会知道如果它包含的标签中有返回值的话，它就插入一个‘`where`’。此外，如果标签返回的内容是以AND 或OR 开头的，则它会剔除掉。 

 如果 where 元素与你期望的不太一样，你也可以通过自定义 trim 元素来定制 where 元素的功能。比如，和 where 元素等价的自定义 trim 元素为： 

```xml
<trim prefix="WHERE" prefixOverrides="AND |OR ">
    ...
</trim>
```

### 12.5、Set&trim

 同理，上面的对于查询 SQL 语句包含 where 关键字，如果在进行更新操作的时候，含有 set 关键词，我们怎么处理呢？ 

1. 编写BlogMapper接口方法

   ```java
   //修改用户信息（trim，set）
   public int upDateBlog(Map<String,Object> map);
   ```

   

2. 编写BlogMapper.xml

   ```xml
   <!--信息修改
           set可以去除多余的逗号
       -->
   <update id="upDateBlog" parameterType="map">
       update mybatis.blog
       <set>
           <if test="title != null">
               title = #{title},
           </if>
           <if test="author != null">
               author = #{author}
           </if>
       </set>
       where id = #{id}
   </update>
   ```

   

3. 测试

   ```java
   //修改数据
   @Test
   public void testUpdate(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
       BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
       HashMap<String, Object> map = new HashMap<String,Object>();
       map.put("author","可爱发222");
       map.put("id","cd69ad4884e545fb8cf9d8f2d0abc01f");
       /*map.put("title","Mybatis如此简单！");*/
       int i = mapper.upDateBlog(map);
       if(i > 0){
           System.out.println("Successfully!!!!");
       }
       sqlSession.close();
   }
   
   ```

   这个例子中，set 元素会动态地在行首插入 SET 关键字，并会删掉额外的逗号（这些逗号是在使用条件语句给列赋值时引入的）。

   **来看看与 set 元素等价的自定义 trim 元素吧：**

   ```xml
   <trim prefix="SET" suffixOverrides=",">
       ...
   </trim>
   ```

    **注意，我们覆盖了后缀值设置，并且自定义了前缀值。** 

### 12.6、SQL片段

 有时候可能某个 sql 语句我们用的特别多，为了增加代码的重用性，简化代码，我们需要将这些代码抽取出来，然后使用时直接调用。 

 **提取SQL片段：** 

```xml
<sql id="if-title-author">
    <if test="title != null">
        title = #{title}
    </if>
    <if test="author != null">
        and author = #{author}
    </if>
</sql>
```

 **引用SQL片段：** 

```xml
<select id="queryBlogIf" parameterType="map" resultType="blog">
    select * from blog
    <where>
        <!-- 引用 sql 片段，如果refid 指定的不在本文件中，那么需要在前面加上 namespace -->
        <include refid="if-title-author"></include>
        <!-- 在这里还可以引用其他的 sql 片段 -->
    </where>
</select>
```

**注意：**

①、最好基于 单表来定义 sql 片段，提高片段的可重用性

②、在 sql 片段中不要包括 where

### 12.7、Foreach

```mysql
select * from blog where 1 = 1 and (id = 1 or id = 2 or id = 3);
```

1. 编写接口

   ```java
   //Foreach
   public List<Blog> queryForeach(Map<String,Object> map);
   ```

   

2. 编写BlogMapper.xml

   ```xml
   <!--
           foreach语句的应用
             参考语句：select * from blog where 1 = 1 and (id = 1 or id = 2 or id = 3);
               collection:指定输入对象中的集合属性
               item:每次遍历生成的对象
               open:开始遍历时的拼接字符串
               close:结束时拼接的字符串
               separator:遍历对象之间需要拼接的字符串(分隔符)
       -->
   <select id="queryForeach" parameterType="map" resultType="Blog">
       select * from blog where 1 = 1
       <foreach collection="ids" open="and (" close=")" separator="or" item="id">
           id = #{id}
       </foreach>
   </select>
   ```

   

3. 测试

   ```java
   //测试ForEach
   @Test
   public void testForEach(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
       BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
       ArrayList<String> ids = new ArrayList<String>();
       ids.add("1");
       ids.add("2");
       ids.add("3");
       HashMap<String, Object> map = new HashMap<String,Object>();
       map.put("ids",ids);
       List<Blog> blogs = mapper.queryForeach(map);
       for (Blog blog : blogs) {
           System.out.println(blog);
       }
       sqlSession.close();
   }
   ```

   **其实动态 sql 语句的编写往往就是一个拼接的问题，为了保证拼接准确**，我们最好首先要写原生的 sql 语句出来，然后在通过 mybatis 动态sql 对照着改，防止出错。多在实践中使用才是熟练掌握它的技巧。

   动态SQL在开发中大量的使用，一定要熟练掌握！

   **一定要防止慢Sql**

## 13、缓存

### 13.1、缓存简介

```
查询： 连接数据库，消耗资源！
	高并发，高可用，高性能
	读写分离（用缓存读 数据库写）主从复制（数据库）
	
```

**1、什么是缓存 [ Cache ]？**

- 存在内存中的临时数据。
- 将用户经常查询的数据放在缓存（内存）中，用户去查询数据就不用从磁盘上(关系型数据库数据文件)查询，从缓存中查询，从而提高查询效率，解决了高并发系统的性能问题。

**2、为什么使用缓存？**

- 减少和数据库的交互次数，减少系统开销，提高系统效率。

**3、什么样的数据能使用缓存？**

- 经常查询并且不经常改变的数据。

### 13.2、Mybatis缓存

- MyBatis包含一个非常强大的查询缓存特性，它可以非常方便地定制和配置缓存。缓存可以极大的提升查询效率。


- MyBatis系统中默认定义了两级缓存：一级缓存和二级缓存


- 默认情况下，只有一级缓存开启。（SqlSession级别的缓存，也称为本地缓存）


- 二级缓存需要手动开启和配置，他是基于namespace级别的缓存。


### 13.3、一级缓存

**一级缓存也叫本地缓存：**

- 与数据库同一次会话期间查询到的数据会放在本地缓存中。
- 以后如果需要获取相同的数据，直接从缓存中拿，没必须再去查询数据库；

### 13.4、测试一级缓存

 1、在mybatis中加入日志，方便测试结果 

```xml
<settings>
<!--标准的日志2厂实现-->
<setting nane="logImp1" value="STDOUT_LOGGING"/>
</settings>
```

 2、编写接口方法 

```java
//查询用户信息
public User getUserById(@Param("id") int id);
```

 3、接口对应的Mapper文件 

```xml
<select id="getUserById" parameterType="_int" resultType="User" useCache="true">
    select * from mybatis.user where id = #{id};
</select>
```

 映射 

```xml
<mappers>
    <mapper resource="com/fafa/dao/UserMapper.xml"/>
</mappers>
```

4、测试

```java
//一级缓存测试（查询用户信息Byid）
@Test
public void testGetUserById(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    User user = mapper.getUserById(2);
    System.out.println(user);
    System.out.println("==========================================");
    User user2 = mapper.getUserById(2);
    System.out.println(user2);
    System.out.println("==========================================");
    System.out.println(user == user2);
    sqlSession.close();
}
```

![1627007182345](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723213033.png)

### 13.5、一级缓存失效的四种情况

 **1.查询不同的东西
2.增删改操作，可能会改变原来的数据，所以必定会刷新缓存!
3.查询不同的Mapper.xml
4.手动清理缓存!** 

**一级缓存是SqlSession级别的缓存，是一直开启的，我们关闭不了它；**

**一级缓存失效情况：**没有使用到当前的一级缓存，效果就是，还需要再向数据库中发起一次查询请求！

 **1、sqlSession不同** 

```java
@Test
public void testQueryUserById(){
    SqlSession session = MybatisUtils.getSession();
    SqlSession session2 = MybatisUtils.getSession();
    UserMapper mapper = session.getMapper(UserMapper.class);
    UserMapper mapper2 = session2.getMapper(UserMapper.class);

    User user = mapper.queryUserById(1);
    System.out.println(user);
    User user2 = mapper2.queryUserById(1);
    System.out.println(user2);
    System.out.println(user==user2);

    session.close();
    session2.close();
}
```

**观察结果**：发现发送了两条SQL语句！

**结论**：每个sqlSession中的缓存相互独立

 **2、sqlSession相同，查询条件不同** 

```java
@Test
public void testQueryUserById(){
    SqlSession session = MybatisUtils.getSession();
    UserMapper mapper = session.getMapper(UserMapper.class);
    UserMapper mapper2 = session.getMapper(UserMapper.class);

    User user = mapper.queryUserById(1);
    System.out.println(user);
    User user2 = mapper2.queryUserById(2);
    System.out.println(user2);
    System.out.println(user==user2);

    session.close();
}
```

**观察结果**：发现发送了两条SQL语句！很正常的理解

**结论**：当前缓存中，不存在这个数据

 **3、sqlSession相同，两次查询之间执行了增删改操作！** 

更改用户信息方法

```java
//更改用户信息
public int upDateUser(Map<String,Object> map);
```

编写对应的Mapper.xml文件

```xml
<!--增删改会刷新缓存-->
<update id="upDateUser" parameterType="map">
    update mybatis.user set name = #{name},pwd = #{pwd} where id = #{id};
</update>
```

 测试 

```java
//一级缓存测试（查询用户信息Byid）
@Test
public void testUpDateUser(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    HashMap<String, Object> map = new HashMap<String, Object>();
    User user = mapper.getUserById(2);
    map.put("id",2);
    map.put("name","undefined");
    map.put("pwd","***********");
    System.out.println(user);
    System.out.println("==========================================");
    //修改
    int i = mapper.upDateUser(map);

    User user2 = mapper.getUserById(2);
    System.out.println(user2);
    System.out.println("==========================================");
    System.out.println(user == user2);
    sqlSession.close();
}
```

**观察结果**：查询在中间执行了增删改操作后，重新执行了

**结论**：因为增删改操作可能会对当前数据产生影响

 **4、sqlSession相同，手动清除一级缓存** 

```java
@Test
public void testQueryUserById(){
    SqlSession session = MybatisUtils.getSession();
    UserMapper mapper = session.getMapper(UserMapper.class);

    User user = mapper.queryUserById(1);
    System.out.println(user);

    session.clearCache();//手动清除缓存

    User user2 = mapper.queryUserById(1);
    System.out.println(user2);

    System.out.println(user==user2);

    session.close();
}
```

 **一级缓存就是一个map** 

### 13.6、二级缓存

- 二级缓存也叫全局缓存，一级缓存作用域太低了，所以诞生了二级缓存

- 基于namespace级别的缓存，一个名称空间，对应一个二级缓存；

- 工作机制

  - 一个会话查询一条数据，这个数据就会被放在当前会话的一级缓存中；

  - 如果当前会话关闭了，这个会话对应的一级缓存就没了；但是我们想要的是，会话关闭了，一级缓存中的数据被保存到二级缓存中；

  - 新的会话查询信息，就可以从二级缓存中获取内容；

  - 不同的mapper查出的数据会放在自己对应的缓存（map）中；

### 13.7、使用步骤

 1、开启全局缓存 【`mybatis-config.xml`】 

```xml
<setting name="cacheEnabled" value="true"/>
```

 2、去每个`mapper.xml`中配置使用二级缓存，这个配置非常简单；【`xxxMapper.xml`】 

```xml
<cache/>
```

 官方示例=====>查看官方文档 

```xml
<cache
       eviction="FIFO"
       flushInterval="60000"
       size="512"
       readOnly="true"/>
```

 这个更高级的配置创建了一个 FIFO 缓存，每隔 60 秒刷新，最多可以存储结果对象或列表的 512 个引用，而且返回的对象被认为是只读的，因此对它们进行修改可能会在不同线程中的调用者产生冲突。 

3、代码测试

- 所有的实体类先实现序列化接口

  ```java
  @Data
  @ToString
  public class User implements Serializable {
      private int id;
      private String name;
      private String pwd;
  }
  ```

- 测试代码

  ```java
  //二级缓存测试（查询用户信息Byid）
  @Test
  public void testUpDateUser2(){
      SqlSession sqlSession = MybatisUtils.getSqlSession();
      SqlSession sqlSession2 = MybatisUtils.getSqlSession();
  
      UserMapper mapper = sqlSession.getMapper(UserMapper.class);
      UserMapper mapper2 = sqlSession2.getMapper(UserMapper.class);
  
      User user = mapper.getUserById(2);
      System.out.println(user);
      System.out.println("==========================================");
      sqlSession.close();
  
      User user2 = mapper2.getUserById(2);
      System.out.println(user2);
      System.out.println("==========================================");
      System.out.println(user == user2);
      sqlSession2.close();
  }
  }
  
  ```

  ![1627008049524](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212538.png)

### 13.8 结论

- 只要开启了二级缓存，我们在同一个Mapper中的查询，可以在二级缓存中拿到数据
- 查出的数据都会被默认先放在一级缓存中
- 只有会话提交或者关闭以后，一级缓存中的数据才会转到二级缓存中

### 13.9、缓存原理图

![1](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212535.png)

![2](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212530.png)

### 13.10、EhCache(自定义缓存)

![3](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20210723212521.png)

第三方缓存实现–EhCache: 查看百度百科

Ehcache是一种广泛使用的java分布式缓存，用于通用缓存；

**要在应用程序中使用Ehcache，需要引入依赖的jar包**

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis.caches/mybatis-ehcache -->
<dependency>
    <groupId>org.mybatis.caches</groupId>
    <artifactId>mybatis-ehcache</artifactId>
    <version>1.1.0</version>
</dependency>
```

 在`UserMapper.xml`中使用对应的缓存即可 

```xml
<mapper namespace = “org.acme.FooMapper” > 
    <cache type = “org.mybatis.caches.ehcache.EhcacheCache” /> 
</mapper>
```

 编写`ehcache.xml`文件，如果在加载时未找到/`ehcache.xml`资源或出现问题，则将使用默认配置。 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd"
         updateCheck="false">
    <!--
      diskStore：为缓存路径，ehcache分为内存和磁盘两级，此属性定义磁盘的缓存位置。参数解释如下：
      user.home – 用户主目录
      user.dir – 用户当前工作目录
      java.io.tmpdir – 默认临时文件路径
    -->
    <diskStore path="./tmpdir/Tmp_EhCache"/>

    <defaultCache
                  eternal="false"
                  maxElementsInMemory="10000"
                  overflowToDisk="false"
                  diskPersistent="false"
                  timeToIdleSeconds="1800"
                  timeToLiveSeconds="259200"
                  memoryStoreEvictionPolicy="LRU"/>

    <cache
           name="cloud_user"
           eternal="false"
           maxElementsInMemory="5000"
           overflowToDisk="false"
           diskPersistent="false"
           timeToIdleSeconds="1800"
           timeToLiveSeconds="1800"
           memoryStoreEvictionPolicy="LRU"/>
    <!--
      defaultCache：默认缓存策略，当ehcache找不到定义的缓存时，则使用这个缓存策略。只能定义一个。
    -->
    <!--
     name:缓存名称。
     maxElementsInMemory:缓存最大数目
     maxElementsOnDisk：硬盘最大缓存个数。
     eternal:对象是否永久有效，一但设置了，timeout将不起作用。
     overflowToDisk:是否保存到磁盘，当系统当机时
     timeToIdleSeconds:设置对象在失效前的允许闲置时间（单位：秒）。仅当eternal=false对象不是永久有效时使用，可选属性，默认值是0，也就是可闲置时间无穷大。
     timeToLiveSeconds:设置对象在失效前允许存活时间（单位：秒）。最大时间介于创建时间和失效时间之间。仅当eternal=false对象不是永久有效时使用，默认是0.，也就是对象存活时间无穷大。
     diskPersistent：是否缓存虚拟机重启期数据 Whether the disk store persists between restarts of the Virtual Machine. The default value is false.
     diskSpoolBufferSizeMB：这个参数设置DiskStore（磁盘缓存）的缓存区大小。默认是30MB。每个Cache都应该有自己的一个缓冲区。
     diskExpiryThreadIntervalSeconds：磁盘失效线程运行时间间隔，默认是120秒。
     memoryStoreEvictionPolicy：当达到maxElementsInMemory限制时，Ehcache将会根据指定的策略去清理内存。默认策略是LRU（最近最少使用）。你可以设置为FIFO（先进先出）或是LFU（较少使用）。
     clearOnFlush：内存数量最大时是否清除。
     memoryStoreEvictionPolicy:可选策略有：LRU（最近最少使用，默认策略）、FIFO（先进先出）、LFU（最少访问次数）。
     FIFO，first in first out，这个是大家最熟的，先进先出。
     LFU， Less Frequently Used，就是上面例子中使用的策略，直白一点就是讲一直以来最少被使用的。如上面所讲，缓存的元素有一个hit属性，hit值最小的将会被清出缓存。
     LRU，Least Recently Used，最近最少使用的，缓存的元素有一个时间戳，当缓存容量满了，而又需要腾出地方来缓存新的元素的时候，那么现有缓存元素中时间戳离当前时间最远的元素将被清出缓存。
  -->

</ehcache>
```

 **合理的使用缓存，可以让我们程序的性能大大提升！** 

