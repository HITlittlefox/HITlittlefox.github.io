---
title: Spring-IoC
category: 大三下
date: 2022-06-28 19:37:56
tags:
---

## 学习顺序为:spring springmvc mybatis

1. Spring是一个轻量级容器框架
   1. 控制反转（IoC）
   2. 面向切面（AOP）

2. 理念：使现有的技术更加容易使用，大杂烩，整合了现有的技术框架

3. SSH=Struct2+Spring+Hibernate

4. SSM=SpringMVC+Spring+Mybatis

5. 官网：[Spring Framework](https://spring.io/projects/spring-framework#overview)

6. 中文文档：[Spring Framework 中文文档 - Spring Framework 5.1.3.RELEASE Reference | Docs4dev](https://www.docs4dev.com/docs/zh/spring-framework/5.1.3.RELEASE/reference/)

7. 官方文档在这个链接https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html

8. Github[spring-projects/spring-framework: Spring Framework (github.com)](https://github.com/spring-projects/spring-framework)

9. MAVEN[Maven Repository: spring (mvnrepository.com)](https://mvnrepository.com/tags/spring)

10. ```java
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.3.21</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.3.21</version>
    </dependency>
    
    ```

11. 优点：

    1. 开源、免费的框架；
    2. 轻量级、非入侵式的框架
    3. 控制反转IoC，面向切面编程AOP
    4. 支持事务的处理，对框架整合的支持

12. 总结一句话：Spring就是一个轻量级的控制反转IoC和面向切面编程AOP的框架

---

## Spring组成及拓展

1. 七大模块
2. 现代化的java开发（基于spring的开发）：构建一切--协调一切--连接一切
   1. Spring Boot
      1. 一个快速开发的脚手架
      2. 基于Springboot可以快速的开发单个微服务
      3. 约定大于配置
   2. Spring Cloud
      1. 基于spring boot实现的
3. Spingboot的前提使完全掌握Spring和SpringMVC
4. 弊端：配置地狱

---
##　IoC理论推导
1. UserDao接口

2. UserDaoImpl接口

3. UserService业务接口

4. UserServiceImpl接口

5. 之前的业务中，用户的需求可能会影响原来的代码，我们需要根据用户的需求去修改原代码

6. 如果程序代码量十分大，修改一次的成本代价十分昂贵。

7. ```java
   private UserDao userDao;
   
   // 使用set进行动态实现值的注入，实现了IoC控制反转！！！
   public void setUserDao(UserDao userDao) {
   this.userDao = userDao;
   }
   ```

8. 使用一个Set接口实现，已经发生了革命性的变化：

   1. 之前程序是主动创建对象，控制权在程序员手上！（用户每一个需求需要程序员去改代码）
   2. 使用了Set注入后，程序不再具有主动性，而是变成了被动的接收对象 
   3. 这种思想，从本质上解决了问题，不用再去管理对象的创建了。系统的耦合性大大降低，可以更加专注业务的实现。这是IoC的原型。

9. 控制反转IoC（Inversion of Control）是一种设计思想，DI（依赖注入）是实现IoC的一种方法。

10. IoC是一种通过**描述**（XML或注解）并通过**第三方**去生产或获取特定对象的方式。在Spring中实现控制反转的是IoC容器，其实现方法是依赖注入（Dependency Injection, DI）。

---

## Hello,Spring

1. Hello对象是Spring创建的；Hello对象的属性是Spring容器（也就是beans）设置的。
2. 控制：谁来控制对象的创建，传统应用程序的对象是由程序本身控制创建的，使用Spring后，对象是由Spring来创建的。
3. 反转：程序本身不创建对象，而变成被动的接收对象
4. 依赖：就是利用set方法来进行注入的
5. IoC是一种编程思想，由主动的编程变成被动的接收
6. 到了现在，彻底不用去程序中主动改动了。如果想要实现不同操作，只需要在xml配置文件中进行修改，所谓的IoC，一句话搞定：对象由Spring来创建、管理、装配！

---



## IoC创建对象的方式

1. 使用无参构造从创建构造
2. 假设使用有参构造创建对象
   1. 根据index参数下标设置
   2. 根据参数名字设置
   3. 根据参数类型设置
3. Spring容器在```ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");```就实例化了所有对象,随用随取.(在配置文件加载时,容器中管理的对象就都被创建了)

---

## Spring配置

1. 别名
2. Bean的配置
3. import:一般用于团队开发使用,可以将多个配置文件,导入合并为一个.
   1. 项目中多个人开发,分别负责不同的类开发,不同类注册在不同bean中,import可以合并.
   2. 使用总配置即可.

---

## 依赖注入

1. 构造器注入
2. Set方式注入(重点)
   1. 依赖注入:Set注入
      1. 依赖:bean对象的创建依赖于容器
      2. 注入:bean对象中的所有属性由容器来注入
   2. 环境搭建
      1. 复杂类型
      2. 真实测试对象
3. 拓展方式注入
   1. ```xmlns:p="http://www.springframework.org/schema/p"```p命名空间注入,可以直接注入属性的值:property
   2. ```xmlns:c="http://www.springframework.org/schema/c"```c命名空间
   3. 需要先导入约束,才能使用
4. bean的作用域
   1. Singleton单例(Spring默认模式)```scope="Singleton"```
   2. prototype原型,每次从容器中get,都会产生一个新对象
   3. request\session\appication,只在web开发中使用

---

## Bean的自动装配

1. 自动装配是Spring满足Bean依赖的一种方式

2. Spring会在上下文中自动寻找,并自动给bean装配属性

3. 有三种自动装配方式:

   1. XML显式配置
   2. java显式配置
   3. 隐式自动装配(重要)

4. 环境搭建

   1. byName:自动去容器上下文找和自己对象Set方法后面的值对应的bean id,并且全局唯一
   2. byType:自动去容器上下文找和自己对象属性类型相同的bean，需要全局唯一

5. 使用注解实现自动装配

   1. 导入约束

      ```
      <beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:context="http://www.springframework.org/schema/context"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
      http://www.springframework.org/schema/beans/spring-beans.xsd
      http://www.springframework.org/schema/context
      http://www.springframework.org/schema/context/spring-context.xsd">
      ```

      

   2. 配置注解的支持

      ```
      <context:annotation-config/>
      ```

   3. @Autowired

      1. 直接在属性上使用,也可以在set方式上使用
      2. 使用autowired不用编写set方法,前提是自动装配的属性在IoC容器中存在且符合bytype
      3. 如果环境复杂,不能一个autowired完成,可以用@Qualifier(value="xxx")辅助

   4. @Resource,或者@Resource(name="xxx")

   5. @Nullable 这个字段可以为null

   6. @Autowired和@Resource的区别

      1. 自动装配,都可以放在属性字段上

      2. @Autowired必须要求对象存在

      3. 执行顺序不同:

         1. @Autowired默认通过byType,多个同类型时,采用byName;
         2. @Resource默认通过byName,如果找不到就byType


---

## 使用注解开发

1. bean
2. 属性如何注入
3. 衍生的注解
   1. dao：@Repository
   2. service：@Service
   3. controller：@Controller
4. 自动装载配置
   1. @Autowired
   2. @Nullable
   3. @Resource
5. 作用域:@Scope("Singleton");@Scope("prototype")
6. 小结：
   1. xml更加万能，适用于任何场合，维护简单方便
   2. 注解：不是自己的类，使用不了，维护相对复杂
   3. 最佳实践：
      1. xml用来管理bean
      2. 注解用来完成属性的注入
      3. 使用过程中，只需要注意一个问题：必须让注解生效，就要开启注解支持

---

##　使用Java的方式配置Spring

1. 使用多个注解@Component、@Beans，完成xml的功能