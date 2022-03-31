## 写在前面

今天，和一位前辈聊了聊实习的事，关于java后端开发的几个问题，真的是被虐的很惨啊（理解和能讲明白完全就是两回事啊）

其中，最沙雕的是，我竟然单纯的以为过滤器（**Filter**）和 拦截器（**Interceptor**）是一个东西，然后前辈当场就diss我一顿

后来我回家翻了翻笔记发现我在学**SpringMVC**的时候是有学过拦截器的（还注明了==重点==两个字），还将其应用到了登录验证功能上

 ![image-20220204195429856](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220204195429.png)

后来我反思了下，**SSM**学完后，直接做了一个书店系统（很简单的CRUD）就结束了，然后就直接==SpringBoot==了，

在里面是直接用的==SpringSecurity==进行的权限限制，渐渐地我就把==拦截器==给忘记了，

至于为啥把他当做过滤器，那是因为在学==JavaWeb==时确实把过滤器当做拦截器用过（比如登录功能）

至于为什么能那么写，就请耐心的看我接下来的内容吧（嘿嘿）

 ![image-20220204200015298](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220204200015.png)

## 一、什么是过滤器（Filter）

过滤器，顾名思义就是起到过滤筛选作用的一种事物，只不过相较于现实生活中的过滤器，这里的过滤器过滤的对象是客户端访问的web资源，

也可以理解为一种预处理手段，对资源进行拦截后，将其中我们认为的杂质（用户自己定义的）过滤，符合条件的放行，不符合的则拦截下来。

 ![image-20220204202844297](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220204202844.png)

### 1.1、过滤器常见的使用场景

- 统一设置编码
- 过滤敏感字符
- 登录校验
- URL级别的访问权限控制
- 数据压缩

### 1.2、Springboot 整合过滤器

- #### Bean注入方式

  > ==编写Filter==

  ```java
  public class HeFilter implements Filter {
      @Override
      public void init(FilterConfig filterConfig) throws ServletException {
      }
  
      @Override
      public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)throws IOException, ServletException {
          System.out.println("您已进入filter过滤器，您的请求正常，请继续遵规则...");
          chain.doFilter(request, response);
      }
  
      @Override
      public void destroy() {
      }
  }
  ```

  > ==编写Filter配置类==

  ```java
  @Configuration
  public class ServletConfig {
      @Bean
      public FilterRegistrationBean heFilterRegistration() {
          FilterRegistrationBean registration = new FilterRegistrationBean(new HeFilter());
          registration.addUrlPatterns("/*");
          return registration;
      }
  }
  ```

- 注解方式

  ```java
  @Slf4j
  @Component
  // filterName就是当前类名称，还有一个urlPattens的参数，这个参数表示要过滤的URL上的后缀名，是多参数，可以用数组表示。
  @WebFilter(value = "/hello") 或 (filterName = "f1", urlPatterns = {"*.html","*.jsp","/hello"})
  public class HelloFilter2 implements Filter {
  
      @Override
      public void init(FilterConfig filterConfig) throws ServletException {
  
      }
  
      @Override
      public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse,
                           FilterChain filterChain) throws IOException, ServletException {
          log.info("进入到过滤器2啦");
          // 这里可以进行一些条件判断（假如要做登录验证的话）
          filterChain.doFilter(servletRequest,servletResponse);
      }
  
      @Override
      public void destroy() {
  
      }
  }
  ```

  

  > 在主启动类上加@ServletComponentScan("com.pandy.blog.filters")   指明filter所在位置的包。 若有多个filter，默认根据filter类名的字母倒叙排列，且@WebFilter注解方式的过滤器优先级高于Bean注入方式配置的过滤器

### 1.3、过滤器（Filter）详解

a) Filter是依赖于Servlet的，需要有Servlet的依赖。

b) init() 在容器初始化时执行，只执行一次。

c) doFilter() 目标请求之前拦截执行，拦截之后需要放行才开始执行目标方法。filterChain.doFilter(servletRequest,servletResponse);

d) destroy() 在容器销毁时执行，只执行一次。

e) Filter可以拦截所有请求。包括静态资源[css，js...]。

f) 基于函数回调实现。

g) 过滤器只能在容器初始化时被调用一次。

## 二、什么是拦截器（Interceptor）

> ==概念==

拦截器是springmvc提供的，类似于过滤器。主要用于拦截用户请求并作相应的处理。

 ![image-20220204205945784](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220204205945.png)

### 2.1、拦截器的使用场景

a) 日志记录

b) 权限校验

c) 登录校验

d) 性能检测[检测方法的执行时间]

==其实拦截器和过滤器很像，有些使用场景。无论选用谁都能实现。需要注意的使他们彼此的使用范围，触发机制。==

### 2.2、springboot整合拦截器

- 编写自定义拦截器类实现HandlerInterceptor接口或继承其子类【推荐实现的方式，实现可以自动生成preHandle..】

  ```java
  @Component
  public class InterceptorDemo implements HandlerInterceptor {
      @Override
      public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
          System.out.println("拦截器preHandle在控制器方法执行前执行");
          //true：表示放行
          return true;
      }
  
      @Override
      public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
          System.out.println("拦截器postHandle在控制器方法执行后执行");
      }
  
      @Override
      public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
          System.out.println("拦截器afterCompletion在请求完成后执行");
      }
  }
  ```

-  基于springmvc编写配置类

  ```java
  @Configuration
  // 老版本呢是继承WebMvcConfigurerAdapter不过新版本已经放弃了，推荐用下面的方式。
  public class InterceptorConfig implements WebMvcConfigurer { 
  
      @Autowired
      private InterceptorDemo interceptorDemo;
  
      @Override
      public void addInterceptors(InterceptorRegistry registry) {
          // ** 表示所有拦截路径
          registry.addInterceptor(interceptorDemo).addPathPatterns("/**");
          // 或下面这种写法  【若编写自定义拦截器类没有加@Component注解】
          registry.addInterceptor(new InterceptorDemo()).addPathPatterns("/**");
      }
  }
  
  ```

### 2.3、拦截器详情

  a) 拦截器是依赖于SpringMVC的，需要有mvc的依赖。

  b) preHandle() 在目标请求完成之前执行。有返回值Boolean类型，true：表示放行

  c) postHandle() 在目标请求之完成后执行。

  d) afterCompletion() 在整个请求完成之后【modelAndView已被渲染执行】。

  e) 拦截器只能拦截==action==请求。不包括静态资源==[css，js...]==。

  f) 基于java==反射机制==实现。

  g) 在拦截器的生命周期中，可以==多次==被调用。

```java
关于拦截器的preHandle()方法的参数说明：
      public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler){
      
      }

      @param request        current HTTP request
      @param response       current HTTP response
      @param handler        chosen handler to execute, for type and/or instance evaluation   //选择要执行的处理程序，用于类型和/或实例计算
```

## 三、拦截器与过滤器的区别

> ==一张图告诉你答案==

 ![image-20220204211710166](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220204211710.png)

1、过滤器和拦截器触发时机不一样，过滤器是在请求进入容器后，但请求进入servlet之前进行预处理的。请求结束返回也是，是在servlet处理完后，返回给

前端之前。

2、拦截器可以获取IOC容器中的各个bean，而过滤器就不行，因为拦截器是spring提供并管理的，spring的功能可以被拦截器使用，在拦截器里注入一个

service，可以调用业务逻辑。而过滤器是JavaEE标准，只需依赖servlet api ，不需要依赖spring。

3、过滤器的实现基于回调函数。而拦截器（代理模式）的实现基于反射

4、Filter是依赖于Servlet容器，属于Servlet规范的一部分，而拦截器则是独立存在的，可以在任何情况下使用。

5、Filter的执行由Servlet容器回调完成，而拦截器通常通过动态代理（反射）的方式来执行。

6、Filter的生命周期由Servlet容器管理，而拦截器则可以通过IoC容器来管理，因此可以通过注入等方式来获取其他Bean的实例，因此使用会更方便。



【重点】过滤器和拦截器非常相似，但是它们有很大的区别:

> 最简单明了的区别就是==过滤器可以修改request，而拦截器不能== 
>
> 过滤器需要在servlet容器中实现，拦截器可以适用于javaEE，javaSE等各种环境 
>
> 拦截器可以==调用IOC容器中的各种依赖，而过滤器不能==
>
>  ==过滤器只能在请求的前后使用，而拦截器可以详细到每个方法==
>
>  ==当有过滤器和拦截器时的执行流程：==

 ![image-20220204212000434](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220204212000.png)



## 四、AOP与过滤器、拦截器的区别

> 过滤器，拦截器拦截的是URL。AOP拦截的是类的元数据(包、类、方法名、参数等)。
>
>  过滤器并没有定义业务用于执行逻辑前、后等，仅仅是请求到达就执行。 
>
> 拦截器有三个方法，相对于过滤器更加细致，有被拦截逻辑执行前、后等。 AOP针对具体的代码，能够实现更加复杂的业务逻辑。 
>
> 三者功能类似，但各有优势，从过滤器--》拦截器--》切面，拦截规则越来越细致。 执行顺序依次是过滤器、拦截器、切面。

> ==三者的使用场景==

在编写相对比较公用的代码时，优先考虑过滤器，然后是拦截器，最后是aop。

比如：

权限校验，一般情况下，所有的请求都需要做登陆校验，此时就应该使用过滤器在最顶层做校验；

日志记录，一般日志只会针对部分逻辑做日志记录，而且牵扯到业务逻辑完成前后的日志记录，因此使用过滤器不能细致地划分模块，此时应该考虑拦截器，

然而拦截器也是依据URL做规则匹配，因此相对来说不够细致，因此我们会考虑到使用AOP实现，AOP可以针对代码的方法级别做拦截，很适合日志功能。



## 写在最后

最后我也明白了，学习这事不能急躁（心急吃不了热豆腐），不然就会想我一样浅尝辄止，只懂个大概或者是概念，

这是远远不够的，Java的路还很漫长，等待着我们去探索，加油！！！

 ![image-20220204212951463](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220204212951.png)
