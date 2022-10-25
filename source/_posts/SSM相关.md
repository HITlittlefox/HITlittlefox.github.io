---
title: SSM相关
category: 我要就业
date: 2022-09-15 22:04:31
tags:
---
### Spring 基础
1. 什么是 Spring 框架?
    1. Spring 是一款开源的轻量级 Java 开发框架，旨在提高开发人员的开发效率以及系统的可维护性。
    2. 我们一般说 Spring 框架指的都是 Spring Framework，它是很多模块的集合，使用这些模块可以很方便地协助我们进行开发
        1. IoC
        2. AOP
        3. 快速访问数据库
        4. 集成第三方组件（电子邮件，任务，调度，缓存等等）
        5. 对单元测试支持比较好
        6. 支持 RESTful Java 应用程序的开发
    3. Spring 最核心的思想就是不重新造轮子，开箱即用，提高开发效率。
    4. 语言的流行通常需要一个杀手级的应用，Spring 就是 Java 生态的一个杀手级的应用框架。
    5. Spring 提供的核心功能主要是 IoC 和 AOP。
2. Spring,Spring MVC,Spring Boot 之间什么关系?
    1. Spring 包含了多个功能模块（上面刚刚提高过），
        1. 其中最重要的是 Spring-Core（主要提供 IoC 依赖注入功能的支持） 模块， 
        2. Spring 中的其他模块（比如 Spring MVC）的功能实现基本都需要依赖于该模块。
    2. Spring MVC 是 Spring 中的一个很重要的模块，
        1. 主要赋予 Spring 快速构建 MVC 架构的 Web 程序的能力。
        2. MVC 是模型(Model)、视图(View)、控制器(Controller)的简写，
        3. 其核心思想是**通过将业务逻辑、数据、显示分离**来组织代码。
    3. Spring 旨在简化 J2EE 企业应用程序开发。Spring Boot 旨在简化 Spring 开发（减少配置文件，开箱即用！）。
        1. 使用 Spring 开启某些 Spring 特性时，需要用 XML 或 Java 进行显式配置。
        2. Spring Boot 只是简化了配置，如果你需要构建 MVC 架构的 Web 程序，你还是需要使用 Spring MVC 作为 MVC 框架，只是说 Spring Boot 帮你简化了 Spring MVC 的很多配置，真正做到开箱即用！
3. Spring IoC
    1. 谈谈自己对于 Spring IoC 的了解
    2. IoC（Inverse of Control:控制反转） 是一种设计思想，而不是一个具体的技术实现。IoC 的思想就是将原本在程序中手动创建对象的控制权，交由 Spring 框架来管理。不过， IoC 并非 Spring 特有，在其他语言中也有应用。
    3. 为什么叫控制反转？
        1. 控制 ：指的是对象创建（实例化、管理）的权力
        2. 反转 ：控制权交给外部环境（Spring 框架、IoC 容器）
    4. 将对象之间的相互依赖关系交给 IoC 容器来管理，并由 IoC 容器完成对象的注入。简化应用开发。
    5. ![20220915233823](https://raw.githubusercontent.com/HITlittlefox/pictures/master/images/20220915233823.png)
    6. 在 Spring 中， IoC 容器是 Spring 用来实现 IoC 的载体
    7. IoC 容器实际上就是个 Map（key，value），Map 中存放的是各种对象。
    8. Spring 时代我们一般通过 XML 文件来配置 Bean，后来开发人员觉得 XML 文件来配置不太好，于是 SpringBoot 注解配置就慢慢开始流行起来。
4. 什么是 Spring Bean？
    1. Bean 代指的就是那些被 IoC 容器所管理的对象。
    2. 通过配置元数据来定义 Bean。
    3. 配置元数据可以是 XML 文件、注解或者 Java 配置类。
        ```xml
        <!-- Constructor-arg with 'value' attribute -->
        <bean id="..." class="...">
        <constructor-arg value="..."/>
        </bean>
        ```
    4. IoC 容器如何使用配置元数据来管理对象
        1. ![20220916001816](https://raw.githubusercontent.com/HITlittlefox/pictures/master/images/20220916001816.png)
5. 将一个类声明为 Bean 的注解有哪些?
    1. (不常用)@Component ：通用的注解，可标注任意类为 Spring 组件。如果一个 Bean 不知道属于哪个层，可以使用@Component 注解标注。
    2. @Repository : 对应持久层即 Dao 层，主要用于数据库相关操作。
    3. @Service : 对应服务层，主要涉及一些复杂的逻辑，需要用到 Dao 层。
    4. @Controller : 对应 Spring MVC 控制层，主要用户接受用户请求并调用 Service 层返回数据给前端页面。
    5. @Configuration : 指示一个类声明一个或多个@Bean方法，并且可以由Spring容器处理，以便在运行时为这些bean生成BeanDefinition和服务请求
6. @Component 和 @Bean 的区别是什么？
    1. 注解作用对象不同
        1. @Component 注解作用于类
        2. @Bean 注解作用于方法
    2. 自动装配与否
        1. @Component 通常是通过**类路径扫描**来自动侦测以及自动装配到 Spring 容器中（我们可以使用 @ComponentScan 注解定义要扫描的路径从中找出标识了需要装配的类自动装配到 Spring 的 bean 容器中）。
        2. @Bean 注解通常是我们在标有该注解的方法中定义产生这个 bean, @Bean 告诉了 Spring 这是某个类的实例，当我需要用它的时候还给我。
    3. 自定义性不同
        1. @Bean 注解比 @Component 注解的自定义性更强，而且很多地方我们只能通过 @Bean 注解来注册 bean。
        2. 比如当我们引用第三方库中的类需要装配到 Spring容器时，则只能通过 @Bean来实现。
7. @Bean注解使用示例：
    ```java
    @Configuration
    public class AppConfig {
        @Bean
        public TransferService transferService() {
            return new TransferServiceImpl();
        }
    }
    ```

    ```xml
    <beans>
        <bean id="transferService" class="com.acme.TransferServiceImpl"/>
    </beans>
    ```
8. 注入 Bean 的注解有哪些？
    1. Spring 内置的 @Autowired 
    2. JDK 内置的 @Resource 和 @Inject
    3. @Autowired 和@Resource使用的比较多一些
9. @Autowired 和 @Resource 的区别是什么？
    1. @Autowired 是 Spring 提供的注解，@Resource 是 JDK 提供的注解。
    2. Autowired 默认的注入方式为byType（根据类型进行匹配），@Resource默认注入方式为 byName（根据名称进行匹配）。
    3. 当一个接口存在多个实现类的情况下，@Autowired 和@Resource都需要通过名称才能正确匹配到对应的 Bean。
    4. Autowired 可以通过 @Qualifier 注解来显示指定名称，@Resource可以通过 name 属性来显示指定名称
10. Bean 的作用域有哪些?
    1.  singleton : IoC 容器中只有唯一的 bean 实例。Spring 中的 bean 默认都是单例的，是对单例设计模式的应用。
    2.  prototype : 每次获取都会创建一个新的 bean 实例。也就是说，连续 getBean() 两次，得到的是不同的 Bean 实例。
    3.  request （仅 Web 应用可用）: 每一次 HTTP 请求都会产生一个新的 bean（请求 bean），该 bean 仅在当前 HTTP request 内有效。
    4.  session （仅 Web 应用可用） : 每一次来自新 session 的 HTTP 请求都会产生一个新的 bean（会话 bean），该 bean 仅在当前 HTTP session 内有效。
    5.  application/global-session （仅 Web 应用可用）： 每个 Web 应用在启动时创建一个 Bean（应用 Bean），，该 bean 仅在当前应用启动时间内有效。
    6.  websocket （仅 Web 应用可用）：每一次 WebSocket 会话产生一个新的 bean。
11. 如何配置 bean 的作用域呢？
    ```xml
    <!-- xml 方式： -->
    <bean id="..." class="..." scope="singleton"></bean>
    ```
    ```java
    // 注解方式：
    @Bean
    @Scope(value = ConfigurableBeanFactory.SCOPE_PROTOTYPE)
    public Person personPrototype() {
        return new Person();
    }
    ```
12. 单例 Bean 的线程安全问题了解吗？
    1. 单例 Bean 存在线程问题，主要是因为当多个线程操作同一个对象的时候是存在资源竞争的。
    2. 常见的有两种解决办法：
        1. 在 Bean 中尽量避免定义可变的成员变量。
        2. 在类中定义一个 ThreadLocal 成员变量，将需要的可变成员变量保存在 ThreadLocal 中（推荐的一种方式）。
        3. 不过，大部分 Bean 实际都是无状态（没有实例变量）的（比如 Dao、Service），这种情况下， Bean 是线程安全的。
13. Bean 的生命周期了解么?
    1. ...

### Spring 与 设计模式
1. Spring 框架中用到了哪些设计模式？
    1. 工厂设计模式 : Spring 使用工厂模式通过 BeanFactory、ApplicationContext 创建 bean 对象。
    2. 代理设计模式 : Spring AOP 功能的实现。
    3. 单例设计模式 : Spring 中的 Bean 默认都是单例的。
    4. 模板方法模式 : Spring 中 jdbcTemplate、hibernateTemplate 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。
    5. 包装器设计模式 : 我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。
    6. 观察者模式: Spring 事件驱动模型就是观察者模式很经典的一个应用。
    7. 适配器模式 : Spring AOP 的增强或通知(Advice)使用到了适配器模式、spring MVC 中也是用到了适配器模式适配Controller。
2. 单例设计模式
    1. 在我们的系统中，有一些对象其实我们只需要一个，比如说：
        1. 一类对象只能有一个实例：线程池、缓存、对话框、注册表、日志对象、充当打印机、显卡等设备驱动程序的对象。
        2. 如果制造出多个实例就可能会导致一些问题产生
        3. 比如：程序的行为异常、资源使用过量、或者不一致性的结果。
    2. 使用单例模式的好处:
        1. 减少创建对象所花费的时间，减少系统开销；
        2. 减少系统内存的使用频率，这将减轻 GC 压力，缩短 GC 停顿时间。
        3. Spring 中 bean 的默认作用域就是 singleton(单例)的。
    3. Spring 中 bean 还有下面几种作用域：prototype、request、session、global-session
    4. Spring 实现单例的方式：
        1. xml : `<bean id="userService" class="top.snailclimb.UserService" scope="singleton"/>`
        2. 注解：`@Scope(value = "singleton")`
    5. Spring 通过 ConcurrentHashMap 实现单例注册表的特殊方式实现单例模式。Spring 实现单例的核心代码如下
```java
// 通过 ConcurrentHashMap（线程安全） 实现单例注册表
private final Map<String, Object> singletonObjects = new ConcurrentHashMap<String, Object>(64);

public Object getSingleton(String beanName, ObjectFactory<?> singletonFactory) {
        Assert.notNull(beanName, "'beanName' must not be null");
        synchronized (this.singletonObjects) {
            // 检查缓存中是否存在实例  
            Object singletonObject = this.singletonObjects.get(beanName);
            if (singletonObject == null) {
                //...省略了很多代码
                try {
                    singletonObject = singletonFactory.getObject();
                }
                //...省略了很多代码
                // 如果实例对象在不存在，我们注册到单例注册表中。
                addSingleton(beanName, singletonObject);
            }
            return (singletonObject != NULL_OBJECT ? singletonObject : null);
        }
        //将对象添加到单例注册表
        protected void addSingleton(String beanName, Object singletonObject) {
                synchronized (this.singletonObjects) {
                    this.singletonObjects.put(beanName, (singletonObject != null ? singletonObject : NULL_OBJECT));
                }
            }
}
```