# Smbms超市管理系统

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200516122458676.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 

 数据库： 

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200516122532275.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 

 **项目如何搭建？**
考虑是不是用maven？ jar包，依赖 

### 1.搭建项目准备工作

1. 搭建一个maven web 项目
2. 配置Tomcat
3. 测试项目是否能够跑起来
4. 导入项目中需要的jar包;
   jsp，Servlet，mysql驱动jstl，stand…
5. 构建项目包结构

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/202005161230352.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70)

6.编写实体类
ROM映射:表-类映射

7.编写基础公共类
1、数据库配置文件（mysql5.xx和8.xx的编写有差异）

```properties
driver = com.mysql.jdbc.Driver
#在和mysql传递数据的过程中，使用unicode编码格式，并且字符集设置为utf-8
url = jdbc:mysql://localhost:3306/smbms?useSSL=false&useUnicode=true&characterEncoding=UTF-8
username = root
password = root
```

 2、编写数据库的公共类 

```java
package com.fafa.dao;

import java.io.InputStream;
import java.sql.*;
import java.util.Properties;

//操作数据库的公共类
public class BaseDao {

    private static String driver;
    private static String url;
    private static String username;
    private static String password;

    //静态代码块，类加载的时候就初始化了
    static {
        Properties properties = new Properties();
        //通过类加载器读取对应的资源
        InputStream is =
            BaseDao.class.getClassLoader().getResourceAsStream("db.properties");
        try {
            properties.load(is);
        } catch (Exception e) {
            e.printStackTrace();
        }

        driver = properties.getProperty("driver");
        url = properties.getProperty("url");
        username = properties.getProperty("username");
        password = properties.getProperty("password");
    }

    //连接数据库
    public static Connection getConnection(){
        Connection connection = null;
        try {
            Class.forName(driver);
            connection = DriverManager.getConnection(url, username, password);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return connection;
    }

    //编写查询公共方法
    public static ResultSet execute(Connection connection, String sql,ResultSet resultSet, Object []params, PreparedStatement preparedStatement) throws SQLException {
        preparedStatement = connection.prepareStatement(sql);

        for (int i = 0; i < params.length; i++) {
            //setObject，占位符从1开始 但是数组下标从0开始
            preparedStatement.setObject(i+1,params[i]);
        }
        resultSet = preparedStatement.executeQuery();
        return resultSet;
    }

    //编写增删改公共方法
    public static int execute(Connection connection,String sql,Object []params,PreparedStatement preparedStatement) throws SQLException {
        preparedStatement = connection.prepareStatement(sql);

        for (int i = 0; i < params.length; i++) {
            //setObject，占位符从1开始 但是数组下标从0开始
            preparedStatement.setObject(i+1,params[i]);
        }

        int updateRows = preparedStatement.executeUpdate();
        return updateRows;
    }

    //释放资源
    public static boolean closeResourse(Connection connection,ResultSet resultSet,PreparedStatement preparedStatement){
        boolean flag = true;

        if (resultSet != null){
            try {
                resultSet.close();
                //GC回收
                resultSet = null;
            } catch (SQLException e) {
                e.printStackTrace();
                flag = false;
            }
        }

        if (preparedStatement != null){
            try {
                preparedStatement.close();
                //GC回收
                preparedStatement = null;
            } catch (SQLException e) {
                e.printStackTrace();
                flag = false;
            }
        }

        if (connection != null){
            try {
                connection.close();
                //GC回收
                connection = null;
            } catch (SQLException e) {
                e.printStackTrace();
                flag = false;
            }
        }
        return flag;
    }

}

```

 3、编写字符编码过滤器 filter包下

```java
public class CharacterEncodingFilter implements Filter {
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        request.setCharacterEncoding("UTF-8");
        response.setCharacterEncoding("UTF-8");

        chain.doFilter(request,response);//放行
    }

    public void destroy() {

    }
}
```



8.导入静态资源

### 2.登录功能实现

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200516125301633.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 

#### 1.编写前端页面

#### 2.设置首页

1.设置欢迎首页 

```xml
 <welcome-file-list>
    <welcome-file>login.jsp</welcome-file>
  </welcome-file-list>
```

#### 3.编写dao层登录用户登录的接口

```java
//得到要登录的用户
public User getLoginUser(Connection connection,String userCode,String userPassword) throws SQLException;
}
```

#### 4.编写dao层接口的实现类

```java
package com.fafa.dao.user;

import com.fafa.dao.BaseDao;
import com.fafa.pojo.User;

import javax.xml.transform.Result;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class UserDaoImpl implements UserDao {
    public User getLoginUser(Connection connection, String userCode,String userPassword) throws SQLException {

        PreparedStatement pstm = null;
        ResultSet rs = null;
        User user = null;

        //数据库连接成功
        if (connection != null) {
            String sql = "select * from smbms_user where userCode=? and userPassword=?";
            Object[] params = {userCode,userPassword};
            rs = BaseDao.execute(connection, pstm, rs, sql, params);
            //遍历
            if (rs.next()) {
                user = new User();
                user.setId(rs.getInt("id"));
                user.setUserCode(rs.getString("userCode"));
                user.setUserName(rs.getString("userName"));
                user.setUserPassword(rs.getString("userPassword"));
                user.setGender(rs.getInt("gender"));
                user.setBirthday(rs.getDate("birthday"));
                user.setPhone(rs.getString("phone"));
                user.setAddress(rs.getString("address"));
                user.setUserRole(rs.getInt("userRole"));
                user.setCreatedBy(rs.getInt("createdBy"));
                user.setCreationDate(rs.getTimestamp("creationDate"));
                user.setModifyBy(rs.getInt("modifyBy"));
                user.setModifyDate(rs.getTimestamp("modifyDate"));
            }
            //关闭数据库  数据库连接先不用关闭，因为事务层可能还会用到
            BaseDao.closeResourse(null, pstm, rs);
        }
        return user;
    }
}

```

####   5.业务层接口

```java
//业务层接口  用户登录
public User login(String userCode,String password) throws SQLException;
```

#### 6.业务层实现类

```java
package com.fafa.service.user;

import com.fafa.dao.BaseDao;
import com.fafa.dao.user.UserDao;
import com.fafa.dao.user.UserDaoImpl;
import com.fafa.pojo.User;
import org.junit.Test;

import java.sql.Connection;
import java.sql.SQLException;

public class UserServiceImpl implements UserService {
    //业务层都会调用Dao层 所以我们要引入Dao层
    private UserDao userDao;

    public UserServiceImpl() {
        userDao = new UserDaoImpl();
    }

    public User login(String userCode, String password){
        Connection connection = null;
        User user = null;
        //连接数据库
        connection = BaseDao.getConnection();

        try {
            //调用Dao层
            user = userDao.getLoginUser(connection, userCode,password);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            //由于 PreparedStatement 和 resultset 已经在 userDao.getLoginUser 被关闭
            BaseDao.closeResourse(connection,null,null);
        }
        return user;
    }


    /*@Test
    public void test(){
        UserServiceImpl userService = new UserServiceImpl();
        User test = userService.login("test", "1111dfdsaf111");
        System.out.println(test.getBirthday());
    }*/
}

```

#### 7.编写Servlet

```java
package com.fafa.servlet.user;

import com.fafa.pojo.User;
import com.fafa.service.user.UserServiceImpl;
import com.fafa.util.Constants;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.Date;

public class LoginServlet extends HttpServlet {
    //    Servlet ：控制层 调用业务层代码
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("LoginServlet---start......");

        //        获取前端传来的账号密码
        String userCode = req.getParameter("userCode");
        String userPassword = req.getParameter("userPassword");

        //        和数据中的代码进行对比
        UserServiceImpl userService = new UserServiceImpl();
        User user = userService.login(userCode, userPassword);
        //      查有此人 可以登录
        if(user != null){
            //将用户信息 存在Session中
            req.getSession().setAttribute(Constants.USER_SESSION,user);
            //然后跳转
            resp.sendRedirect("jsp/frame.jsp");
        }else{//查无此人
            //转发回到登录页面 顺带提示 用户名或者密码错误
            req.setAttribute("error","用户名或者密码错误");
            req.getRequestDispatcher("login.jsp").forward(req,resp);
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```

#### 8.注册Servlet

```xml
<!--登录Servlet-->
<servlet>
    <servlet-name>login</servlet-name>
    <servlet-class>com.fafa.servlet.user.LoginServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>login</servlet-name>
    <url-pattern>/login.do</url-pattern>
</servlet-mapping>
```

### 3.登录功能优化

#### 1.注销功能

思路：移除session ，返回登录页

```java
//用户注销功能
public class LogoutServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        HttpSession session = req.getSession();
        //        移除 用户信息
        session.removeAttribute(Constants.USER_SESSION);

        User user = (User)session.getAttribute(Constants.USER_SESSION);
        //移除成功
        if (user == null){
            //           重定向 到 error.jsp 注意路径
            resp.sendRedirect(req.getContextPath()+"/jsp/error.jsp");
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```

####  2.注册xml 

```xml
<!--注销Servlet-->
<servlet>
    <servlet-name>logout</servlet-name>
    <servlet-class>com.fafa.servlet.user.LogoutServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>logout</servlet-name>
    <url-pattern>/user/logout</url-pattern>
</servlet-mapping>
```

### 4.登录拦截优化

 在filter包下编写一个过滤器，并注册 

```java
//拦截器（没有登录就无法进行访问 也就是非法访问）
public class SysFilter implements Filter {
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws IOException, ServletException {
        //        主要思路检测是Session里是否有当前用户者的信息
        HttpServletRequest request = (HttpServletRequest) req;
        HttpServletResponse response = (HttpServletResponse) resp;

        HttpSession session = request.getSession();
        User user = (User)session.getAttribute(Constants.USER_SESSION);
        //没有相关的信息
        if (user == null){
            response.sendRedirect(request.getContextPath()+"/login.jsp");
        }else{
            //放行
            chain.doFilter(req,resp);
        }
    }

    public void destroy() {

    }
}
```

注册

```xml
<!--拦截过滤器-->
<filter>
    <filter-name>SysFilter</filter-name>
    <filter-class>com.fafa.filter.SysFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>SysFilter</filter-name>
    <url-pattern>/jsp/*</url-pattern>
</filter-mapping>
```

### 5.密码修改

1. 写项目，建议从底层向上写  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200516180913135.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 
2. UserDao接口 

```java
//修改当前用户密码
public int updatePwd(Connection connection,int id,String password) throws SQLException;
```

​	3.UserDao接口实现类

```java
//  修改当前用户的密码
public int updatePwd(Connection connection, int id, String password) throws SQLException {
    //提升作用域
    PreparedStatement pstm = null;
    int execute = 0;
    if (connection != null){//保证安全 进行数据库连接验证
        String sql = "update smbms_user set userPassword = ? where id = ?";
        Object [] params = {password,id};//这里的两个对象分别对应上面的 两个 问号
        execute = BaseDao.execute(connection, pstm, sql, params);//执行sql语句
        //关闭资源
        BaseDao.closeResourse(null,pstm,null);
    }

    return execute;
}
```

​	4.UserService层

```java
//根据用户id修改密码
public boolean updatePwd(int id,String password) throws SQLException;
```

​	5.UserService接口实现类

```java
//  修改密码
public boolean updatePwd(int id, String password) {
    //        获取连接
    Connection connection = null;
    boolean flag = false;
    try {
        connection = BaseDao.getConnection();
        if (userDao.updatePwd(connection,id,password) > 0){//修改成功
            flag = true;
        }
    } catch (Exception e) {
        e.printStackTrace();
    } finally {
        //关闭资源
        BaseDao.closeResourse(connection,null,null);
    }
    return flag;
}

```

​	6.UserServlet

```java
//实现servlet复用
public class UserServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("已经入UserServlet");
        //从session里获得id
        HttpSession session = req.getSession();
        Object o = session.getAttribute(Constants.USER_SESSION);
        int id = 0;
        String password = req.getParameter("newpassword");
        boolean flag = false;
        //确保user存在  并且新密码不为空
        if (o != null && !StringUtils.isNullOrEmpty(password)){
            id = ((User)o).getId();
            UserServiceImpl userService = new UserServiceImpl();
            flag = userService.updatePwd(id, password);
            //修改密码成功
            if(flag){
                req.setAttribute("message","修改密码成功 请退出重新登陆");
                //移除session
                session.removeAttribute(Constants.USER_SESSION);
                //            resp.sendRedirect("login.jsp");

            }else{//修改密码失败
                req.setAttribute("message","修改密码失败");
            }
        }else{
            req.setAttribute("message","新密码有问题");
        }
        req.getRequestDispatcher("pwdmodify.jsp").forward(req,resp);

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```

​	7.注册Servlet

```xml
<!--修改密码Servlet-->
<servlet>
    <servlet-name>updatepwd</servlet-name>
    <servlet-class>com.fafa.servlet.user.UserServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>updatepwd</servlet-name>
    <url-pattern>/jsp/user.do</url-pattern>
</servlet-mapping>
```

### 6.优化密码修改使用Ajax

1.阿里巴巴的fastjson

```xml
<!-- https://mvnrepository.com/artifact/com.alibaba/fastjson -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.68</version>
</dependency>
```

2.后台代码修改

```java
package com.fafa.servlet.user;

import com.alibaba.fastjson.JSONArray;
import com.fafa.pojo.User;
import com.fafa.service.user.UserServiceImpl;
import com.fafa.util.Constants;
import com.mysql.jdbc.StringUtils;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.HashMap;
import java.util.Map;

//实现servlet复用
public class UserServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String method = req.getParameter("method");
        if(method.equals("savepwd") && method != null){
            this.updatePwd(req,resp);
        }else if(method.equals("pwdmodify") && method != null){
            this.pwdmodify(req,resp);
        }

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }

    //修改密码
    public void updatePwd(HttpServletRequest request, HttpServletResponse response){
        System.out.println("已经入UserServlet");
        //        从session里获得id
        HttpSession session = request.getSession();
        Object o = session.getAttribute(Constants.USER_SESSION);
        int id = 0;
        String password = request.getParameter("newpassword");
        boolean flag = false;
        //确保user存在  并且新密码不为空
        if (o != null && !StringUtils.isNullOrEmpty(password)){
            id = ((User)o).getId();
            UserServiceImpl userService = new UserServiceImpl();
            flag = userService.updatePwd(id, password);
            //修改密码成功
            if(flag){
                request.setAttribute("message","修改密码成功 请退出重新登陆");
                //移除session
                session.removeAttribute(Constants.USER_SESSION);
                //            resp.sendRedirect("login.jsp");

            }else{//修改密码失败
                request.setAttribute("message","修改密码失败");
            }
        }else{
            request.setAttribute("message","新密码有问题");
        }

        try {
            //            转发到修改密码的页面
            request.getRequestDispatcher("pwdmodify.jsp").forward(request,response);
        } catch (ServletException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    //通过ajax验证旧密码，到session拿即可
    public void pwdmodify(HttpServletRequest request, HttpServletResponse response){
        Object o = request.getSession().getAttribute(Constants.USER_SESSION);
        String oldpassword = request.getParameter("oldpassword");
        //万能的Map：结果集
        Map<String, String> resultMap = new HashMap<String, String>();

        if (null == o) {//session过期
            resultMap.put("result", "sessionerror");
        } else if (StringUtils.isNullOrEmpty(oldpassword)) {//旧密码输入为空
            resultMap.put("result", "error");
        } else {
            String sessionPwd = ((User) o).getUserPassword();
            if (oldpassword.equals(sessionPwd)) {
                resultMap.put("result", "true");
            } else {//旧密码输入不正确
                resultMap.put("result", "false");
            }
        }
        try {
            response.setContentType("application/json");
            PrintWriter outPrintWriter = null;
            outPrintWriter = response.getWriter();
            outPrintWriter.write(JSONArray.toJSONString(resultMap));//阿里巴巴的JSONArray工具类
            outPrintWriter.flush();//强制刷新
            outPrintWriter.close();//关闭流
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
}

```

 3.测试

### 7.用户管理实现

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200517210107269.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70) 

1. 导入分页的工具类-PageSupport
2. 用户列表页面导入-userlist.jsp

#### 1、获取用户数量

1. UserDao

```java
//查询用户总数
public int getUserCount(Connection connection,String userName,int userRole)throws SQLException;
```

​	2.UserDaoImpl

```java
//根据用户名或者角色查询用户总数（最难理解的sql语句）
public int getUserCount(Connection connection, String userName, int userRole) throws SQLException {
    PreparedStatement pstm = null;
    ResultSet rs = null;
    int count = 0;//总数

    if (connection != null){
        StringBuffer sql = new StringBuffer();//StringBuffer是可变字符串序列，而且效率高
        sql.append("select count(1) as count from smbms_user u,smbms_role r where u.userRole = r.id");
        ArrayList<Object> list = new ArrayList<Object>();//存放我们的参数

        if (!StringUtils.isNullOrEmpty(userName)){
            sql.append(" and u.userName like ?");//使用了模糊查询
            list.add("%"+userName+"%");//index:0
        }
        if(userRole > 0){
            sql.append(" and u.userRole = ?");
            list.add(userRole);//index:0
        }
        //把list转换为数组
        Object[] params = list.toArray();
        System.out.println("UserDaoImpl->getUserCount:"+sql.toString());
        rs = BaseDao.execute(connection,pstm,rs,sql.toString(),params);
        if(rs.next()){
            count = rs.getInt("count");//从结果集中获取最终的数量
        }
    }
    return count;
}
```

​	3.UserService

```java
//查询记录数
public int getUserCount(String userName,int userRole);
```

​	4.UserServiceImpl

```java
public int getUserCount(String userName, int userRole) {
    Connection connection = null;
    int count = 0;

    try {
        connection = BaseDao.getConnection();
        count = userDao.getUserCount(connection,userName,userRole);
    } catch (SQLException e) {
        e.printStackTrace();
    }finally {
        BaseDao.closeResourse(connection,null,null);
    }
    return count;
}public int getUserCount(String userName, int userRole) {
    Connection connection = null;
    int count = 0;

    try {
        connection = BaseDao.getConnection();
        count = userDao.getUserCount(connection,userName,userRole);
    } catch (SQLException e) {
        e.printStackTrace();
    }finally {
        BaseDao.closeResourse(connection,null,null);
    }
    return count;
}
```

#### 2、获取用户列表

1. UserDao

   ```java
   //根据条件查询用户列表
   public List<User> getUserList(Connection connection,String userName,int userRole,int currentPageNo,int pageSize)throws SQLException;
   ```

   

2. UserDaoImpl

   ```java
   //  根据条件查询用户列表
   public List<User> getUserList(Connection connection, String userName, int userRole, int currentPageNo, int pageSize) throws SQLException {
       PreparedStatement pstm = null;
       ResultSet rs = null;
       List<User> userList = new ArrayList<User>();//多态
   
       if (connection != null){
           //编写Sql语句
           StringBuffer sql = new StringBuffer();
           sql.append("select u.*,r.roleName as userRoleName from smbms_user u,smbms_role r where u.userRole = r.id");
           List<Object> list = new ArrayList<Object>();//这个是传递给sql语句的的 和上面那个有区别
           if(userName != null){
               sql.append(" and u.userName like ?");
               list.add("'%"+userName+"%'");
           }
           if (userRole > 0){
               sql.append(" and u.userRole = ?");
               list.add(userRole);
           }
           //在mysql数据库中，分页使用limit startIndex，pageSize;总数
           sql.append(" order by creationDate DESC limit ?,?");
           currentPageNo = (currentPageNo - 1) * pageSize;
           //开始的索引：（当前的页数 - 1） * 每页显示的行数
           list.add(currentPageNo);
           list.add(pageSize);
   
           Object[] params = list.toArray();
           System.out.println("sql--->"+sql.toString());
           rs = BaseDao.execute(connection,pstm,rs,sql.toString(),params);
           while(rs.next()){
               User _user = new User();
               _user.setId(rs.getInt("id"));
               _user.setUserCode(rs.getString("UserCode"));
               _user.setUserName(rs.getString("userName"));
               _user.setGender(rs.getInt("gender"));
               _user.setBirthday(rs.getDate("birthday"));
               _user.setPhone(rs.getString("phone"));
               _user.setUserRole(rs.getInt("userRole"));
               _user.setUserRoleName(rs.getString("userRoleName"));
               userList.add(_user);
           }
           //关闭资源
           BaseDao.closeResourse(null,pstm,rs);
       }else{
           System.out.println("数据库连接失败");
       }
       return userList;
   }
   ```

   

3. UserService

   ```java
   //根据条件查询用户列表
   public List<User> getUserList(String userName,int userRole,int currentPageNo,int pageSize );
   ```

   

4. UserServiceImpl

   ```java
   //根据条件查询用户列表
   public List<User> getUserList(String userName, int userRole, int currentPageNo, int pageSize) {
       List<User> list = null;
       Connection connection = null;
   
       try {
           connection = BaseDao.getConnection();
           list = userDao.getUserList(connection,userName,userRole,currentPageNo,pageSize);
       } catch (SQLException e) {
           e.printStackTrace();
       }finally {
           BaseDao.closeResourse(connection,null,null);
       }
   
       return list;
   }
   ```

#### 3、获取角色列表

1. RoleDao

   ```java
   /*
   获取角色列表
   * */
   List<Role> getRoleList(Connection connection)throws SQLException;
   ```

   

2. RoleDaoImpl

   ```java
   //获取角色列表
   public List<Role> getRoleList(Connection connection) throws SQLException {
       PreparedStatement pstm = null;
       ResultSet rs = null;
       List<Role> roleList = new ArrayList<Role>();
       if(connection != null){
           //编写Sql语句
           String sql = "select * from smbms_role";
           Object[] params = {};
           rs = BaseDao.execute(connection, pstm, rs, sql, params);
   
           while(rs.next()){
               Role _role = new Role();
               _role.setId(rs.getInt("id"));
               _role.setRoleCode(rs.getString("roleCode"));
               _role.setRoleName(rs.getString("roleName"));
               roleList.add(_role);
           }
           //关闭资源
           BaseDao.closeResourse(null,pstm,rs);
       }
       return roleList;
   }
   ```

   

3. RoleService

   ```java
   //获取角色列表
   public List<Role> getRoleList();
   ```

   

4. RoleServiceImpl

   ```java
   public class RoleServiceImpl implements RoleService {
       RoleDaoImpl roleDao;
       public RoleServiceImpl() {
           roleDao = new RoleDaoImpl();
       }
   
       //获取角色列表
       public List<Role> getRoleList(){
           Connection connection = null;
           List<Role> roleList = null;
           try {
               connection = BaseDao.getConnection();
               roleList = roleDao.getRoleList(connection);
           } catch (SQLException e) {
               e.printStackTrace();
           }finally {
               BaseDao.closeResourse(connection,null,null);
           }
   
           return roleList;
       }
   }
   
   ```


#### 4、用户显示的Servlet

1. 获取用户前端请求

2. 判断请求是否需要执行，看参数的值判断

3. 为了实现分页，需要计算出当前页面和总页数，页面大小。。

4. 用户列表展示

5. 返回前端

   ```java
   //用户信息查询 重点 难点
   public void query(HttpServletRequest req, HttpServletResponse resp) throws IOException {
       //        首先获取前端传来的参数
       String queryUserName = req.getParameter("queryname");
       String temp = req.getParameter("queryUserRole");
       String pageIndex = req.getParameter("pageIndex");
   
       int queryUserRole = 0;//第一次肯定是全部查询
       int pagesize = Constants.PAGESIZE;//页面大小
       int currentPageNo = 1;//第一次肯定是第一页
   
   
       //获取用户列表 和 角色列表
       UserService userService = new UserServiceImpl();
       List<User> userList = null;
       RoleService roleService = new RoleServiceImpl();
       List<Role> roleList = null;
   
       if(queryUserName == null){
           queryUserName = "";
       }
       if(temp != null && !temp.equals("")){
           queryUserRole = Integer.parseInt(temp);//给查询赋值0,1，2,3
       }
       if (pageIndex != null){
           try {
               currentPageNo = Integer.valueOf(pageIndex);
           } catch (NumberFormatException e) {
               resp.sendRedirect("error.jsp");
           }
       }
       //      获取用户总数
       int totalCount = userService.getUserCount(queryUserName, queryUserRole);
   
       PageSupport pages = new PageSupport();//主要是对数据进行一些安全限定
       pages.setCurrentPageNo(currentPageNo);//当前页
       pages.setPageSize(pagesize);          //页面大小
       pages.setTotalCount(totalCount);      //总页数
   
       int totalPageCount = pages.getTotalPageCount();
       //       上一页 下一页 限制
       if(currentPageNo < 1){//小于首页
           currentPageNo = 1;
       }else if(currentPageNo > totalPageCount){//大于尾页
           currentPageNo = totalPageCount;
       }
   
   
       //      获取角色列表
       roleList = roleService.getRoleList();
       req.setAttribute("roleList",roleList);
       //        根据条件查询用户列表
       userList = userService.getUserList(queryUserName, queryUserRole, currentPageNo, pagesize);
       //        给前端进行赋值
       req.setAttribute("userList",userList);
   
       req.setAttribute("totalCount",totalCount);
       req.setAttribute("currentPageNo",currentPageNo);
       req.setAttribute("totalPageCount",totalPageCount);
       try {
           req.getRequestDispatcher("userlist.jsp").forward(req,resp);
       } catch (ServletException e) {
           e.printStackTrace();
       }
   }
   ```

   

#### 5.添加用户

##### 5.1、查询用户是否存在

UserDao

```java
//查询用户是否存在
public User getLoginUser(Connection connection,String userCode);
```

UserDaoImpl

```java
//查询用户是否存在
public User getLoginUser(Connection connection, String userCode) {
    User user = null;
    PreparedStatement pstm = null;
    ResultSet rs = null;
    if (connection != null) {
        try {
            String sql = "select * from smbms_user where userCode = ?";
            System.out.println("查询用户是否存在sql--->" + sql);
            Object[] params = {userCode};
            rs = BaseDao.execute(connection, pstm, rs, sql, params);
            if (rs.next()) {
                user = new User();//这里一定要实例化
                user.setId(rs.getInt("id"));
                user.setUserCode(rs.getString("userCode"));
                user.setUserName(rs.getString("userName"));
                user.setGender(rs.getInt("gender"));
                user.setBirthday(rs.getDate("birthday"));
                user.setPhone(rs.getString("phone"));
                user.setUserRole(rs.getInt("userRole"));
                user.setUserRoleName(rs.getString("userRoleName"));
                user.setCreatedBy(rs.getInt("createdBy"));
                user.setCreationDate(rs.getTimestamp("creationDate"));
                user.setModifyBy(rs.getInt("modifyBy"));
                user.setModifyDate(rs.getTimestamp("modifyDate"));
                System.out.println("User != null");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            BaseDao.closeResourse(null,pstm,rs);
        }
    }
    return user;
}
```

UserService

```java
//根据userCode查询出User
public User selectUserCodeExist(String userCode);
```

UserServiceImpl

```java
//  根据userCode查询出User
    public User selectUserCodeExist(String userCode) {
    Connection connection;
    User user;
    connection = BaseDao.getConnection();
    user = userDao.getLoginUser(connection,userCode);
    BaseDao.closeResourse(connection,null,null);
    return user;
}
```

UserServlet

```java
//判断用户编码是否存在
private void userCodeExist(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    //判断用户账号是否可用
    String userCode = request.getParameter("userCode");
    //为了方便转换成json格式  使用了万能的Map集合
    HashMap<String, String> resultMap = new HashMap<String, String>();
    if (StringUtils.isNullOrEmpty(userCode)) {
        //userCode == null || userCode.equals("")
        resultMap.put("userCode", "exist");
    } else {
        UserService userService = new UserServiceImpl();
        User user = userService.selectUserCodeExist(userCode);
        if (null != user) {
            resultMap.put("userCode", "exist");
        } else {
            resultMap.put("userCode", "notexist");
        }
    }

    //把resultMap转为json字符串以json的形式输出
    //配置上下文的输出类型
    response.setContentType("application/json");
    //从response对象中获取往外输出的writer对象
    PrintWriter outPrintWriter = response.getWriter();
    //把resultMap转为json字符串 输出
    outPrintWriter.write(JSONArray.toJSONString(resultMap));
    outPrintWriter.flush();//刷新
    outPrintWriter.close();//关闭流
}
```

##### 5.2、添加用户信息

UserDao

```java
//添加用户信息
public int addUser(Connection connection,User user);
```

UserDaoImpl

```java
//  添加用户信息
public int addUser(Connection connection, User user) throws SQLException {
    PreparedStatement pstm = null;
    int result = 0;
    List<Object> list = new ArrayList<Object>();//存取需要用到的对象
    if (connection != null) {
        //编写sql语句
        StringBuffer sql = new StringBuffer();
        sql.append("insert into smbms_user(userCode,userName,userPassword,gender,birthday,phone,address,userRole,createdBy,creationDate) values(?,?,?,?,?,?,?,?,?,?)");
        System.out.println("sql--->" + sql.toString());
        list.add(user.getUserCode());
        list.add(user.getUserName());
        list.add(user.getUserPassword());
        list.add(user.getGender());
        list.add(user.getBirthday());
        list.add(user.getPhone());
        list.add(user.getAddress());
        list.add(user.getUserRole());
        list.add(user.getCreatedBy());
        list.add(user.getCreationDate());

        Object[] params = list.toArray();
        result = BaseDao.execute(connection, pstm, sql.toString(), params);
        BaseDao.closeResourse(null, pstm, null);
    }
    return result;
}
```

UserService

```java
//添加用户信息
public boolean useradd(User user);
```

UserServiceImpl

**<font color='red'>事务要放在业务层，还有Dao层的异常一般都要抛出</font>**

```java
//  添加用户信息
public boolean useradd(User user) {
    boolean flag = false;
    int result = 0;
    Connection connection = null;
    try {
        connection = BaseDao.getConnection();
        connection.setAutoCommit(false);//开启JDBC事务管理（设置事务手动提交）
        result = userDao.addUser(connection, user);
        connection.commit();//提交事务
        if (result > 0){
            flag = true;
            System.out.println("add success!");
        }else{
            System.out.println("add failed!");
        }
    } catch (SQLException e) {
        e.printStackTrace();
        try {
            System.out.println("rollback==================");
            connection.rollback();//事务回滚
        } catch (SQLException e1) {
            e1.printStackTrace();
        }
    }finally {
        //关闭资源
        BaseDao.closeResourse(connection,null,null);
    }

    return flag;
}
```

#### 6、移除用户信息（Ajax）

