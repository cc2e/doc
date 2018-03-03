### Spring 

Bean工厂，是spring框架最核心的接口，它提供了高级IoC的配置机制，

com.springframework.context.ApplicationContext建立在BeanFactory基础之上，提供了更多面向应用的功能，国际化支持，和框架事件系系

BeanFactory为 IoC容器，而称 ApplicationContext为应用上下文

几乎所有应用场合都可以直接使用ApplicationContext而非底层的BeanFactory



### 资源访问利器

- FileSystemResource 以文件系统绝对路径的方式进行访问

- ClassPathResouce 以类路径的方式进行访问

- ServletContextResource 以相对于web应用根目录的方式进行访问

  ​

  ```java
  Resource result1 = new ClassPathResource("conf/file.txt");
  WritableResource result2 = new PathResource("d:/www/master/conf/a.xml");

  OutputStream stream1 = result1.getOutputStream();
  stream1.write("这是要写入的资源".getBytes());
  stream1.close();

  InputStream ins1 = result1.getInputStream();
  InputStream ins2 = result2.getInputStream();

  ByteArrayOutputStream bodys = new ByteArrayOutputStream();
  int i ;
  while((i=ins1.read())!=-1){
    bodys.write(i);
  }
  System.out.println(bodys.toString());

  System.out.println("result1"+result1.getFilename());
  System.out.println("result2"+result2.getFilename());

  ```

  ​

- Servlet 用法 

  ```
  Resource resa = new ServletContextResource("application,"WEB-INF/classes/conf/file1.txt");
  ```

  ​

  ## # BeanFactory

- AutowireCapableBeanFactory

- SingletonBeanRegistry

- DefaultSingletonBeanRegistry

- AbstractBeanFactory


- ListableBeanFactory
- HierarchicalBeanFactory
- ConfigurableBeanFactory
- BeanDefinitionRegistry



```xml
<context-param>
	<param-name>contextConfigLocation</param-name>
	<param-value>/WEB-INF/smart-dao.xml, /WEB-INF/smart-service.xml</param-value>
</context-param>


<servlet>
	<servlet-name>log4jConfigServlet</servlet-name>
	<servlet-class>org.springframework.web.util.Log4jConfigServlet</servlet-class>
	<load-on-startup>1</load-on-startup>
</servlet>

<servlet>
	<servlet-name>springContextLoaderServlet</servlet-name>
	<servlet-class>org.springframework.web.context.ContextLoaderServlet</servlet-class>
	<load-on-startup>2</load-on-startup>
</servlet>

```





---



#### 属性注入 

```java
- Example1 普能属性注入

<bean id="car" class="com.smart.ditype.Car">
	<property name="maxSpeed" value="20000" />
    <property name="brand" value="法拉利zl" />
    <property name="price" value="2000000"/>
</bean>


- Example2  构造函数的属性注入

<bean id="car3" class="com.smart.ditype.Car">
	<constructor-arg index="0" type="java.lang.Spring" value="威驰FS" ／>
	<constructor-arg index="1" type="java.lang.Spring" value="日本丰田" ／>
	<constructor-arg index="2" type="int" value="600" ／>
</bean>


- Example 2  引用实例注入 引用 注入 car3
  
<bean id="company" class="com.smart.cons.Componey">
	<property name="cars" ref="car3"/>
	<property name="name" value="微幕视点"/>
</bean>
```



- 扫描注解定义的Bean

```xml
<?xml version="1.0" encoding="utf-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		xmlns:context="http://www.springframework.org/schema/context"
		xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.0.xsd http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context-4.0.xsd">
	
    <!--指定-->
    <context:component-scan base-package="com.smart.anno"/>
    
    <!-- 指定扫描包 -->
    <context:component-scan base-package="com.smart" resource-pattern="anno/*.class"/>
</beans>
```





注入时 使用过滤表达式

```xml
annotation    所有标注了xxxAnnotation类该类型彩用目标类是否标注了某个注解进行过滤
assignable    所有继承或扩展xxService的类，该类型彩用目标不类是否继承或扩展了某个特定类进行过滤
aspectj  继承或扩展它们的类
regex   正则表达式过滤类名
custom   采用 TypeFile代码方式实现过滤规则，该类必须实现


<context:component-scan base-package="com.smart">
     <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>                                       
</context:component-scan>
```





```java
@Service
public class LoginService{
    @Autowired(required=false)
    private LogDao logDao;
}


package com.smart.anno;
import org.springframework.beans.factory.anntation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Service;
@Service
public class LogonService{
    @Autowired
    private LogDao logDao;
    @Autowired
    @Qualifier("userDao")
    private UserDao userDao;
}

```





DB Bean

```XML
<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close" p:driverClassName="com.mysql.jdbc.Driver"
      p:url="jdbc:mysql://loclhost:3306/sampledb"
      p:userName="root"
      p:password="123456" />



file://  jdbc.properties
driverClassName="commysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/sampledb
userName=root
password=123456

<bean class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer"
      p:location="classpath:com/smart/placeholder/jdbc.properties"
      p:fileEncoding="utf-8"
      />

<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource"
      destroy-method="close"
      p:driverClassName="${driverClassName}"
      p:url="${url}"
      p:username="${userName}"
      p:password="${password}"
      />

```



Java类的配置中引用属性 

```java
file://  jdbc.properties
driverClassName="commysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/sampledb
userName=root
password=123456




package com.smart.placeholder;
import org.apache.commons.lang.builder.ToStringBuilder;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;
@Component
public class MyDataSource{
    @Value("${driverClassName}")
    private String driverClassName;
    @Value("${url}")
    private String url;
    @Value("${userName}")
    private String userName;
    @Value("${password}")
    private String password;
    
    public String toString(){
        return ToStringBuilder.reflectionToString(this);
    }
}
```

---

### DESC加密

```java

package com.smart.placeholder;

public class DESUtils{
    private static Key key;
    private static String KEY_STR = "myKey";
    static{
        try{
          KeyGeneration generator = KeyGenerator.getInstance("DES");
          generator.init(new SecureRandom(KEY_STR.getBytes()));
          key = generator.generateKey();
          generator = null;
        }catch(Exception e){
           throw new RuntimeException(e);
        }
    }
    public static String getEncryptString(String str){
        BASE64Encoder base64en = new BASE64Encoder();
        try{
            byte[] strBytes = str.getBytes("UTF8");
            Cipher cipher = Cipher.getInstance("DES");
            cipher.init(Cipher.ENCRYPT_MODE,key);
            byte[] encryptStrBytes = cipher.doFinal(strBytes);
            return base64en.encode(encryptStrBytes);
        }catch(Exception e){
            throw new RuntimeException(e);
        }
    }
    public static String getDecryptString(String str){
        BASE64Decoder base64De = new BASE64Decoder();
        try{
            byte[] strBytes = base64De.decodeBuffer(str);
            Cipher cipher = Cipher.getInstance("DES");
            cipher.init(Cipher.DECRYPT_MODE,key);
            byte[] decryptStrBytes = cipher.doFinal(strBytes);
            return new String(decryptStrBytes,"UTF8");
        }catch(Exception e){
            throw new RuntimeException(e);
        }
    }
}



```





### Spring 事件类

###### ApplicationEvent(Object source); 通过source指定事件源

- ApplicationContextEvent : 容器事件，它拥有4个子类，表示容器启动，刷新，停止，关闭的事件
- RequestHandleEvent：web应用相关的事件，只有在web.xml中定义了DispatcherServlet时，才会产生，分别代表Servlet及Portlet的事件请求













