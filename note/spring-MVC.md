### 1. 什么是SpringMVC

#### 1.1 概述

Spring MVC是Spring Framework的一部分，是基于Java实现MVC的轻量级Web框架。

#### 1.2 为什么要学习SpringMVC

1. 轻量级，简单易学
2. 高效 , 基于请求响应的MVC框架
3. 与Spring兼容性好，无缝结合
4. 约定优于配置
5. 功能强大：RESTful、数据验证、格式化、本地化、主题等
6. 简洁灵活

#### 1.3 SpringMVC执行原理

![图片](D:\Study\Note\640.png)

1. DispatcherServlet表示前置控制器，是整个SpringMVC的控制中心。用户发出请求，DispatcherServlet接收请求并拦截请求。

   我们假设请求的url为 : http://localhost:8080/SpringMVC/hello

   **如上url拆分成三部分：**

   http://localhost:8080服务器域名

   SpringMVC部署在服务器上的web站点

   hello表示控制器

   通过分析，如上url表示为：请求位于服务器localhost:8080上的SpringMVC站点的hello控制器。

2. HandlerMapping为处理器映射。DispatcherServlet调用HandlerMapping,HandlerMapping根据请求url查找Handler。

3. HandlerExecution表示具体的Handler,其主要作用是根据url查找控制器，如上url被查找控制器为：hello。

4. HandlerExecution将解析后的信息传递给DispatcherServlet,如解析控制器映射等。

5. HandlerAdapter表示处理器适配器，其按照特定的规则去执行Handler。

6. Handler让具体的Controller执行。

7. Controller将具体的执行信息返回给HandlerAdapter,如ModelAndView。

8. HandlerAdapter将视图逻辑名或模型传递给DispatcherServlet。

9. DispatcherServlet调用视图解析器(ViewResolver)来解析HandlerAdapter传递的逻辑视图名。

10. 视图解析器将解析的逻辑视图名传给DispatcherServlet。

11. DispatcherServlet根据视图解析器解析的视图结果，调用具体的视图。

12. 最终视图呈现给用户。



### 2. 如何创建一个SpringMVC项目（注解版）

1. 新建一个web项目
2. 导入相关jar包
3. 编写web.xml , 注册DispatcherServlet
4. 编写springmvc配置文件
5. 接下来就是去创建对应的控制类 , controller
6. 最后完善前端视图和controller之间的对应
7. 测试运行调试.

web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

</web-app>
```

springmvc-servlet.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/mvc
       https://www.springframework.org/schema/mvc/spring-mvc.xsd">
    <context:component-scan base-package="com.gk.controller"/>
    <mvc:default-servlet-handler/>
    <mvc:annotation-driven/>
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="internalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>

</beans>
```

HelloController.java

```java
package com.gk.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/hello")
public class HelloController  {

    @RequestMapping("/h1")
    public String hello(Model model){
        model.addAttribute("msg","Hello! SpringMVC Annotation!");
        return "hello";
    }
}

```

### 3. RestFul风格

#### 3.1 **概念**

Restful就是一个资源定位及资源操作的风格。不是标准也不是协议，只是一种风格。基于这个风格设计的软件可以更简洁，更有层次，更易于实现缓存等机制。

#### 3.2 **功能**

资源：互联网所有的事物都可以被抽象为资源

资源操作：使用POST、DELETE、PUT、GET，使用不同方法对资源进行操作。

分别对应 添加、 删除、修改、查询。

#### 3.3 使用

 @PathVariable 注解，让方法参数的值对应绑定到一个URI模板变量上

```java
package com.gk.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

@Controller
public class HelloController {
    @RequestMapping("/hello")
    public String hello(Model model){
        model.addAttribute("msg","Hello! SpringMVC");
        return "test";
    }
    @RequestMapping(path = "/add/{a}/{b}",method = RequestMethod.GET)
    public String test1(@PathVariable int  a , @PathVariable int b , Model model){
        int res = a + b;
        model.addAttribute("msg","结果为："+res);
        return "test";
    }
    //使用PostMapping注解可以直接将请求方式改为Post
    @PostMapping("/add/{a}/{b}")
    public String test2(@PathVariable int  a , @PathVariable int b , Model model){
        int res = a + b;
        model.addAttribute("msg","结果为："+res);
        return "test";
    }
}

```

### 4. 转发和重定向

在配置了视图解析器的情况下，直接在方法返回的字符串前加forward或者redirect就可以达到转发或者重定向功能

```java
    @RequestMapping("/redirect")
    public String test3(){
        return "redirect:index.jsp";
    }
```

### 5. 数据接收

1. **提交的域名称和处理方法的参数名不一致**

   提交数据 : http://localhost:8080/hello?username=kuangshen

   处理方法 :

   ```
   //@RequestParam("username") : username提交的域的名称 .
   @RequestMapping("/hello")
   public String hello(@RequestParam("username") String name){
      System.out.println(name);
      return "hello";
   }
   ```

2. **提交的是一个对象**

   要求提交的表单域和对象的属性名一致  , 参数使用对象即可

   1、实体类

   ```
   public class User {
      private int id;
      private String name;
      private int age;
      //构造
      //get/set
      //tostring()
   }
   ```

   2、提交数据 : http://localhost:8080/mvc04/user?name=kuangshen&id=1&age=15

   3、处理方法 :

   ```
   @RequestMapping("/user")
   public String user(User user){
      System.out.println(user);
      return "hello";
   }
   ```

   后台输出 : User { id=1, name='kuangshen', age=15 }

   ==说明：如果使用对象的话，前端传递的参数名和对象名必须一致，否则就是null。==

### 6. Jackson

#### 6.1 依赖

```xml
<dependency>
   <groupId>com.fasterxml.jackson.core</groupId>
   <artifactId>jackson-databind</artifactId>
   <version>2.9.8</version>
</dependency>
```

#### 6.2 Controller类

```java
package com.gk.controller;

import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.gk.pojo.User;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class HelloController {
    //produces字段作用为将返回值的编码改为UTF-8，这样避免乱码
    @RequestMapping(value = "/json1",produces = "application/json;charset=utf-8")
    @ResponseBody
    public String test1(Model model) throws JsonProcessingException {
        ObjectMapper objectMapper = new ObjectMapper();
        User user = new User(1,"宋思远","男");
        String string = objectMapper.writeValueAsString(user);
        return string;
    }
}
```

> 乱码统一解决方案
>
> ```xml
> <mvc:annotation-driven>
>    <mvc:message-converters register-defaults="true">
>        <bean class="org.springframework.http.converter.StringHttpMessageConverter">
>            <constructor-arg value="UTF-8"/>
>        </bean>
>        <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
>            <property name="objectMapper">
>                <bean class="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBean">
>                    <property name="failOnEmptyBeans" value="false"/>
>                </bean>
>            </property>
>        </bean>
>    </mvc:message-converters>
> </mvc:annotation-driven>
> ```
>
> 在类上直接使用 **@RestController** ，这样子，里面所有的方法都只会返回 json 字符串了，不用再每一个都添加@ResponseBody ！
>
> 修改后的Controller类:
>
> ```java
> package com.gk.controller;
> 
> import com.fasterxml.jackson.core.JsonProcessingException;
> import com.fasterxml.jackson.databind.ObjectMapper;
> import com.gk.pojo.User;
> import org.springframework.ui.Model;
> import org.springframework.web.bind.annotation.RequestMapping;
> import org.springframework.web.bind.annotation.RestController;
> 
> @RestController
> public class HelloController {
>     @RequestMapping("/json1")
>     public String test1(Model model) throws JsonProcessingException {
>         ObjectMapper objectMapper = new ObjectMapper();
>         User user = new User(1,"宋思远","男");
>         String string = objectMapper.writeValueAsString(user);
>         System.out.println(string);
>         return string;
>     }
> }
> ```

#### 6.3 将时间戳转换为json的方法抽象成一个工具类

JsonUtils.java

```java
package com.gk.utils;

import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;
import java.text.SimpleDateFormat;

public class JsonUtils {
    public static String getJson(Object object) {
        return getJson(object, "yyyy-MM-dd HH:mm:ss");
    }

    public static String getJson(Object object, String dateFormat) {
        ObjectMapper objectMapper = new ObjectMapper();
        //不使用时间差的方式
        objectMapper.configure(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS, false);
        //自定义日期格式对象
        SimpleDateFormat sdf = new SimpleDateFormat(dateFormat);
        //指定日期格式
        objectMapper.setDateFormat(sdf);
        try {
            return objectMapper.writeValueAsString(object);
        } catch (JsonProcessingException e) {
            e.printStackTrace();
        }
        return null;
    }
}
```

### 7. fastjson

#### 7.1 依赖

```xml
        <!-- https://mvnrepository.com/artifact/com.alibaba/fastjson -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>2.0.21</version>
        </dependency>
```

#### 7.2 使用

```java
package com.kuang.controller;

import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.JSONObject;
import com.kuang.pojo.User;

import java.util.ArrayList;
import java.util.List;

public class FastJsonDemo {
   public static void main(String[] args) {
       //创建一个对象
       User user1 = new User("秦疆1号", 3, "男");
       User user2 = new User("秦疆2号", 3, "男");
       User user3 = new User("秦疆3号", 3, "男");
       User user4 = new User("秦疆4号", 3, "男");
       List<User> list = new ArrayList<User>();
       list.add(user1);
       list.add(user2);
       list.add(user3);
       list.add(user4);

       System.out.println("*******Java对象 转 JSON字符串*******");
       String str1 = JSON.toJSONString(list);
       System.out.println("JSON.toJSONString(list)==>"+str1);
       String str2 = JSON.toJSONString(user1);
       System.out.println("JSON.toJSONString(user1)==>"+str2);

       System.out.println("\n****** JSON字符串 转 Java对象*******");
       User jp_user1=JSON.parseObject(str2,User.class);
       System.out.println("JSON.parseObject(str2,User.class)==>"+jp_user1);

       System.out.println("\n****** Java对象 转 JSON对象 ******");
       JSONObject jsonObject1 = (JSONObject) JSON.toJSON(user2);
       System.out.println("(JSONObject) JSON.toJSON(user2)==>"+jsonObject1.getString("name"));

       System.out.println("\n****** JSON对象 转 Java对象 ******");
       User to_java_user = JSON.toJavaObject(jsonObject1, User.class);
       System.out.println("JSON.toJavaObject(jsonObject1, User.class)==>"+to_java_user);
  }
}
```

### 8. SSM整合
