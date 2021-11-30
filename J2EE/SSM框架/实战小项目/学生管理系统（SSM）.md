# 学生管理系统（SSM）

## 1、搭建项目

> <font color='red'>创建项目</font>

创建一个maven项目，使用webapp模板

> <font color='red'>导入Maven相关依赖</font>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
    <spring.version>5.2.2.RELEASE</spring.version>
    <jackson.version>2.10.1</jackson.version>
    <mapstruct.version>1.4.0.Final</mapstruct.version>
</properties>

<dependencies>
    <!--Spring + SpringMVC-->
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <!--参数校验-->
    <!-- https://mvnrepository.com/artifact/org.hibernate/hibernate-validator -->
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-validator</artifactId>
        <version>6.0.18.Final</version>
    </dependency>
    <!--@RequestBody jackson-->
    <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>${jackson.version}</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.datatype/jackson-datatype-jdk8 -->
    <dependency>
        <groupId>com.fasterxml.jackson.datatype</groupId>
        <artifactId>jackson-datatype-jdk8</artifactId>
        <version>${jackson.version}</version>
    </dependency>
    <dependency>
        <groupId>com.fasterxml.jackson.datatype</groupId>
        <artifactId>jackson-datatype-jsr310</artifactId>
        <version>${jackson.version}</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.module/jackson-module-parameter-names -->
    <dependency>
        <groupId>com.fasterxml.jackson.module</groupId>
        <artifactId>jackson-module-parameter-names</artifactId>
        <version>${jackson.version}</version>
    </dependency>
    <!-- 切面事务 包含aspectjweaver（aspectjrt.jar）+ spring-jdbc + spring-tx -->
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-aspects -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-aspects</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <!--缓存、定时任务-->
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-context-support -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context-support</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <!--Spring的单元测试-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>${spring.version}</version>
        <scope>test</scope>
    </dependency>
    <!--mybatis相关依赖-->
    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>1.3.1</version>
    </dependency>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.4.5</version>
    </dependency>
    <!--数据库连接池 用到的是 HikariCP -->
    <!-- https://mvnrepository.com/artifact/com.zaxxer/HikariCP -->
    <dependency>
        <groupId>com.zaxxer</groupId>
        <artifactId>HikariCP</artifactId>
        <version>3.4.1</version>
    </dependency>
    <!--数据库连接驱动-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.49</version>
    </dependency>
    <!--日志 这个包含log4j-->
    <!-- https://mvnrepository.com/artifact/ch.qos.logback/logback-classic -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.2.3</version>
        <scope>compile</scope>
    </dependency>

    <!--servlet-api 和 jsp-api-->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>4.0.0</version>
        <scope>provided</scope>
    </dependency>
    <!--这个如果不使用jsp的自定义属性，可以不导入-->
    <!-- https://mvnrepository.com/artifact/javax.servlet.jsp/javax.servlet.jsp-api -->
    <dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>javax.servlet.jsp-api</artifactId>
        <version>2.3.3</version>
        <scope>provided</scope>
    </dependency>

    <!--jstl（包含standard.jar）-->
    <dependency>
        <groupId>jstl</groupId>
        <artifactId>jstl</artifactId>
        <version>1.2</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>jstl</artifactId>
        <version>1.2</version>
    </dependency>
    <!--lombok-->
    <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.18.10</version>
        <scope>provided</scope>
    </dependency>
    <!--mapstruct 进行转化的-->
    <!-- https://mvnrepository.com/artifact/org.mapstruct/mapstruct -->
    <dependency>
        <groupId>org.mapstruct</groupId>
        <artifactId>mapstruct</artifactId>
        <version>${mapstruct.version}</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.mapstruct/mapstruct-processor -->
    <dependency>
        <groupId>org.mapstruct</groupId>
        <artifactId>mapstruct-processor</artifactId>
        <version>${mapstruct.version}</version>
    </dependency>
    <!--单元测试-->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
</dependencies>

<!--静态资源导出问题-->
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

> <font color='red'>Spring的配置（applicationContext.xml）</font>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:tx="http://www.springframework.org/schema/tx" xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context
                           http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/aop
                           http://www.springframework.org/schema/aop/spring-aop.xsd
                           http://www.springframework.org/schema/tx
                           http://www.springframework.org/schema/tx/spring-tx.xsd">
    <!--@Service等注解配置bean，扫描根目录-->
    <context:component-scan base-package="com.fafa.student">
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>
    <!--加载自定义配置到spring环境中-->
    <context:property-placeholder location="classpath:db.properties"/>
    <!--配置数据源  c3p0 druid 都可以  这里使用 Hikari
    destroy-method 是 销毁方式
    -->
    <bean id="datasource" class="com.zaxxer.hikari.HikariDataSource" destroy-method="close">
        <property name="driverClassName" value="${jdbc.driver}"/>
        <property name="jdbcUrl" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>

        <!--单位：ms，从连接池获取到连接的超时时间-->
        <property name="connectionTimeout" value="${jdbc.connectionTimeout}"/>
        <!--单位：个，连接池里面最少有5个连接可用-->
        <property name="minimumIdle" value="${jdbc.minimumIdle}"/>
        <!--单位：个，连接池里面最多有多少个数据库的连接-->
        <property name="maximumPoolSize" value="${jdbc.maximumPoolSize}"/>
        <!--单位：ms，默认就是10min，一个连接在池子里面如果10min后还没有被使用的话，那么就会把它释放掉（>minimumIdle）-->
        <property name="idleTimeout" value="${jdbc.idleTimeout}"/>
        <!--单位：ms，默认就是30min，一个连接最多存活30min,
        show variable like '%wait_timeout%'(8h) mysql默认最大连接时间是8小时，超时会单方面取消连接
        -->
        <property name="maxLifetime" value="${jdbc.maxLifetime}"/>
    </bean>
    <!--配置mybatis-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="datasource"/>
        <property name="mapperLocations" value="classpath:mybatis/mapper/*.xml"/>
        <property name="configLocation" value="classpath:mybatis/mybatis-config.xml"/>
    </bean>
    <!--自动扫描-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <!--注入SqlSessionFactory-->
        <property name="basePackage" value="com.fafa.student.mapper"/>
        <!--假如有多个数据圆的时候可以通过该属性指定，现在就一个也可以不配置-->
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
    </bean>
    <!--事务配置-->
    <bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="datasource"/>
    </bean>
    <!--配置通知:配置你要做什么事情，拦截后的执行的规则-->
    <tx:advice transaction-manager="txManager" id="txAdvice">
        <tx:attributes>
            <tx:method name="*" propagation="REQUIRED" isolation="DEFAULT"/>
            <!--不添加事务的-->
            <tx:method name="get*" read-only="true"/>
            <tx:method name="find*" read-only="true"/>
            <tx:method name="select*" read-only="true"/>
            <tx:method name="query*" read-only="true"/>
            <tx:method name="list*" read-only="true"/>
        </tx:attributes>
    </tx:advice>
    <!--aop 对谁做 切入点-->
    <aop:config>
        <!--配置切入点  第一个 * 代表任意返回值-->
        <aop:pointcut id="pointcut"
                      expression="execution(* com.fafa.student.service..*Service.*(..))"/>
        <!--配置增强器 advisor:advice+pc-->
        <aop:advisor advice-ref="txAdvice" pointcut-ref="pointcut"/>
    </aop:config>
    <!--配置spring生成代理的方式，默认就是jdk-->
    <!--<aop:aspectj-autoproxy proxy-target-class="true"/>-->
</beans>
```

> <font color='red'>mybatis配置（mybatis-config.xml）</font>

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <settings>
        <!--下划线转驼峰：student_name == studentName-->
        <setting name="mapUnderscoreToCamelCase" value="true"/>
        <!--开启日志-->
        <setting name="logImpl" value="SLF4J"/>
        <!--列值为null是否调用bean的set或者map的put-->
        <setting name="callSettersOnNulls" value="true"/>
    </settings>
    <!--别名-->
    <typeAliases>
        <package name="com.fafa.student.pojo"/>
    </typeAliases>
</configuration>
```

> <font color='red'>数据库的连接信息(db.properties)</font>

```properties
jdbc.driver = com.mysql.jdbc.Driver
# 如果使用的是mysql 8.0 及以上的话，需要加时区设置;  &serverTimezone=Asia/Shanghai
jdbc.url = jdbc:mysql://localhost:3306/ssmbuild?useSSL=false&useUnicode=true&characterEncoding=utf8
jdbc.username = root
jdbc.password = root
jdbc.connectionTimeout = 30000
jdbc.minimumIdle = 5
jdbc.maximumPoolSize = 10
jdbc.idleTimeout = 600000
jdbc.maxLifetime = 1800000
```

> <font color='red'>Logback配置（简写版的）</font>

放在resources的目录下即可（logback.xml）

```xml
<?xml version="1.0" encoding="UTF-8"?>

<configuration scan="false">

    <!--定义日志文件的存储地址 勿在 LogBack 的配置中使用相对路径-->
    <property name="LOG_HOME" value="${user.home}/ssm-student" />

    <!--控制台日志， 控制台输出 -->
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <!--格式化输出：%d表示日期，%thread表示线程名，%-5level：级别从左显示5个字符宽度,%msg：日志消息，%n是换行符-->
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{50} - %msg%n</pattern>
            <charset>UTF-8</charset>
        </encoder>
    </appender>

    <!-- show parameters for hibernate sql 专为 Hibernate 定制
     mapper包打印执行的sql，需要日志级别为DEBUG -->
    <logger name="com.fafa.student.mapper" level="debug" additivity="false">
        <appender-ref ref="stdout"/>
    </logger>

    <!-- 日志输出级别 -->
    <root level="INFO">
        <appender-ref ref="STDOUT" />
    </root>

</configuration>
```

> <font color='red'>springmvc配置</font>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/mvc
                           https://www.springframework.org/schema/mvc/spring-mvc.xsd
                           http://www.springframework.org/schema/context
                           https://www.springframework.org/schema/context/spring-context.xsd">

    <!--SpringMVC扫描的根目录-->
    <context:component-scan base-package="com.fafa.student.controller"
                            use-default-filters="false">
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>

    <!--注册RequestMappingHandlerMapping 和 RequestMappingHandlerAdapter 等重要组件，
        AnnotationDrivenBeanDefinitionParser
        十分重要！！！
    -->
    <mvc:annotation-driven/>
    <!--配置静态资源-->
    <!--2.静态资源过滤  图片，视频，html等等，具体看笔记-->
    <!--方式一-->
    <!--<mvc:default-servlet-handler/>-->
    <!--方式二
      location:webapp 下的路径 mapping：访问路径
      resources/img === a/img
    -->
    <mvc:resources mapping="/resources/**" location="/resources/" cache-period="0"/>

    <!--配置视图解析器，这里配置的jsp的视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>

    <!--文件上传-->

    <!--拦截器-->

</beans>
```

> <font color='red'>web.xml</font>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--监听servlet容器的启动，加载spring的配置文件-->
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    <!--默认从/WEB-INF/applicationContext.xml加载spring的配置文件-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <!--classpath:从类路径下面找，classpath:* 除了本应用的类路径，还包含jar包里面的-->
        <param-value>classpath:applicationContext.xml</param-value>
    </context-param>

    <!--配置字符编码过滤问题-->
    <filter>
        <filter-name>charEncoding</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        <init-param>
            <param-name>forceEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>charEncoding</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <!--配置springMVC的核心转发servlet   DispatchServlet-->
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!--默认从/WEB-INF/springmvc-servlet.xml加载spring的配置文件-->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
        <!--当值大于或者等于0时：容器启动时就会实例化这个servlet
        否则（小于0）：使用这个servlet的时候才会去实例化-->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

</web-app>
```

## 2、前端资源引入

![image-20210821091855782](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210821091903.png)

> <font color='red'>index.jsp</font>

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>Index</title>
    </head>

    <%--EL 表达式的形式--%>
    <%--引入css--%>
    <link rel="stylesheet" href="${pageContext.request.contextPath}/resources/gijgo/css/gijgo.css"/>
    <link rel="stylesheet" href="${pageContext.request.contextPath}/resources/bs4.6.0/css/bootstrap.css"/>
    <%--引入js--%>
    <script src="${pageContext.request.contextPath}/resources/jquery/jQuery.js"></script>
    <%--bundle包含了bootstrap.js以及bootstrap本身依赖的第三方库 比如proper--%>
    <script src="${pageContext.request.contextPath}/resources/bs4.6.0/js/bootstrap.bundle.min.js"></script>
    <script src="${pageContext.request.contextPath}/resources/gijgo/js/gijgo.js"></script>
    <%--国际化--%>
    <script src="${pageContext.request.contextPath}/resources/gijgo/js/messages/messages.zh-cn.js"></script>
    <body>
        <button class="btn btn-danger">危险</button>
    </body>
</html>
```

> <font color='red'>测试</font>

![image-20210821092231755](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210821092231.png)

<font color='green'>ok！</font>

## 3、学生表的创建

```mysql
create database ssm_student CHARACTER SET utf8;
use ssm_student;
create table `student`(
    `id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '主键',
    `no` varchar(20) NOT NULL COMMENT '学号',
    `real_name` varchar(20) NOT NUll COMMENT '姓名',
    `birth_day` date NOT NUll COMMENT '出生日期',
    `phone` varchar(15) NOT NUll COMMENT '联系电话',
    `email` varchar(30) NOT NUll COMMENT '邮箱',
    `photo_path` varchar(200) DEFAULT 'resources/imgs/plus.png' COMMENT '个人免冠照存放路径',
    PRIMARY KEY(`id`)
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

![1](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210821113250.png)

## 4、头部和尾部的布局

- 头部（top.jsp）

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
      <head lang="zh-cn">
          <title>top页面</title>
          <%--EL 表达式的形式--%>
          <%--引入css--%>
          <link rel="stylesheet" href="${pageContext.request.contextPath}/resources/gijgo/css/gijgo.css"/>
          <link rel="stylesheet" href="${pageContext.request.contextPath}/resources/bs4.6.0/css/bootstrap.css"/>
          <link rel="stylesheet" href="${pageContext.request.contextPath}/resources/bs4.6.0/css/bootstrap-grid.css"/>
          <link rel="stylesheet" href="${pageContext.request.contextPath}/resources/bs4.6.0/css/bootstrap-reboot.css"/>
          <%--引入js--%>
          <script src="${pageContext.request.contextPath}/resources/jquery/jQuery.js"></script>
          <%--bundle包含了bootstrap.js以及bootstrap本身依赖的第三方库 比如proper--%>
          <script src="${pageContext.request.contextPath}/resources/bs4.6.0/js/bootstrap.bundle.min.js"></script>
          <script src="${pageContext.request.contextPath}/resources/bs4.6.0/js/bootstrap.js"></script>
          <script src="${pageContext.request.contextPath}/resources/gijgo/js/gijgo.js"></script>
          <%--国际化--%>
          <script src="${pageContext.request.contextPath}/resources/gijgo/js/messages/messages.zh-cn.js"></script>
          <%--引入common.js--%>
          <script src="${pageContext.request.contextPath}/resources/js/common.js"></script>
      </head>
      <body>
          <div class="row my-4">
              <%--布局logo图片--%>
              <div class="col-sm-10 pr-0">
                  <img src="${pageContext.request.contextPath}/resources/imgs/logo.png" class="img-fluid">
              </div>
              <div class="col-sm-2 d-flex justify-content-center align-items-center"
                   style="background: #0062cc">
                  <a href="#" class="btn btn-outline-warning border-0">退出</a>
              </div>
              <%--提示框开始--%>
              <!-- Modal -->
              <div class="modal fade" data-backdrop="static" tabindex="-1" id="tipModal">
                  <div class="modal-dialog modal-dialog-centered modal-sm">
                      <div class="modal-content">
                          <div class="modal-header">
                              <h5 class="modal-title">提示信息</h5>
                              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                                  <span aria-hidden="true">&times;</span>
                              </button>
                          </div>
                          <div class="modal-body" id="tipCont"></div>
                          <div class="modal-footer">
                              <button type="button" class="btn btn-primary" data-dismiss="modal">确认</button>
                          </div>
                      </div>
                  </div>
              </div>
              <%--提示框结束--%>
          </div>
      </body>
  </html>
  ```

- 尾部(bottom.jsp)

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
      <head lang="zh-cn">
          <title>bottom页面</title>
          <style>
              #bottom{
                  position: fixed;
                  left: 0;
                  right:0;
                  bottom: 10px;
                  margin-left: 800px;
                  margin-right: auto;
                  width: 470px;
                  color: #999;
                  font-size: 14px;
              }
          </style>
      </head>
      <body>
          <div class="row my-4">
              <div class="col-sm-12" id="bottom">
                  Copyright 可爱发出品 <span style="color: red">http:www.keaifa.com</span>
              </div>
          </div>
      </body>
  </html>
  
  ```

  ![image-20210822090523179](https://raw.githubusercontent.com/keaifafafa/IO/master/img/pic/20210822090530.png)

## 5、添加学生页面布局及前端验证

> <font color='red'>add.jsp</font>

```jsp
<%@page import="java.util.List" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head lang="zh-cn">
        <title>学生管理页面</title>
        <style>

        </style>
    </head>
    <body>
        <div class="container">
            <%--引入头部--%>
            <jsp:include page="../../top.jsp"/>
            <div class="row">
                <section class="col-sm-4 offset-sm-4">
                    <%--这里是使用ajax进行提交的--%>
                    <form id="addForm" novalidate>
                        <%--表单项--%>
                        <div class="form-group">
                            <label for="no">
                                学号：
                            </label>
                            <input type="text" class="form-control" name="no" id="no" required/>
                            <%-- bootstrap里写好的类 直接调用即可 --%>
                            <div class="invalid-feedback">学号不能为空</div>
                        </div>
                        <div class="form-group">
                            <label for="realName">
                                姓名：
                            </label>
                            <input type="text" class="form-control" name="realName" id="realName" autocomplete="off" required/>
                            <div class="invalid-feedback">姓名不能为空</div>
                        </div>
                        <div class="form-group">
                            <label for="birthDay">
                                生日：
                            </label>
                            <input type="date" class="form-control" name="birthDay" id="birthDay" required/>
                            <div class="invalid-feedback">生日不能为空</div>
                        </div>
                        <div class="form-group">
                            <label for="phone">
                                手机：
                            </label>
                            <input type="text" class="form-control" name="phone" id="phone" autocomplete="off" required/>
                            <div class="invalid-feedback">手机号不能为空</div>
                        </div>
                        <div class="form-group">
                            <label for="email">
                                邮箱：
                            </label>
                            <input type="email" class="form-control" name="email" id="email" required/>
                            <div class="invalid-feedback">请输入合法的邮箱</div>
                        </div>
                        <div class="d-flex justify-content-around">
                            <input type="button" onclick="doAddStudent()" class="btn btn-primary" value="提交"/>
                            <input type="reset" class="btn btn-warning" value="重置">
                            <a href="${pageContext.request.contextPath}/admin/toStudentManage" class="btn btn-info">返回</a>
                        </div>
                    </form>
                </section>
            </div>
            <%--引入尾部--%>
            <jsp:include page="../../bottom.jsp"/>
        </div>
    </body>
    <script>
        <%--前端校验--%>
        function doAddStudent() {
            /*
        1.form表单 加上 novalidate
        2.在form表单项上写上校验规则及其对应的提示信息
        3.在提交表单时进行校验并加上相应的css类
        * */
            //checkValidity是js原生的 不是jquery的
            // checkValidity方法可以用来验证当前表单控件元素，或者整个表单是否验证通过，返回值是布尔值，true或者false。
            var flag = document.getElementById("addForm").checkValidity();
            //添加css样式  我已经校验过了
            $("#addForm").addClass("was-validated");
            //校验不通过
            if (!flag) {
                return;
            }
            //提交数据到后台
            //获取数据 并且写成json格式
            //封装通用的获取表单数据的方法
            var obj = formDataObj("#addForm");
            //使用ajax进行提交
            $.ajax({
                url: "${pageContext.request.contextPath}/admin/addStu",
                type: "post",
                data: obj,
                success: function (result) {
                    /*alert(result);*/
                    $("#tipCont").text(result);
                    $("#tipModal").modal("show");
                }
            })
        }
    </script>
</html>
```

> <font color='red'>common.js</font>

```javascript
/*
* 获取from表单项的值 并封装为 JSON对象返回
*
*  contentType="application/x-www-form-urlencoded"---data:json对象---req.getParameter("")
*  contentType="application/json"---data:JSON.stringify(json对象)---req.getInputStream(@RequestBody)
* */
function formDataObj(selector) {
    //封装通用的获取表单数据的方法
    var arr = $(selector).serializeArray();
    var retObj = {};
    $.each(arr,function (i,ele) {
        if(retObj[ele["name"]]){
            retObj[ele["name"]] += "," + ele["value"];
        }else{
            retObj[ele["name"]] = ele["value"];
        }
    });
    return retObj;
}
```



> <font color='red'>**注意点**</font>

这里要注意：模态框的使用，那个提交按钮，不要写成submit的类型，写成button  不然一出现就消失！

## 6、学生管理页面布局

> <font color='red'>manage.jsp</font>

```jsp
<%@page import="java.util.List" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head lang="zh-cn">
        <title>学生管理页面</title>
        <style>

        </style>
    </head>
    <body>
        <div class="container">
            <%--引入头部--%>
            <jsp:include page="../../top.jsp"/>

            <div class="row">
                <%--布局管理页员 toolbar 顶部工具栏  这里的 section 和 div 作用 差不多--%>
                <section class="col-sm-12 mb-2">
                    <%-- 为了将三个按钮凑到同一行 --%>
                    <div class="d-flex justify-content-start align-items-center">
                        <a href="${pageContext.request.contextPath}/admin/toStudentAdd" class="btn btn-primary mr-3">
                            新增
                        </a>
                        <a href="#" class="btn btn-danger mr-3">
                            删除
                        </a>
                        <%--这里的form 默认mb是不等于0的 --%>
                        <form action="#" class="form-inline mb-0">
                            <input type="text" class="form-control mr-3" name="realName" placeholder="请输入用户名"/>
                            <input type="button" class="btn btn-info" value="查询"/>
                        </form>
                    </div>
                </section>
            </div>
            <%--引入尾部--%>
            <jsp:include page="../../bottom.jsp"/>
        </div>
    </body>
</html>
```

## 7、
