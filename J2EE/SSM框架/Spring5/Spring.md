# Spring

## 1、Spring

### 1.1、简介 

- Spring:春天-------->给软件行业带来了春天！
- 2002年，首次推出了Spring框架的雏形：interface21框架
- Spring框架即以interface21框架为基础，经过重新设计，并且不断丰富其内涵，于2004年3月24日，发布了1.0正式版。
- Rod Johnson,Spring Framework创始人，著名作者。
- Spring的理念：使现有技术更加容易使用，本身是一个大杂烩，整合了现有技术的框架！
- SSH：Struct2 + Spring +Hibernate！（已经淘汰了）
- SSM：SpringMvc +Spring + Mybatis！

- spring官网： https://spring.io/projects/spring-framework#overview

- 官方下载： https://repo.spring.io/release/org/springframework/spring/


- GitHub： https://github.com/spring-projects/spring-framework


- Spring Web MVC： [spring-webmvc最新版](https://mvnrepository.com/artifact/org.springframework/spring-webmvc/5.2.7.RELEASE)

  ```xml
  <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
  <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.2.7.RELEASE</version>
  </dependency>
  
  <!--
  有了这个就可以整合Mybatis框架了 https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
  <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>5.2.7.RELEASE</version>
  </dependency>
  ```

### 1.2、优点

- Spring是一个开源的免费框架（容器）！
- Spring是一个轻量级的非入侵式的框架！
- 控制反转（IOC），面向切面编程（AOP）！
- 支持事务的处理，对框架整合的支持！

开源免费容器，轻量级非侵入式，控制反转，面向切面，支持事务，支持框架整合

**Spring是一个轻量级的控制反转(IOC)和面向切面(AOP)编程的框架**

### 1.3、组成 



![1](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210725165019.png)

### 1.4、扩展

**现代化的java开发 -> 基于Spring的开发**

![2](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210725165156.png)

![3](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210725165214.png)



## 2、IOC理论推导

### 传统的调用

1. UserDao

   ```java
   public interface UserDao {
       void getUser();
   }
   ```

   

2. UserDaoImpl

   ```java
   public class UserDaoImpl implements UserDao{
       public void getUser() {
           System.out.println("默认获取用户数据");	
       }
   }
   ```

   

3. UserSevice

   ```java
   public interface UserService {
       void getUser();
   }
   ```

   

4. UserServiceImpl

   ```java
   package Service;
   import dao.UserDao;
   import dao.UserDaoImpl;
   
   public class UserServiceImpl implements UserService{
       UserDao userDao = new UserDaoImpl();		
       public void getUser(){
           userDao.getUser();
       }	
   }
   ```

   

5. 测试

   ```java
   import Service.UserService;
   import Service.UserServiceImpl;
   
   public class MyTest {
       public static void main(String[] args) {
           // 用户实际调用的是业务层，dao层他们不需要接触
           UserService userService = new UserServiceImpl();
           userService.getUser();
       }
   }
   ```

   

6. 在我们之前的业务中，用户的需求可能会影响我们原来的代码，我们需要根据用户的需求去修改原代码！如果程序代码量十分大，修改一次的成本代价十分昂贵！

![4](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210725165521.png)

**改良：我们使用一个Set接口实现。已经发生了革命性的变化！**

**UserServiceImpl**

```java
//优化后的代码  利用Set进行动态实现值的注入
private UserDao userDao;

public void setUserDao(UserDao userDao) {
    this.userDao = userDao;
}

public void getUser() {
    userDao.getUser();
}
```

set() 方法实际上是动态改变了 UserDao userDao 的 初始化部分（**new UserDaoImpl()**

测试:

```java
public class MyTest {
    public static void main(String[] args) {
        //用户实际调用的是业务层，dao层他们不需要接触
        UserService userService = new UserServiceImpl();

        ((UserServiceImpl) userService).setUserDao(new UserDaoMysqlImpl());
        userService.getUser();
    }
}

```

- 之前，程序是主动创建对象！控制权在程序猿手上！
- 使用了set注入后，程序不再具有主动性，而是变成了被动的接受对象！（主动权在客户手上）
  本质上解决了问题，程序员不用再去管理对象的创建

- 系统的耦合性大大降低，可以更专注在业务的实现上


- 这是IOC（控制反转）的原型，反转(理解)：**主动权交给了用户**

![5](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210725165853.png)

### IOC本质

 ![1](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210726115950.png)

 ![2](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210726120016.png)

 ![3](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210726120022.png)

 ![4](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210726120033.png)

## 3、Hello Spring

在父模块中导入jar包

```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.7.RELEASE</version>
</dependency>

```

pojo的Hello.java

```java
package pojo;

public class Hello {

    private String str;

    public String getStr() {
        return str;
    }

    public void setStr(String str) {
        this.str = str;
    }

    @Override
    public String toString() {
        return "Holle [str=" + str + "]";
    }
}

```

在resource里面的xml配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--在Spring中创建对象，在Spring这些都称为bean
     类型 变量名 = new 类型();
     Hello hello = new Hello();

     bean = 对象(hello)
     id = 变量名(hello)
     class = new的对象(new Hello();)
     property 相当于给对象中的属性设值,让str="Spring"
    -->
    <bean id="hello" class="pojo.Hello">
        <property name="str" value="Spring"/>
    </bean>
</beans>

```

测试类MyTest

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import pojo.Hello;

public class MyTest {

    public static void main(String[] args) {
        //获取Spring的上下文对象
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        //我们的对象下能在都在spring·中管理了，我们要使用，直接取出来就可以了
        Hello holle = (Hello) context.getBean("hello");
        System.out.println(holle.toString());
    }

}

```

核心用set注入，所以必须要有下面的se()方法

```java
//Hello类
public void setStr(String str) {
    this.str = str;
}
```

**思考**：

 ![5](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210726121338.png)

IOC：对象由Spring来创建，管理，装配！

**弹幕评论里的理解**：

原来这套程序是：你写好菜单买好菜，客人来了自己把菜炒好招待，就相当于你请人吃饭

现在的这套程序是：你告诉楼下餐厅，你要那些菜，客人来的时候，餐厅把做好的你需要的菜送上来

IOC:炒菜这件事，不再由你自己来做，而是委托给了第三方--->餐厅来做

此时的区别就是，如果我们还需要做其他的菜，我不需要自己搞菜谱买食材在做好，而是告诉餐厅我要什么菜，什么时候要，你做好送来

在前面第一个module试试引入Spring

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="userDaomSql" class="dao.UserDaoMysqlImpl"></bean>

    <bean id="userServiceImpl" class="service.UserServiceImp">
        <!--ref引用spring中已经创建很好的对象-->
        <!--value是一个具体的值,基本数据类型-->
        <property name="userDao" ref="userDaomSql"/>
    </bean>

</beans>

```

第一个module改良后测试

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
import service.UserServiceImpl;

public class MyTest {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        UserServiceImpl userServiceImpl = (UserServiceImpl) context.getBean("userServiceImpl");
        userServiceImpl.getUser();
    }
```

**总结：**

所有的类都要装配到beans.xml里

所有的bean都要通过容器来取（ApplicationContext）

容器里面取得的bean，拿出来就是一个对象，用对象调用方法即可

## 4、IOC创建对象的方式

1. 使用无参数构造对象，默认

2. 使用有参构造（如下）

   - 方式一：下标赋值

     index指的是有参构造中参数的下标，下标从0开始;index指的是有参构造中参数的下标，下标从0开始;

     ```xml
     <!--IOC创建对象方式一 下标
         index指的是有参构造中参数的下标，下标从0开始;
         -->
     <bean id="user" class="com.fafa.pojo.User">
         <constructor-arg index="0" value="可爱发"/>
     </bean>
     ```

   - 方式二：类型赋值（不建议使用）

     ```xml
     <!--IOC创建对象方式二 通过类名(不推荐)
         基本类型直接写即可（如int），引用类型，如String（java.lang.String这样写）
         -->
     <bean id="user" class="com.fafa.pojo.User">
         <constructor-arg type="java.lang.String" value="高冷发"/>
     </bean>
     ```

   - 方式三：直接通过参数名（掌握）

     ```xml
     <!--IOC创建对象方式三 名字（推荐）
         比如参数名是name 那么就是name="name" 具体的值就是value="具体值"
         -->
     <bean id="user" class="com.fafa.pojo.User">
         <constructor-arg name="name" value="傲娇发"/>
     </bean>
     ```

     注册bean之后就是对象的初始化了（类似 new 类名()）

     弹幕评论：

     name方式还需要无参构造和set方法，index和type只需要有参构造就可以了，就算是两个对象，也只是有一个实例（**单例模式：全局唯一**）

     ```java
     User user = (User) context.getBean("user");
     User user2 = (User) context.getBean("user");
     System.out.println(user == user2);
     ```

     ![image-20210726132519625](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210726132521.png)

   总结：在配置文件加载的时候，容器（<bean>）中管理的对象就已经初始化了

## 5、Spring配置

### 5.1、别名

```xml
<bean id="user" class="pojo.User">
    <constructor-arg name="name" value="chen"></constructor-arg>
</bean>

<alias name="user" alias="userLove"/>
<!-- 使用时
 User user2 = (User) context.getBean("userLove");	
-->

```

### 5.2、Bean的配置

```xml
<!--id：bean的唯一标识符，也就是相当于我们学的对象名
class：bean对象所对应的会限定名：包名+类型
name：也是别名，而且name可以同时取多个别名 -->
<bean id="user" class="pojo.User" name="u1 u2,u3;u4">
    <property name="name" value="chen"/>
</bean>
<!-- 使用时
 User user2 = (User) context.getBean("u1");	
-->

```

### 5.3、import

import一般用于团队开发，它可以使用多个配置文件，导入并合并为一个

假设，现在项目中有多个人开发，这三个复制不同的类开发，不同类需要注册在不同的bean中，我们可以利用import将所有人的beans.xml合并为一个总的！

- 张三（beans.xml）

- 李四（beans2.xml）

- 王五（beans3.xml）

- applicationContext.xml

  ```xml
  <import resource="beans.xm1"/>
  <import resource="beans2.xml"/>
  <import resource="beans3.xm1"/>
  ```

**使用的时候，直接使用总的配置就可以了**

**注意：**

按照在总的xml中的导入顺序来进行创建，后导入的会重写先导入的，最终实例化的对象会是后导入xml中的那个

## 6、DI注入（掌握）

### 6.1、构造器注入

前面讲过的

### 6.2、set方式注入（重点）

- 依赖注入：Set注入！
  - 依赖：bean对象的创建依赖容器！
  - 注入：bean对象中的所有属性，由容器来注入！

【环境搭建】

1. 复杂类型（Address类）

   ```java
   public class Address {
       private String address;
   
       public String getAddress() {
           return address;
       }
   
       public void setAddress(String address) {
           this.address = address;
       }
   }
   
   ```

   

2. 真实测试对象（Student类）

   ```java
   public class Student {
       private String name;
       private Address address;
       private String[] books;
       private List<String> hobbys;
       private Map<String,String> card;
       private Set<String> games;
       private String wife;
       private Properties info;
   }
   
   ```

   

3. applicationContext.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
                              https://www.springframework.org/schema/beans/spring-beans.xsd">
       
       
           <!--第二种，Bean注入，ref-->
           <property name="address" ref="address"/>
   
           <!--数组-->
           <property name="books">
               <array>
                   <value>红楼梦</value>
                   <value>西游记</value>
                   <value>水浒传</value>
                   <value>三国演义</value>
               </array>
           </property>
   
           <!--List-->
           <property name="hobbys">
               <list>
                   <value>唱歌</value>
                   <value>篮球</value>
                   <value>混音</value>
                   <value>敲代码</value>
               </list>
           </property>
   
           <!--Map 有点特别  里面用entry-->
           <property name="card">
               <map>
                   <entry key="身份证" value="11111111"/>
                   <entry key="手机号" value="1008611"/>
               </map>
           </property>
   
           <!--Set-->
           <property name="games">
               <set>
                   <value>LOL</value>
                   <value>COC</value>
                   <value>BOB</value>
               </set>
           </property>
   
           <!--空指针-->
           <property name="wife">
               <null/>
           </property>
   
           <!--props-->
           <property name="info">
               <props>
                   <prop key="indexNumber">201906080115</prop>
                   <prop key="sex">男</prop>
                   <prop key="username">root</prop>
                   <prop key="password">541888</prop>
               </props>
           </property>
       </bean>
   </beans>
   ```
   
   
   
4. 测试类

   ```java
   public class MyTest {
       public static void main(String[] args) {
           ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
           Student stu = (Student) context.getBean("stu");
           System.out.println(stu.toString());
           /*
           Student(
           name=小小怪,
           address=Address(address=纽约),
           books=[红楼梦, 西游记, 水浒传, 三国演义],
           hobbys=[唱歌, 篮球, 混音, 敲代码],
           card={身份证=11111111, 手机号=1008611},
           games=[LOL, COC, BOB],
           wife=null,
           info={password=541888, indexNumber=201906080115, sex=男, username=root}
           )
   */
   
       }
   }
   
   ```
   
   

### 6.3、拓展方式（第三方）

官方文档位置

 ![1](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210727194629.png)

pojo增加User类

```java
package pojo;

public class User {
    private String name;
    private int id;
    public User() {

    }
    public User(String name, int id) {
        super();
        this.name = name;
        this.id = id;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getId() {
        return id;
    }
    public void setId(int id) {
        this.id = id;
    }
    @Override
    public String toString() {
        return "User [name=" + name + ", id=" + id + "]";
    }
}

```

注意： beans 里面加上这下面两行

使用p和c命名空间需要导入xml约束

xmlns:p=“http://www.springframework.org/schema/p”
xmlns:c=“http://www.springframework.org/schema/c”

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--拓展注入方式
    P命名空间注入(Set注入) 和 C命名空间注入(构造器)
    -->
    <!--P命名(property) -->
    <bean id="userP" class="com.fafa.pojo.User" p:age="18" p:name="可爱发"/>
    <!--C命名空间（constructor）-->
    <bean id="userC" class="com.fafa.pojo.User" c:age="20" c:name="傲娇发"/>
</beans>
```

测试

```java
//测试扩展注入方式（C 和 P）
@Test
public void test01(){
    ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
    /* User userP = context.getBean("userP", User.class);*/
    User userP = (User) context.getBean("userP");
    System.out.println(userP.toString());
    System.out.println("======================================");
    User userC = context.getBean("userC", User.class);
    System.out.println(userC.toString());
}
```

### 6.4、Bean Scopes(Bean 作用域)

 ![3](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210727210229.png)

 ![4](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210727210253.png)

**单例模式(Spring的默认模式)**

```xml
<bean id="user2" class="pojo.User" c:name="cxk" c:age="19" scope="singleton"></bean>
```

 ![5](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210727210337.png)

单例模式是把对象放在pool中，需要再取出来，使用的都是同一个对象实例

**原型模式: 每次从容器中get的时候，都产生一个新对象！**

```xml
<bean id="user2" class="pojo.User" c:name="cxk" c:age="19" scope="prototype"></bean>
```

 ![6](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210727210428.png)

其余的request、session、application这些只能在web开放中使用！

## 7、Bean的自动装配（掌握）

- 自动装配是Spring满足我们的Bean依赖的一种方式
- Spring会在上下文中自动寻找，并自动给bean装配属性！

在Spring中有三种装配的方式

1. 在xml中显示的配置
2. 在java中显示的配置
3. 隐式 的自动装配bean【重要】 

#### 7.1、测试

环境搭建：一个人两个宠物

#### 7.2、byName自动装配

```xml
<!--
    byName:会自动在容器中查找，和自己对象set方法的set后面的值对应的id
    例如：setDog，去set后面的字符作为id，则id = dog 才可以进行自动装配
    -->
<bean id="people" class="com.fafa.pojo.People" autowire="byName">
    <property name="name" value="可爱发"/>
    <!-- <property name="cat" ref="cat"/>
        <property name="dog" ref="dog"/>-->
</bean>
```

byName只能取到小写，大写取不到

#### 7.3、byType自动装配

```xml
<!--
    byType：会在容器中自动查找，和自己对象属性相同的Bean
    例如，Dog dog；那么就会查找pojo的dog类，在进行自动装配
    -->
<bean id="people" class="com.fafa.pojo.People" autowire="byType">
    <property name="name" value="可爱发"/>
    <!-- <property name="cat" ref="cat"/>
        <property name="dog" ref="dog"/>-->
</bean>
```

byType自动装配：byType会自动查找，和自己对象set方法参数的类型相同的bean

保证所有的class唯一(类为全局唯一)

#### 7.4、使用注解实现自动装配

jdk1.5支持的注解，spring2.5支持的注解

The introduction of annotation-based configuration raised the question of whether this approach is “better” than XML.（翻译：基于注释的配置的引入提出了一个问题，即这种方法是否比XML“更好”）

1.  导入context约束

   **xmlns:context="http://www.springframework.org/schema/context"**

2. 配置注解的支持：<context:annotation-config/>

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
                              https://www.springframework.org/schema/beans/spring-beans.xsd
                              http://www.springframework.org/schema/context
                              https://www.springframework.org/schema/context/spring-context.xsd">
   
       <context:annotation-config/>
   </beans>
   
   ```

   

##### 7.4.1、@Autowired

**默认是byType方式，如果匹配不上，就会byName**

在属性上使用，也可以在set上使用

我们可以不用编写set方法了，前提是自动装配的属性在Spring容器里，且要符合ByName 自动装配

```java
public class People {
    @Autowired
    private Cat cat;
    @Autowired
    private Dog dog;
    private String name;
}
```

```java
@Nullable 字段标记了这个注解，说明该字段可以为空

public name(@Nullable String name){

}
```

```java
//源码
public @interface Autowired { 
    boolean required() default true; 
}
```

如果定义了Autowire的require属性为false，说明这个对象可以为null，否则不允许为空（false表示找不到装配，不抛出异常）

##### 7.4.2、@Autowired+@Qualifier

**@Autowired不能唯一装配时，需要@Autowired+@Qualifier**

如果@Autowired自动装配环境比较复杂。自动装配无法通过一个注解完成的时候，可以使用@Qualifier(value = “dog”)去配合使用，指定一个唯一的id对象

```java
public class People {
    @Autowired
    private Cat cat;
    @Autowired
    @Qualifier(value = "dog01")
    private Dog dog;
    private String name;

}
```

弹幕评论：

如果xml文件中同一个对象被多个bean使用，Autowired无法按类型找到，可以用@Qualifier指定id查找

##### 7.4.3、@Resource

默认是byName方式，如果匹配不上，就会byType

```java
public class People {
    @Resource(name = "cat01")
    private Cat cat;
    @Resource(name = "dog01")
    private Dog dog;
    private String name;

}
```

弹幕评论：

Autowired是byType，@Autowired+@Qualifier = byType || byName

Autowired是先byteType,如果唯一則注入，否则byName查找。resource是先byname,不符合再继续byType

#### 区别：

@Resource和@Autowired的区别：

- 都是用来自动装配的，都可以放在属性字段上
- @Autowired通过byType的方式实现，而且必须要求这个对象存在！【常用】
- @Resource默认通过byname的方式实现，如果找不到名字，则通过byType实现！如果两个都找不到的情况下，就报错！【常用】
- 执行顺序不同：@Autowired通过byType的方式实现。@Resource默认通过byname的方式实现

## 8、使用注解开发（掌握）

在Spring4之后，使用注解开发，必须要保证aop包导入

![1](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210801182728.png)

使用注解需要导入context的约束

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context
                           https://www.springframework.org/schema/context/spring-context.xsd">
    
	<!--开启注解配置-->
    <context:annotation-config/>

</beans>

```

### 8.1、bean

弹幕评论：

有了 < context:component-scan >,另一个< context:annotation-config/>标签可以移除掉，因为已经被包含进去了

```java
<!--指定要扫描的包，这个包下面的注解才会生效
	别只扫一个com.kuang.pojo包--> 
<context:component-scan base-package="com.kuang"/> 
<context:annotation-config/>
1234
//@Component 组件
//等价于<bean id="user" classs"pojo.User"/> 
@Component
public class User {  
     public String name ="秦疆";
}
```

### 8.3、属性如何注入@value

```java

//等价于<bean id = "user" class = "com.fafa.pojo.User"/>
//@Component 组件
@Component("xxx")
//设置作用域
@Scope("singleton")
public class User {
    private String name = "发发";


    public String getName() {
        return name;
    }

    //赋值
    @Value("keaifa")
    public void setName(String name) {
        this.name = name;
    }
}

```

### 8.3、衍生的注解

@Component有几个衍生的注解，会按照web开发中，mvc框架分层

- dao(@Repository)
- service(@Service)
- controller(@Controller)

**这四个注解的功能是一样的，都是代表将某个类注册到容器中**

### 8.4、自动装配

@Autowired：默认是byType方式，如果匹配不上，就会byName方式

@Nullable：字段标记了这个注解，说明该字段可以为空

@Resource：默认是byName方式，如果匹配不上，就会byType方式

### 8.5、作用域@Scope

```java
//原型模式prototype，单例模式singleton
//scope("prototype")相当于<bean scope="prototype"></bean>
@Component 
@scope("prototype")
public class User { 

    //相当于<property name="name" value="kuangshen"/> 
    @value("kuangshen") 
    public String name; 

    //也可以放在set方法上面
    @value("kuangshen")
    public void setName(String name) { 
        this.name = name; 
    }
}

```

### 8.6、小结

**xml与注解：**

- xml更加万能，维护简单，适用于任何场景
- 注解，不是自己的类就使用不了，维护复杂

**最佳实践：**

- xml用来管理bean
- 注解只用来完成属性的注入
- 要开启注解支持

## 9、使用Java的方式配置Spring（了解）

不使用Spring的xml配置，完全交给java来做！

Spring的一个子项目，在Spring4之后，他成为了核心功能

 ![2](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210801185126.png)

**实体类：pojo的User.java**

```java

@ToString
//这个注解的意思就是说这个类被Spring类接管了，注册到了容器中
@Component
public class User {
    private String name;

    public String getName() {
        return name;
    }
    @Value("可爱发")//属性注入值
    public void setName(String name) {
        this.name = name;
    }
}

```

要么使用@Bean，要么使用@Component和ComponentScan，两种效果一样

配置文件：config中的MyConfig.java

```java
//这个也会被Spring容器托管，注册到容器中，因为他本来就是一个@Component
//@Component代表这是一个配置类，就和我们之前看到的beans.xml一样
@Configuration
//扫描包
@ComponentScan("com.fafa.pojo")
//引入其他类
@Import(MyConfig2.class)
public class MyConfig {
    //注册一个bean，就相当于我们之前写的一个bean标签
    //这个方法的名字，就相当于bean标签中的id属性
    //这个方法的返回值，就相当于bean标签中的class属性
    @Bean
    public User getUser(){
        return new User();//就是返回要注入到bean的对象！
    }
}

```

ComponentScan、@Component("pojo”) 这两个注解配合使用

**测试类**

```java
public class MyTest {
    public static void main(String[] args) {
        //如果完全使用了配置类方式去做，我们就只能通过AnnotationConfig 上下文来获取容器，通过配置类的class对象加载！
        ApplicationContext context = new AnnotationConfigApplicationContext(MyConfig.class);
        User user = context.getBean("getUser", User.class);
        System.out.println(user.toString());
    }
}

```

**总结：**

**@Bean是相当于< bean>标签创建的对象，而我们之前学的@Component是通过spring自动创建的这个被注解声明的对象，所以这里相当于有两个User对象被创建了。一个是bean标签创建的（@Bean），一个是通过扫描然后使用@Component，spring自动创建的User对象，所以这里去掉@Bean这些东西，然后开启扫描。之后在User头上用@Component即可达到spring自动创建User对象了**

## 10、代理模式（很重要）

为什么要学习代理模式？

因为这是Spring AOP的底层！【SpringAOP 和 SpringMVC 面试必问】

代理模式的分类：

- 静态代理
- 动态代理

![image-20210801204156559](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210801204157.png)

### 10.1、静态代理

角色分析：

- 抽象角色：一般会使用接口或者抽象类来解决
- 真实角色：被代理的角色
- 代理角色：代理真实角色，代理真实角色以后，我们一般会做一些附属操作
- 客户：访问代理对象的人！

代码步骤：

1. 接口

   ```java
   public interface Host {
       public void rent();
   }
   ```

2. 真实角色

   ```java
   /*房子的主人，即房东*/
   public class HostImpl implements Host{
       public void rent() {
           System.out.println("这个房东要出租房子！！！");
       }
   }
   ```

3. 代理角色

   ```java
   /**
    * 中介
   * */
   public class Proxy {
       public Host host;
   
       public Proxy() {
       }
   
       public Proxy(Host host) {
           this.host = host;
       }
       //代理进行出租
       public void rent(){
           host.rent();
           seeHouse();
           fare();
           contract();
       }
       //代理的附属条件
       //中介费
       public void fare(){
           System.out.println("需要缴纳中介费520元！");
       }
       //看房
       public void seeHouse(){
           System.out.println("顾客可以查看房子！");
       }
       //签合同
       public void contract(){
           System.out.println("双方满意，签合同！");
       }
   }
   
   ```

4. 客户端访问角色（租客）

   ```java
   /**
    * 租客
    * */
   public class Client {
       public static void main(String[] args) {
           //房东要出租房子
           Host host = new HostImpl();
           //中介帮房东出租房子，但这也会收取一定的费用（增加一些房东不做的操作）
           Proxy proxy = new Proxy(host);
           //看不到房东，但是通过代理，还是租到了房子（也就是中介）
           proxy.rent();
       }
   
   }
   ```

代理模式好处：

- 可以使真实角色操作更加纯粹!不用去关注一些公共的业务
- 公共也就是交给代理角色！实现了业务的分工！
- 公共业务发生扩展的时候，方便集中管理！

缺点：

- 一个真是对象就会产生一个代理角色；代码量会倍增（几十个真实角色就得写几十个代理），开发效率变低！

### 10.2、进一步理解静态代理

情景：在不更改原有公司业务代码的情况下，进行功能拓展

1. 接口

   ```java
   
   public interface UserService {
           public void add();
           public void delete();
           public void update();
           public void query();
   }
   ```

2. 真实对象（即实现类）

   ```java
   public class UserServiceImpl implements UserService {
       public void add() {
           System.out.println("增加一个用户");
       }
   
       public void delete() {
           System.out.println("删除一个用户");
       }
   
       public void update() {
           System.out.println("修改一个用户");
       }
   
       public void query() {
           System.out.println("查询一个用户");
       }
       //1.改动原有的业务代码，在公司里是大忌！！！
   }
   ```

3. 代理

   ```java
   /*
   * 代理
   * 目的是不改变UserserviceImpl的原有代码的情况下
   * 增添新的内容（日志方法）
   * */
   public class UserServiceProxy {
       private UserService userService;
       //Spring里推荐使用set方式
       public void setUserService(UserService userService) {
           this.userService = userService;
       }
       public void add(){
           msg("add");
           userService.add();
       }
       public void delete(){
           msg("delete");
           userService.delete();
       }
       public void update(){
           msg("update");
           userService.update();
       }
       public void query(){
           msg("query");
           userService.query();
       }
       //日志方法
       public void msg(String msg){
           System.out.println("【Log】使用了"+ msg +"方法");
       }
   }
   
   ```

4. 客户端访问者

   ```java
   public class Client {
       public static void main(String[] args) {
           /* UserService user = new UserServiceImpl();
           user.delete();*/
           UserServiceImpl userService = new UserServiceImpl();
           UserServiceProxy proxy = new UserServiceProxy();
           proxy.setUserService(userService);
           proxy.query();
       }
   
   }
   ```

### 10.3、动态代理（运用反射机制）

动态代理和静态代理角色一样，动态代理底层是反射机制

动态代理类是动态生成的，不是我们直接写好的！

动态代理（两大类）：基于接口，基于类

- 基于接口：JDK的动态代理【使用ing】
- 基于类：cglib
- java字节码实现：javasisit

了解两个类

1. Proxy：代理

2. InvocationHandler：调用处理程序

   ![1](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210802181742.png)

   实例：

   接口Host.interface

   ```java
   public interface Host {
       public void rent();
   }
   ```

   接口Host的实现类HostImpl

   ```java
   /*房子的主人，即房东*/
   public class HostImpl implements Host {
       public void rent() {
           System.out.println("这个房东要出租房子！！！");
       }
   }
   ```

   动态代理

   ```java
   /*
   动态代理
   * */
   public class ProxyInvocationHandler implements InvocationHandler {
       //被代理的接口
       private Host target;
   
       public void setTarget(Host target) {
           this.target = target;
       }
       //生成得到代理类
       public Object getProxy(){
           // newProxyInstance() -> 生成代理对象，就不用再写具体的代理类了
           // this.getClass().getClassLoader() -> 找到加载类的位置
           // target.getClass().getInterfaces() -> 代理的具体接口
           // this -> 代表了接口InvocationHandler的实现类ProxyInvocationHandler
           return Proxy.newProxyInstance(this.getClass().getClassLoader(),
                                         target.getClass().getInterfaces(),this);
       }
   
       //处理代理实例，并返回结果
       public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
           // 动态代理的本质，就是使用反射机制实现的
           // invoke()执行它真正要执行的方法
           Object result = method.invoke(target,args);
           return result;
       }
   }
   
   ```

   测试类

   ```java
   /**
    * 租客
    * */
   public class Client {
       public static void main(String[] args) {
           //房东要出租房子
           Host host = new HostImpl();
   
           ProxyInvocationHandler handler = new ProxyInvocationHandler();
           handler.setTarget(host);
           Host proxy = (Host) handler.getProxy();
           proxy.rent();
       }
   
   }
   
   ```

   弹幕评论：
   什么时候调用invoke方法的?
   代理实例调用方法时invoke方法就会被调用，可以debug试试

3. 改为万能代理类

   ```java
   /*
   动态代理
   * */
   public class ProxyInvocationHandler implements InvocationHandler {
       //改为Object就可以成为一个工具类，兼容性更好
       private Object target;
   
       public void setTarget(UserService target) {
           this.target = target;
       }
       //得到代理类
       public Object getProxy(){
           return Proxy.newProxyInstance(this.getClass().getClassLoader(),
                                         target.getClass().getInterfaces(),this);
       }
   
       //处理代理实例，并返回结果
       public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
           Object result = method.invoke(target,args);
           log(method.getName());
           return result;
       }
   
       //附加的打印日志方法
       public void log(String msg){
           System.out.println("[Log]:使用了"+msg+"方法哦，亲~");
       }
   }
   ```

   测试类

   ```java
   public class Client {
       public static void main(String[] args) {
           //真实角色
           UserServiceImpl userService = new UserServiceImpl();
           //代理角色，不存在
           ProxyInvocationHandler handler = new ProxyInvocationHandler();
           handler.setTarget(userService);//设置代理的对象
           //动态生成代理类
           UserService proxy = (UserService) handler.getProxy();
           //调用业务方法
           proxy.query();
       }
   }
   ```

4. 动态代理的好处：

   - 可以使真实角色操作更加纯粹!不用去关注一些公共的业务
   - 公共也就是交给代理角色！实现了业务的分工！
   - 公共业务发生扩展的时候，方便集中管理！
   - =============================================【前三条静态代理也有】
   - 一个动态代理代理的是一个接口，一般就是对应的一类业务
   - 一个动态代理类可以代理多个类，只要是实现了同一个接口即可！

## 11、AOP 面向切面编程（掌握）

### 11.1、什么是AOP？

 ![1](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210802203834.png)

![2](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210802203842.png)

### 11.2、AOP在Spring中的使用

提供声明式事务，允许用户定义切面

- 横切关注点：跨越应用程序多个模块的方法或功能。即是，与我们业务逻辑无关的，但是我们需要关注的部分，就是横切关注点。如日志，安全，缓存，事务等等…
- 切面(Aspect)：横切关注点 被模块化的特殊对象。即，它是一个类。（Log类）
- 通知(Advice)：切面必须要完成的工作。即，它是类中的一个方法。（Log类中的方法）
- 目标(Target)：被通知对象。（生成的代理类)
- 代理(Proxy)：向目标对象应用通知之后创建的对象。（生成的代理类）
- 切入点(PointCut)：切面通知执行的”地点”的定义。（最后两点：在哪个地方执行，比如：method.invoke()）
- 连接点(JointPoint)：与切入点匹配的执行点

![3](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210802204152.png)

SpringAop中，通过Advice定义横切逻辑，Spring中支持5中类型的Advice：

![4](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210802204303.png)

**即AOP在不改变原有代码的情况下，去增加新的功能（代理）**

### 11.3、使用Spring实现AOP

【重点】

- 使用AOP织入，需要导入一个依赖

  ```xml
  <!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
  <dependency>
      <groupId>org.aspectj</groupId>
      <artifactId>aspectjweaver</artifactId>
      <version>1.9.4</version>
      <scope>runtime</scope>
  </dependency>
  ```

#### 11.3.1、方法一：使用原生的Spring API接口

Spring API接口实现

需要先导入aop约束

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/aop
                           https://www.springframework.org/schema/aop/spring-aop.xsd">

</beans>
```

applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/aop
                           https://www.springframework.org/schema/aop/spring-aop.xsd">
    <!--注册Bean-->
    <bean id="userService" class="com.fafa.service.UserServiceImpl"/>
    <bean id="log" class="com.fafa.log.Log"/>
    <bean id="afterLog" class="com.fafa.log.AfterLog"/>

    <!--方式一：使用原生的Spring API接口-->
    <!--配置AOP：需要导入AOP的约束-->
    <aop:config>
        <!--切入点 expression:表达式
        execution(* * * * * * *)
        第一个*代表返回值类型，第二个是要执行的位置 （*(..)代表全部，任意）
        -->
        <aop:pointcut id="pointcut" expression="execution(* com.fafa.service.UserServiceImpl.*(..))"/>

        <!--执行环绕增加-->
        <aop:advisor advice-ref="log" pointcut-ref="pointcut"/>
        <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut"/>
    </aop:config>

</beans>
```

UserService.java

```java
public interface UserService {
    public void add();
    public void delete();
    public void update();
    public void select();
}
```



UserService的实现类 UserServiceImpl.java

```java
public class UserServiceImpl implements UserService{
    public void add() {
        System.out.println("增加一个用户");
    }

    public void delete() {
        System.out.println("删除一个用户");
    }

    public void update() {
        System.out.println("修改一个用户");
    }

    public void select() {
        System.out.println("查询一个用户");

    }
}
```

前置Log.java

```java
public class Log implements MethodBeforeAdvice {
    //method:要执行的目标对象方法
    //args:参数
    //target:目标参数
    public void before(Method method, Object[] args, Object target) throws Throwable {
        System.out.println(target.getClass().getName()+"的"+method.getName()+"方法 ");
    }
}
```

后置AfterLog.java

```java
public class AfterLog implements AfterReturningAdvice {
    public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
        System.out.println(method.getName()+"方法被调用，返回值是"+returnValue);
    }
}

```

测试类

```java
public class MyTest {
    @Test
    public void test01(){
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        //注意点：动态代理 代理的是 接口(不要写成实现类)
        UserService bean = (UserService) context.getBean("userService");
        bean.select();
    }
}
```

#### 11.3.2、方法二：自定义类实现AOP

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/aop
                           https://www.springframework.org/schema/aop/spring-aop.xsd">
    <!--注册Bean-->
    <bean id="userService" class="com.fafa.service.UserServiceImpl"/>
    <bean id="log" class="com.fafa.log.Log"/>
    <bean id="afterLog" class="com.fafa.log.AfterLog"/>
    
    <!--方式二：自定义-->
    <bean id="diy" class="com.fafa.diy.DiyPointCut"/>
    <aop:config>
        <!--自定义切面-->
        <aop:aspect ref="diy">
            <!--切入点-->
            <aop:pointcut id="point" expression="execution(* com.fafa.service.UserServiceImpl.*(..))"/>
            <aop:before method="before" pointcut-ref="point"/>
            <aop:after method="after" pointcut-ref="point"/>
        </aop:aspect>
    </aop:config>


</beans>
```

diy类

```java
public class DiyPointCut {

    public void before(){
        System.out.println("========方法执行前========");
    }

    public void after(){
        System.out.println("========方法执行后========");
    }
}
```

测试

```java
public class MyTest {
    @Test
    public void test01(){
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        //注意点：动态代理 代理的是 接口(不要写成实现类)
        UserService bean = (UserService) context.getBean("userService");
        bean.select();
    }
}
```

#### 11.3.3、方法三：使用注解实现（了解）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/aop
                           https://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- 注册 -->
    <bean id="userservice" class="com.fafa.service.UserServiceImpl"/>
    <!--方式三，使用注解实现-->
    <bean id="diyAnnotation" class="com.fafa.diy.DiyAnnotation"></bean>

    <!-- 开启自动代理 
  实现方式：默认JDK (proxy-targer-class="fasle")
        cglib (proxy-targer-class="true")-->
    <aop:aspectj-autoproxy/>
</beans>

```

DiyAnnotation.java

```java
package diy;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;

@Aspect  //标注这个类是一个切面
public class DiyAnnotation {

    @Before("execution(* service.UserServiceImpl.*(..))")
    public void before(){
        System.out.println("=====方法执行前=====");
    }

    @After("execution(* service.UserServiceImpl.*(..))")
    public void after(){
        System.out.println("=====方法执行后=====");
    }

    //在环绕增强中，我们可以给地暖管一个参数，代表我们要获取切入的点
    @Around("execution(* service.UserServiceImpl.*(..))")
    public void around(ProceedingJoinPoint joinPoint) throws Throwable {
        System.out.println("环绕前");

        Object proceed = joinPoint.proceed();

        System.out.println("环绕后");
    }
}

```

测试

```java
public class MyTest {
    @Test
    public void test01(){
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        //注意点：动态代理 代理的是 接口(不要写成实现类)
        UserService bean = (UserService) context.getBean("userService");
        bean.select();
    }
}
```

输出结果：

 ![x](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210802205550.png)

## 12、整合Mybatis

### 12.1、mybatis-spring方式一

1. 编写数据源配置（连接驱动，账号密码等）
2. sqlSessionFactory
3. SqlSessionTemplate（**相当于SqlSession，只不过其线程更加安全**）
4. 需要给接口加实现类【new】
5. 将自己写的实现类，注入到spring中
6. 测试！

**数据源：**

- Database:使用Spring的数据替换Mybatis的配置
- 这里使用Spring提供的JDBC：org.springframework.jdbc.datasource
- 其他数据源： c3p0 dbcp druid

【核心对象】

- sqlSessionFactory

  在基础的 MyBatis 用法中，是通过 `SqlSessionFactoryBuilder` 来创建 `SqlSessionFactory` 的。 而在 MyBatis-Spring 中，则使用 `SqlSessionFactoryBean` 来创建。

  文档：http://mybatis.org/spring/zh/factorybean.html

- `sqISessionTemplate`

  `SqlSessionTemplate` 是 MyBatis-Spring 的核心。作为 `SqlSession` 的一个实现，这意味着可以使用它无缝代替你代码中已经在使用的 `SqlSession`。`SqlSessionTemplate` 是线程安全的，可以被多个 DAO 或映射器所共享使用。

  当调用 SQL 方法时（包括由 `getMapper()` 方法返回的映射器中的方法），`SqlSessionTemplate` 将会保证使用的 `SqlSession` 与当前 Spring 的事务相关。此外，它管理 session 的生命周期，包含必要的关闭、提交或回滚操作。另外，它也负责将 MyBatis 的异常翻译成 Spring 中的 `DataAccessExceptions`。

  由于模板可以参与到 Spring 的事务管理中，并且由于其是线程安全的，可以供多个映射器类使用，你应该**总是**用 `SqlSessionTemplate` 来替换 MyBatis 默认的 `DefaultSqlSession` 实现。在同一应用程序中的不同类之间混杂使用可能会引起数据一致性的问题。

  可以使用 `SqlSessionFactory` 作为构造方法的参数来创建 `SqlSessionTemplate` 对象。

  文档：http://mybatis.org/spring/zh/sqlsession.html

  ![image-20210804220050925](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210804220052.png)

先导入jar包

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>spring-study</artifactId>
        <groupId>com.fafa</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>spring-10-mybatis</artifactId>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.47</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.3</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.2.0.RELEASE</version>
        </dependency>
        <!--Spring操作数据库的话，需要一个spring-jdbc-->
        <!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.2.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.4</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>2.0.3</version>
        </dependency>

        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.10</version>
        </dependency>
    </dependencies>
    <!--在build中配置resources，来防止资源导出失败的问题-->
    <!-- Maven解决静态资源过滤问题 -->
    <build>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <!--<filtering>false</filtering>-->
                <filtering>true</filtering>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <!--<filtering>true</filtering>-->
                <filtering>false</filtering>
            </resource>
        </resources>
    </build>

</project>
```

**代码步骤：**

pojo实体类 User：

```java
package com.fafa.pojo;


public class User {
    private int id;
    private String name;
    private String pwd;

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
        return "User{" +
            "id=" + id +
            ", name='" + name + '\'' +
            ", pwd='" + pwd + '\'' +
            '}';
    }
}

```

mapper目录下的 UserMapper、UserMapperImpl、UserMapper.xml

接口UserMapper：

```java
public interface UserMapper {
    //获取所有用户信息
    public List<User> getAllUser();
}
```

UserMapperImpl

```java
public class UserMapperImpl implements UserMapper {
    //我们的所有操作，都使用sqlSession来执行在原来，现在都使用SqlSessionTemplate；因为他的线程是安全的
    private SqlSession sqlSession;

    public void setSqlSession(SqlSession sqlSession) {
        this.sqlSession = sqlSession;
    }

    public List<User> getAllUser() {
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        return mapper.getAllUser();
    }
}

```

UserMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace=绑定一个对应的Dao/Mapper接口 -->
<mapper namespace="com.fafa.mapper.UserMapper">
    <!--select查询语句-->
    <select id="getAllUser" resultType="user">
        select * from mybatis.user;
    </select>
</mapper>
```

resource目录下的 mybatis-config.xml、spring-dao.xml、applicationContext.xml

mybatis-config.xml：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--mybatis核心配置文件-->
<configuration>
    <!--起一个别名-->
    <typeAliases>
        <typeAlias type="com.fafa.pojo.User" alias="user"/>
    </typeAliases>
</configuration>
```

spring-dao.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--DataSource:使用Spring的数据源来替换Mybatis的位置 c3p0 dbcp druid
    我们这里使用Spring提供的JDBC:org.springframework.jdbc.datasource
        -->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">

        <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
        <property name="url"
                  value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=utf-8"/>
        <property name="username" value="root"/>
        <property name="password" value="root"/>
    </bean>

    <!--SqlSession-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <!--绑定Mybatis配置文件-->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
        <property name="mapperLocations" value="classpath:com/fafa/mapper/*.xml"/>
    </bean>
    <!--SqlSessionTemplate:就是我们使用的sqlSession-->
    <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
        <!--只能使用构造器注入sqlSessionFactory，因为他没有set方法-->
        <constructor-arg index="0" ref="sqlSessionFactory"/>
    </bean>

</beans>
```

applicationContext.xml:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--导入其他配置资源-->
    <import resource="spring-dao.xml"/>
    <!--注册方式一的-->
    <bean id="userMapper" class="com.fafa.mapper.UserMapperImpl">
        <property name="sqlSession" ref="sqlSession"/>
    </bean>

    <!--注册方式二的（了解）-->
    <bean id="userMapper2" class="com.fafa.mapper.UserMapperImpl2">
        <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
    </bean>

</beans>
```

测试类

```java
public class MyTest {
    /*纯Mybatis的方式*/
    @Test
    public void test01(){
        SqlSession sqlSession = MybatisUtil.getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        List<User> allUser = mapper.getAllUser();
        for (User user : allUser) {
            System.out.println(user.toString());
        }
    }
    //整合方式一
    @Test
    public void test02(){
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserMapper userMapper = (UserMapper) context.getBean("userMapper");
        List<User> allUser = userMapper.getAllUser();
        for (User user : allUser) {
            System.out.println(user);
        }
    }
}

```

### 12.2、整合方式二（了解即可）

- sqlSessionDaoSupport

  `SqlSessionDaoSupport` 是一个抽象的支持类，用来为你提供 `SqlSession`。调用 `getSqlSession()` 方法你会得到一个 `SqlSessionTemplate`，之后可以用于执行 SQL 方法，就像下面这样:

  ```java
  public class UserDaoImpl extends SqlSessionDaoSupport implements UserDao {
      public User getUser(String userId) {
          return getSqlSession().selectOne("org.mybatis.spring.sample.mapper.UserMapper.getUser", userId);
      }
  }
  ```

  在这个类里面，通常更倾向于使用 `MapperFactoryBean`，因为它不需要额外的代码。但是，如果你需要在 DAO 中做其它非 MyBatis 的工作或需要一个非抽象的实现类，那么这个类就很有用了。

  `SqlSessionDaoSupport` 需要通过属性设置一个 `sqlSessionFactory` 或 `SqlSessionTemplate`。如果两个属性都被设置了，那么 `SqlSessionFactory` 将被忽略。

  假设类 `UserMapperImpl` 是 `SqlSessionDaoSupport` 的子类，可以编写如下的 Spring 配置来执行设置：

  ```xml
  <!--注册方式二的（了解）-->
  <bean id="userMapper2" class="com.fafa.mapper.UserMapperImpl2">
      <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
  </bean>
  ```

  文档：http://mybatis.org/spring/zh/sqlsession.html

UserServiceImpl2.java:

```java
/*新增的创建SqlSession的方式（了解即可）*/
public class UserMapperImpl2 extends SqlSessionDaoSupport implements UserMapper {
    /*这里不需要自己在去手动定义SqlSession了*/
    public List<User> getAllUser() {
        return getSqlSession().getMapper(UserMapper.class).getAllUser();
    }
}
```

spring-dao.xml:`SqlSessionTemplate`可以不写了

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--DataSource:使用Spring的数据源来替换Mybatis的位置 c3p0 dbcp druid
        我们这里使用Spring提供的JDBC:org.springframework.jdbc.datasource
    -->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">

        <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
        <property name="url"
                  value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=utf-8"/>
        <property name="username" value="root"/>
        <property name="password" value="root"/>
    </bean>

    <!--SqlSession-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <!--绑定Mybatis配置文件-->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
        <property name="mapperLocations" value="classpath:com/fafa/mapper/*.xml"/>
    </bean>
	<!-- 方法二：SqlSessionTemplate 可以不写了-->
</beans>
```

applicationContext.xml:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--导入其他配置资源-->
    <import resource="spring-dao.xml"/>
    <!--注册方式二的（了解）-->
    <bean id="userMapper2" class="com.fafa.mapper.UserMapperImpl2">
        <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
    </bean>

</beans>
```

测试：

```java
//整合方式二
@Test
public void test03(){
    ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
    UserMapper userMapper = (UserMapper) context.getBean("userMapper2");
    List<User> allUser = userMapper.getAllUser();
    for (User user : allUser) {
        System.out.println(user);
    }
}
```

## 13、声明式事务

### 13.1、回顾事务

- 把一组业务当成一个业务来做，要么都成功，要么都失败！
- 事务在项目开发中，十分的重要，涉及到数据的一致性问题
- 确保完整性和一致性

事务的ACID原则：
1、原子性
2、隔离性
3、一致性
4、持久性

ACID参考文章：https://www.cnblogs.com/melodyjerry/p/13621129.html

Spring中的事务管理

- 声明式事务：AOP
- 编程式事务：需要再代码中，进行事务管理

### **13.2、声明式事务**

先导入jar包

```xml
1<dependencies>

    <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.2.7.RELEASE</version>
    </dependency>

    <dependency>
        <groupId>org.aspectj</groupId>
        <artifactId>aspectjweaver</artifactId>
        <version>1.9.4</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.2.7.RELEASE</version>
    </dependency>

    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.2</version>
    </dependency>

    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>2.0.4</version>
    </dependency>

    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.47</version>
    </dependency>

    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.18.12</version>
    </dependency>

</dependencies>

<!--在build中配置resources，来防止资源导出失败的问题-->
<!-- Maven解决静态资源过滤问题 -->
<build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>false</filtering>
        </resource>
        <resource>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>false</filtering>
        </resource>
    </resources>
</build>
```

**代码步骤：**

pojo实体类：

```java
import lombok.Data;
import lombok.ToString;

@Data
@ToString
public class User {
    private int id;
    private String name;
    private String pwd;
    //无参构造
    public User() {
    }
    //有参构造
    public User(int id, String name, String pwd) {
        this.id = id;
        this.name = name;
        this.pwd = pwd;
    }
}

```

mapper目录下的 UserMapper、UserMapperImpl、UserMapper.xml

接口UserMapper

```java
import java.util.List;

public interface UserMapper {
    //获取全部用户
    public List<User> getAllUser();

    //添加一个用户
    public int addUser(User user);

    //删除一个用户
    public int delOneById(@Param("id") int id);
}

```

UserMapperImpl

```java
import com.fafa.pojo.User;
import org.apache.ibatis.session.SqlSession;

import java.util.List;

public class UserMapperImpl implements UserMapper {
    private SqlSession sqlSession;

    public void setSqlSession(SqlSession sqlSession) {
        this.sqlSession = sqlSession;
    }

    public List<User> getAllUser() {
        /*要在同一方法里测试才有效，不然无效*/
        User user = new User(88, "程嘉敏", "I Love U!");
        addUser(user);//添加
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        List<User> allUser = mapper.getAllUser();
        delOneById(88);//删除
        return allUser;
    }

    public int addUser(User user) {
        return sqlSession.getMapper(UserMapper.class).addUser(user);
    }

    public int delOneById(int id) {
        return sqlSession.getMapper(UserMapper.class).delOneById(id);
    }
}

```

UserMapper.xml

其中删除语句是有错误的，目的就是要测试事务

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace=绑定一个对应的Dao/Mapper接口 -->
<mapper namespace="com.fafa.mapper.UserMapper">
    <!--select查询语句-->
    <select id="getAllUser" resultType="user">
        select * from mybatis.user;
    </select>
    <!--插入语句-->
    <insert id="addUser" parameterType="user">
        insert into mybatis.user (id,name,pwd) values (#{id},#{name},#{pwd});
    </insert>
    <!--删除用户-->
    <delete id="delOneById" parameterType="_int">
        deletes from mybatis.user where id = #{id};
    </delete>

</mapper>
```

resource目录下的mybatis-config.xml、spring-dao.xml、applicationContext.xml

mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--mybatis核心配置文件-->
<configuration>
    <!--起一个别名-->
    <typeAliases>
        <typeAlias type="com.fafa.pojo.User" alias="user"/>
    </typeAliases>

</configuration>
```

spring-dao.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/tx
                           https://www.springframework.org/schema/tx/spring-tx.xsd
                           http://www.springframework.org/schema/aop
                           https://www.springframework.org/schema/aop/spring-aop.xsd">
    <!--DataSource:使用Spring的数据源来替换Mybatis的位置 c3p0 dbcp druid
        我们这里使用Spring提供的JDBC:org.springframework.jdbc.datasource
    -->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
        <property name="url"
                  value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=utf-8"/>
        <property name="username" value="root"/>
        <property name="password" value="root"/>
    </bean>

    <!--SqlSession-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <!--绑定Mybatis配置文件-->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
        <property name="mapperLocations" value="classpath:com/fafa/mapper/*.xml"/>
    </bean>
    <!--获取SqlSession-->
    <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
        <constructor-arg name="sqlSessionFactory" ref="sqlSessionFactory"/>
    </bean>

    <!--配置·声明式事务(AOP的方式)-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <!--<constructor-arg ref="dataSource"/>-->
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <!--结合AOP，实现事物的织入-->
    <!--1.配置事务通知-->
    <tx:advice id="txAdvice" transaction-manager="transactionManager">
        <!--给那些方法配置事务-->
        <!--配置事务的传播特性  new propagation -->
        <tx:attributes>
            <tx:method name="*" propagation="REQUIRED"/>
        </tx:attributes>
    </tx:advice>
    <!--配置事务切入-->
    <aop:config>
        <!--切入点-->
        <aop:pointcut id="txPointCut" expression="execution(* com.fafa.mapper.*.*(..))"/>
        <!--环绕执行-->
        <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"/>
    </aop:config>
</beans>
```

applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--导入其他配置资源-->
    <import resource="spring-dao.xml"/>
    <!--注册方式一-->
    <bean id="userMapper" class="com.fafa.mapper.UserMapperImpl">
        <property name="sqlSession" ref="sqlSession"/>
    </bean>

</beans>
```

测试类

```java
public class MyTest {
    //测试事务（ACID原则）
    @Test
    public void test01(){
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserMapper mapper = context.getBean("userMapper", UserMapper.class);
        List<User> allUser = mapper.getAllUser();
        for (User user : allUser) {
            System.out.println(user);
        }
    }
}

```



**思考：**
为什么需要事务？

- 如果不配置事务，可能存在数据提交不一致的情况下；
- 如果不在spring中去配置声明式事务，我们就需要在代码中手动配置事务！
- 事务在项目的开发中非常重要，涉及到数据的一致性和完整性问题！
