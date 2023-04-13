### 1. spring出现的目的？

解决企业级应用开发过于复杂繁琐

### 2. spring是什么？

spring是轻量级的拥有控制反转(Ioc)和面向切面编程(AOP)的容器

### 3. spring官方资料文档？

[Spring Framework Documentation](https://docs.spring.io/spring-framework/docs/5.3.24/reference/html/index.html)

### 4. 控制反转(IOC)

将对象的创建，组装交给Ioc容器进行，程序员不再关注对象的创建

#### 4.1 IOC创建对象方式

IOC默认使用空参构造来创建对象，如果有有参构造，需要在bean中使用constructor-arg进行构造，constructor-arg可以通过下标，类型，参数名称来进行赋值

1. 下标：

```xml
<bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg index="0" value="7500000"/>
    <constructor-arg index="1" value="42"/>
</bean>
```

2. 类型

```xml
<bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg type="int" value="7500000"/>
    <constructor-arg type="java.lang.String" value="42"/>
</bean>
```

3. 参数名称

```xml
<bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg name="years" value="7500000"/>
    <constructor-arg name="ultimateAnswer" value="42"/>
</bean>
```

### 5. spring配置

#### 5.1 别名 alias

#### 5.2 导入 import

### 6. 依赖注入

#### 6.1 构造器注入

```xml
<constructor-arg>
</constructor-arg>
```



#### 6.2 Set方式注入

pojo:

```java
package com.gk.pojo;

import java.util.*;

public class Student {
    private String name;
    private Address address;
    private String[] books;
    private Properties info;
    private Map<String,String> card;
    private List<String> hobbies;
    private Set<String> games;
    private String wife;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Address getAddress() {
        return address;
    }

    public void setAddress(Address address) {
        this.address = address;
    }

    public String[] getBooks() {
        return books;
    }

    public void setBooks(String[] books) {
        this.books = books;
    }

    public Properties getInfo() {
        return info;
    }

    public void setInfo(Properties info) {
        this.info = info;
    }

    public Map<String,String> getCard() {
        return card;
    }

    public void setCard(Map<String,String> card) {
        this.card = card;
    }

    public List<String> getHobbies() {
        return hobbies;
    }

    public void setHobbies(List<String> hobbies) {
        this.hobbies = hobbies;
    }

    public Set<String> getGames() {
        return games;
    }

    public void setGames(Set<String> games) {
        this.games = games;
    }

    public String getWife() {
        return wife;
    }

    public void setWife(String wife) {
        this.wife = wife;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", address=" + address +
                ", books=" + Arrays.toString(books) +
                ", info=" + info +
                ", card=" + card +
                ", hobbies=" + hobbies +
                ", games=" + games +
                ", wife='" + wife + '\'' +
                '}';
    }
}

```

xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="address" class="com.gk.pojo.Address">
        <property name="address" value="China">
        </property>
    </bean>
    <bean id="student" class="com.gk.pojo.Student">
        <property name="name" value="Bob">
        </property>
        <property name="books">
            <array>
                <value>红楼梦</value>
                <value>西游记</value>
                <value>水浒传</value>
                <value>三国演义</value>
            </array>
        </property>
        <property name="address" ref="address"></property>
        <property name="card">
            <map>
                <entry key="01" value="Bob"></entry>
            </map>
        </property>
        <property name="games">
            <set>
                <value>HALO</value>
            </set>
        </property>
        <property name="hobbies">
            <list>
                <value>唱</value>
                <value>跳</value>
                <value>Rap</value>
                <value>篮球</value>
            </list>
        </property>
        <property name="info">
            <props>
                <prop key="Bob">Bob@gmail.com</prop>
            </props>
        </property>
        <property name="wife">
            <null/>
        </property>
    </bean>

</beans>
```



#### 6.3 其他方式注入

6.3.1 p标签注入

```xml 
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="user" class="com.gk.pojo.User" p:name="Bob" p:age="18">
    </bean>
</beans>
```

注：p标签本质是set方法注入

6.3.2 c标签注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="user" class="com.gk.pojo.User" p:name="Bob" p:age="18"/>
    <bean id="user2" class="com.gk.pojo.User" c:name="john" c:age="25" />

</beans>
```

注：需要pojo类有有参构造才能使用c标签注入，c标签本质是构造器注入

#### 6.4 bean的作用域

![image-20221226111957714](D:\Study\Note\image-20221226111957714.png)

6.4.1 单例模式

6.4.2 原型模式

### 7. bean的自动装配

+ 自动装配是spring满足bean依赖的一种方式
+ spring会在上下文中自动寻找，并给bean自动装配属性 

在spring中有三种装配方式

1. 在xml中显式的装配
2. 在java中显式的装配
3. 隐式的自动装配bean【重要】

#### 7.1 XML显式装配

7.1.1 byName

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="cat" class="com.gk.Cat">
    </bean>
    <bean id="dog" class="com.gk.Dog">
    </bean>
    <bean id="person" class="com.gk.Person" autowire="byName">
        <property name="name" value="Jhon"></property>
    </bean>
</beans>
```

7.1.2 byType

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="cat" class="com.gk.Cat">
    </bean>
    <bean id="dog" class="com.gk.Dog">
    </bean>
    <bean id="person" class="com.gk.Person" autowire="byType">
        <property name="name" value="Jhon"></property>
    </bean>
</beans>
```

注：两者不同之处在于一个是通过，set后的名称来查找bean，一个是通过属性类型来查找bean，通过byType需要保证类型全局唯一



#### 7.2 使用注解装配

使用注解装配须知：

1. 要导入context约束

```xml
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

2. 注解的支持

<context:annotation-config/>

3. 在需要自动装配的bean或者set方法上添加@Autowired

```java
package com.gk;

import org.springframework.beans.factory.annotation.Autowired;

public class Person {
    private Cat cat;
    private Dog dog;
    private String name ;

    public Cat getCat() {
        return cat;
    }
    @Autowired
    public void setCat(Cat cat) {
        this.cat = cat;
    }

    public Dog getDog() {
        return dog;
    }
    @Autowired
    public void setDog(Dog dog) {
        this.dog = dog;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "Person{" +
                "cat=" + cat +
                ", dog=" + dog +
                ", name='" + name + '\'' +
                '}';
    }
}

```

4. 使用@Qualifier显式地指定bean进行装配

```java
    @Autowired
    @Qualifier("cat11")
    private Cat cat;
    @Autowired
    @Qualifier("dog22")
    private Dog dog;
    private String name ;
```

```xml
    <context:annotation-config/>
    <bean id="cat11" class="com.gk.Cat"/>
    <bean id="cat22" class="com.gk.Cat"/>
    <bean id="dog11" class="com.gk.Dog"/>
    <bean id="dog22" class="com.gk.Dog"/>
    <bean id="person" class="com.gk.Person" />
```

5. @Resource注解是java原生注解，通过ByName进行装配，也可以指定name

### 8 使用注解开发

需要导入aop包

#### 8.1 bean注册

对pojo类使用@Component注解实现由IOC容器进行管理bean

#### 8.2 对bean的属性进行设置

对属性值或者set方法使用@Value注解，完成对属性值的设置

```java
package com.gk.pojo;

import org.junit.validator.ValidateWith;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class User {

    @Value("Bob")
    private String name;

    @Value("25")
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}

```



#### 8.3 @Component衍生注解

对于web开发会将项目分为dao层，service层，controller层，每层有对应注解

> dao --> @Repository
>
> service --> @Service
>
> controller --> @Controller

四个注解的功能是等价的



#### 8.4 xml与注解的最佳实践

使用xml管理bean

使用注解完成bean的属性值设置

### 9 JavaConfig

可以完全不使用spring的xml文件配置

```java
package com.gk.config;

import com.gk.pojo.User;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class MyConfig {
    @Bean
    public User getUser(){
        return new User();
    }
}

```

### 10 代理模式

代理模式的好处：

1. 可以使真实角色的操作更加纯粹！不用去关心一些公共业务
2. 公共业务交给代理角色，实现了业务的分工
3. 公共业务发生扩展时方便集中管理

代理模式的缺点：

1. 一个真实角色就会产生一个代理角色，代码量会翻一倍

#### 10.1 静态代理





#### 10.2 动态代理

1. 动态代理和静态代理角色一样
2. 动态代理的代理类是动态生成的
3. 动态代理类分为两大类：基于接口的动态代理，基于类的动态代理
   + 基于接口-------JDK动态代理
   + 基于类----------cglib
   + java字节码-----javassist

需要了解两个类：Proxy，InvocationHandler

动态代理的本质，就是使用反射实现

```java
package com.gk.demo01;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

public class ProxyInvocationHandler implements InvocationHandler {

    //被代理的接口
    private Object target;

    public void setTarget(Object target) {
        this.target = target;
    }
    //生成得到代理类
    public Object getProxy(){
        return Proxy.newProxyInstance(this.getClass().getClassLoader(), target.getClass().getInterfaces(),this);
    }
    //处理代理实例并返回结果
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable{
        Object result = method.invoke(target, args);
        return result;
    }
}

```

### 11 AOP

#### 11.1 什么是AOP

AOP(Aspect Oriented Programming) 意为：面向切面编程，通过预编译方式和运行期间动态代理实现程序功能的统一维护的一种技术，AOP是OOP的一种延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可用性，同事提高了开发效率。

#### 11.2 AOP在Spring中的作用

==提供声明式事务：允许用户自定义切面==

- 切面(Aspect)：一个关注点的模块化，跨越多个类。事务管理是企业 Java 应用程序中横切关注点的一个很好的例子。在 Spring AOP 中，切面通过使用常规类（[基于模式的方法](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#aop-schema)）或使用 `@Aspect`注解（[@AspectJ 样式](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#aop-ataspectj)）进行注解的常规类来实现的。
- 连接点(Join point)：程序执行过程中的一个点，例如方法的执行或异常的处理。在 Spring AOP 中，一个连接点总是代表一个方法执行。
- 通知(Advice)：方面在特定连接点采取的行动。不同类型的通知包括“around”、“before”和“after”通知。（稍后讨论通知类型。）许多 AOP 框架，包括 Spring，将通知建模为拦截器并在连接点周围维护一个拦截器链。
- 切入点(Pointcut)：匹配连接点的谓词。通知与切入点表达式相关联，并在切入点匹配的任何连接点运行（例如，执行具有特定名称的方法）。切入点表达式匹配的连接点概念是 AOP 的核心，Spring 默认使用 AspectJ 切入点表达式语言。
- 简介(Introduction)：代表一个类型声明额外的方法或字段。Spring AOP 允许您向任何建议的对象引入新接口（和相应的实现）。例如，您可以使用引入使 bean 实现 `IsModified`接口，以简化缓存。（介绍在 AspectJ 社区中称为类型间声明。）
- 目标对象(Target object)：一个或多个方面建议的对象。也称为“建议对象”。由于 Spring AOP 是通过使用运行时代理实现的，因此该对象始终是代理对象。
- AOP 代理(AOP proxy)：由 AOP 框架创建的对象，用于实现切面契约（建议方法执行等）。在 Spring Framework 中，AOP 代理是 JDK 动态代理或 CGLIB 代理。
- 编织(Weaving)：将方面与其他应用程序类型或对象链接以创建建议对象。这可以在编译时（例如，使用 AspectJ 编译器）、加载时或运行时完成。Spring AOP 与其他纯 Java AOP 框架一样，在运行时执行织入。

![image-20221227154327015](D:\Study\Note\image-20221227154327015.png)

#### 11.3 在Spring中使用AOP

11.3.1 依赖包

```xml
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.6</version>
        </dependency>
```

11.3.2 使用

+ 使用spring提供的API接口

```xml
    <bean id="userService" class="com.gk.service.UserServiceImpl"/>
    <bean id="log" class="com.gk.log.Log"/>
    <bean id="logAfter" class="com.gk.log.AfterLog"/>
    <!--使用原生spring API接口配置aop-->
    <aop:config>
        <!--切入点：expression:表达式，execution(要执行的位置 * * * * *)-->
        <aop:pointcut id="pointcut" expression="execution(* com.gk.service.UserServiceImpl.*(..))"/>

        <!--执行环绕增强-->
        <aop:advisor advice-ref="log" pointcut-ref="pointcut"/>
        <aop:advisor advice-ref="logAfter" pointcut-ref="pointcut"/>

    </aop:config>
```

```java
package com.gk.log;

import org.springframework.aop.MethodBeforeAdvice;
import java.lang.reflect.Method;

public class Log implements MethodBeforeAdvice {
    //method:要执行的目标对象的方法
    //objects:参数
    //o:目标对象
    @Override
    public void before(Method method, Object[] objects, Object o) throws Throwable {
        System.out.println(o.getClass().getName()+"的"+method.getName()+"方法被执行了");
    }
}
```



+ 使用自定义类来实现AOP

```xml
    <bean id="diy" class="com.gk.diy.DiyPointcut"/>
    <aop:config>
        <aop:aspect ref="diy">
            <!--切入点-->
            <aop:pointcut id="point" expression="execution(* com.gk.service.UserServiceImpl.*(..))"/>

            <!--通知-->
            <aop:before method="before" pointcut-ref="point"/>
            <aop:after method="after" pointcut-ref="point"/>
        </aop:aspect>
    </aop:config>
```

```java
public class DiyPointcut {
    public void before(){
        System.out.println("============方法执行前============");
    }
    public void after(){
        System.out.println("============方法执行后============");
    }
}
```



+ 使用注解实现

```java
package com.gk.diy;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;

@Aspect
public class AnnotationPointCut {
    @Before("execution(* com.gk.service.UserServiceImpl.*(..))")
    public void before(){
        System.out.println("=========使用注解，方法执行前=========");
    }
    @After("execution(* com.gk.service.UserServiceImpl.*(..))")
    public void after(){
        System.out.println("=========使用注解，方法执行后=========");
    }
    @Around("execution(* com.gk.service.UserServiceImpl.*(..))")
    public void around(ProceedingJoinPoint pj) throws Throwable {
        System.out.println("=========使用注解，环绕前=========");
        Object proceed = pj.proceed();
        System.out.println("=========使用注解，环绕后=========");
    }
}

```

```xml
    <bean id="annotaoionPointCut" class="com.gk.diy.AnnotationPointCut"/>
    <aop:aspectj-autoproxy />
```

### 12 整合Mybatis

#### 12.1 步骤

+ 导入相关jar包

```xml
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.47</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.11</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>6.0.2</version>
        </dependency>
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.9.1</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>3.0.1</version>
        </dependency>
```

+ 编写配置文件
+ 测试

#### 12.2 回顾Mybatis

1. 编写实体类
2. 编写核心配置文件
3. 编写接口
4. 编写Mapper.xml
5. 测试

#### 12.3 Mybatis-Spring

1. 编写数据源配置
2. sqlSessionFactory
3. sqlSessionTemplate
4. 给Mapper接口写实现类
5. 将实现类注入到spring中
6. 测试

12.3.1 使用SqlSessionTemplate

```java
package com.gk.mapper;

import com.gk.pojo.User;
import org.mybatis.spring.SqlSessionTemplate;

import java.util.List;

public class UserMapperImpl implements UserMapper {
    
    private SqlSessionTemplate sqlSession;

    public void setSqlSession(SqlSessionTemplate sqlSession) {
        this.sqlSession = sqlSession;
    }

    @Override
    public List<User> selectUser() {
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        return mapper.selectUser();
    }
}
```

```xml
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <!--绑定Mybatis配置-->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
        <property name="mapperLocations" value="classpath:com/gk/mapper/*.xml"/>
    </bean>
    <!--SqlSessionTemplate,就是我们使用的sqlSession-->
    <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
        <!--只能使用构造器注入-->
        <constructor-arg index="0" ref="sqlSessionFactory"/>
    </bean>
```



需要new一个SqlSessionTemplate，并且在bean配置文件中使用构造器进行构造，将sqlSessionFactory注入到

sqlSessionTemplate中

12.3.2 使用SqlSessionDaoSupport

```java
package com.gk.mapper;

import com.gk.pojo.User;
import org.mybatis.spring.SqlSessionTemplate;
import org.mybatis.spring.support.SqlSessionDaoSupport;

import java.util.List;

public class UserMapperImpl2 extends SqlSessionDaoSupport implements UserMapper {
    @Override
    public List<User> selectUser() {
        return getSqlSession().getMapper(UserMapper.class).selectUser();
    }
}

```

```xml
    <bean id="userMapper2" class="com.gk.mapper.UserMapperImpl2">
        <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
    </bean>
```



只需要让mapper实现类继承SqlSessionDaoSupport类，之后直接使用getSqlSession()即可，这样写简单许多。

### 13 声明式事务

#### 1.回顾事务

+ 要么都成功，要么都失败
+ 事务在项目开发中十分重要，涉及到数据的一致性问题
+ 䧁数据的完整性和一致性

#### 2. 事务的ACID原则

+ 原子性
+ 一致性
+ 隔离性
+ 持久性

#### 3. spring中事务配置

```xml
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <constructor-arg ref="dataSource"/>
    </bean>
    <!--结合AOP进行事务的织入-->
    <!--配置事务通知-->
    <tx:advice id="txAdvice" transaction-manager="transactionManager">
        <tx:attributes>
<!--            给哪些方法配置事务-->
<!--            配置事务的传播特性：new propagation-->
            <tx:method name="add" propagation="REQUIRED"/>
            <tx:method name="delete"/>
            <tx:method name="update"/>
            <tx:method name="query"/>
            <tx:method name="*"/>
        </tx:attributes>
    </tx:advice>
    <aop:config>
        <aop:pointcut id="txPointCut" expression="execution( * com.gk.mapper.*.*(..))"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"/>
    </aop:config>
```

==此处事务使用aop进行配置织入==

#### 4. 事务传播属性

![image-20221228160610991](D:\Study\Note\image-20221228160610991.png)

