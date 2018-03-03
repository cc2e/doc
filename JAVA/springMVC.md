# SpringMVC的优势

### 1清晰的角色划分

- 前端控制器 DispatcherServlet
- 请求到处理器映射HandlerMapping
- 处理器适配器HandlerAdapter
- 视图解析器 viewResolver
- 处理器或页面控制器（Controller)
- 验证器 （Validator)
- 命令对象（Command)
- 表单对象 Form Object

### 2 扩展灵活

>  由于命令对象就是一个POJO,无需继承特定的API，可以命名用命令对象直接作为业务对象
>
> 方便和其它框架集成
>
> 可适配，通过HandlerAdapter，可以支持任意的类作为处理器
>
> 可定制性，HandlerMapping ,ViewResolver



强大的数据验证，格式化，绑定机制

利用Spring提供的Mock对象能够非常简单的进行Web层单元测试

本地化，主题的解析的支持，国际化和主题切换

强大的Jsp标签库，使JSP编写更容易





---





#### Model模型

> 因此包含数据和行为，可以认为是领域模型或JavaBean组件，包含数据和行为（改变状态，业务逻辑）
>
> 1.保存数据，2.修改数据，3.查询数据



#### View视图

> 负王赠进行模型的展示，一般就是我们见到的用户界面，客户想看到的东西
>
> ：展示数据模型，提交供交互



####  Controller控制器

> 接收用户请求，委托给模型进行处理（状态改变），处理完毕后把返回的模型数据返回给视图
>
> ：接受用户请求，委托为模型进行处理，选择数视图



### 关键词

- CGI：公共网关接口，一种Web服务端使用的脚本技术，重量级
- Servlet：一种JavaEE web组件技术，是一种在服务端执行的web组件，用于接收web用户请求并处理，最后动态产生响就，每次请求只产生一个线程，轻量级，



# Example

```
public class LoginServlet extends HttpServlet{
    
}
```





## 模型代码

```java
public class UserBean implements java.io.Serializable{
    private String username;
    private String password;
    public String getUsername(){
        return username;
    }
    public void setUsername(String username){
        this.username=username;
    }
    public String getPassword(){
        return password;
    }
    public void setPassword(String password){
        this.password=password;
    }
    public boolean login(){
        if("zhang".equals(this.username)&&"123".equals(this.password)){
            return true;
        }
        return false;
    }
}
```



## 视图

```jsp
<%@page import="cn.javass.chapter1.javabean.UserBean" %>
<%@page language="java" contentType="text/html;charset=utf-8" pageEncoding="utf-8"%>
<!doctype html>
<html>
   <head>
       <meta http-equiv="Content-Type" content="text/html;charset=utf-8" >
       <title>登录</title>
    </head>
    <body>
       <form action="${pageContext.request.contextPath}/modelLogin" method="post">
           <input type="hidden" name="submitFlage" value="login"/>
           <p>
               username:<input type="text" name="username" value="${user.username}"/>
           </p>
           <p>
               password:<input type="text" name="password" />
           </p>
           <input type="submit" value="login"/>
        </form>
    </body>
</html>

```





## Controller

```java
public class ModelServlet extends HttpServlet{
    @Override
    protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException{
        doPost(req,res); 
    }
    @Override
    protected void doPost(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException{
        String submitFlag = req.getParameter("submitFlag");
        if("toLogin".equals(submitFlag)){
			toLogin(req,res);
            return;
        }else if("login".equals(submitFlag)){
            login(req,res);
            return;
        }
        toLogin(req,res);
    }
    
    private void toLogin(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException{
        req.getRequestDispatcher("mvc/login.jsp").forward(req,res);
    }
    private void login(HttpServletRequest req,HttpServletResponse res)throws IOException,ServletException{
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        UserBean user= new UserBean();
        user.setUsername(username);
        user.setPassword(password);
        if(user.login()){
            res.sendRedirect(req.getContextPath()+"mvc/success.jsp");
        }else{
            req.setAttribute("user",user);
            toLogin(req,res);
            return;
        }
    }
}
```



Front Controller

> 前端控制器，负责为表现层提供统一访问点， 根据参数进行控制

Application Controller

> 应用控制器，用来选择具体视图技术，和具体的功能处理，一种策略设计模式的应用

Page Controller

> 页面控制器／动作／处得器：功能处理代码，收集参数，封装参数，发到至模型，转调业务对象处理模型

Context

> 上下文，我还记得Model中为视图准备要展示的模型数据，我们直接放在request中，有了上下文之后，我们可以将相关数据放置在上下文，从而与协议无关的访问／设置模型数据



---

```
<servlet>
	<servlet-name>chapter</servlet-name>
	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
	<load-on-startup>1</load-on-startup>
</servlet>
<servlet-mappping>
	<servlet-name>chapter</servlet-name>
	<url-pattern>/<url-pattern>
</servlet-mapping>


<bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
<bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>
```





```
public class LiteralExprSample{
    public static void main(String[] args){
        ExpressionParser parser = new SpelExpressionParser();
    }
}
```



---

parent 		父类工程

commons     工具类

entity     实体类

dao	    数据库访问层

service   服务层

web  	web层

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc" xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
	http://www.springframework.org/schema/beans/spring-beans.xsd
	http://www.springframework.org/schema/context
	http://www.springframework.org/schema/context/spring-context-4.3.xsd
	http://www.springframework.org/schema/mvc
	http://www.springframework.org/schema/mvc/spring-mvc-4.3.xsd http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">

    <context:component-scan base-package="com.biyao.cms.web" use-default-filters="false"><!-- base-package 如果多个，用“,”分隔 -->
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>

    <context:annotation-config/>
    <context:property-placeholder location="classpath:prop/env.properties"/>

    <mvc:annotation-driven/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <mvc:exclude-mapping path="/index.html"/>
            <mvc:exclude-mapping path="/view/**"/>
            <mvc:exclude-mapping path="/js/**"/>
            <mvc:exclude-mapping path="/css/**"/>
            <mvc:exclude-mapping path="/font/**"/>
            <mvc:exclude-mapping path="/images/**"/>
            <mvc:exclude-mapping path="/login"/>
            <mvc:exclude-mapping path="/logout"/>
            <mvc:exclude-mapping path="/auth"/>
            <bean class="com.biyao.cms.web.common.security.AuthInterceptor"/>
        </mvc:interceptor>
        <mvc:interceptor>
            <mvc:mapping path="/push/auditPassPush"/>
            <mvc:mapping path="/push/auditNotPassPush"/>
            <bean class="com.biyao.cms.web.common.security.PushAuthorizeInterceptor"/>
        </mvc:interceptor>
    </mvc:interceptors>

    <mvc:default-servlet-handler/>

    <bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/" />
        <property name="suffix" value=".jsp" />
        <property name="viewClass" value="org.springframework.web.servlet.view.JstlView" />
    </bean>

    <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <property name="maxInMemorySize" value="10240" /> <!-- 最大内存大小 (10240) -->
        <property name="maxUploadSize" value="-1" /> <!-- 最大文件大小，-1为无限止(-1) -->
    </bean>

</beans>

```



### spring mvc annonition

```
multipartResolver  //文件上传解析器

localeResolver   //本地化解析器

themeResolver   //主题解析器，类型为 LocaleResolver的Bean作为该类型的组件

detectAllHandlerMapping  //处理器 映射器-根据类型匹配机制查找上下文及父spring容器中所有类型为handlerMapping的Bean

detectAllHandlerAdapters //处理器-适配器


detectAllHandlerExceptionResolvers   处理器异常解析器


org.springframework.web.servlet.view.InternalResourceViewResolver 视图解析器



```

