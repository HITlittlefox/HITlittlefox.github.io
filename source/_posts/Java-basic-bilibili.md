---
title: Java-basic-bilibili   
date: 2021-08-05 00:00:00  
tags:  
category: Java
---

### 学习地点：Bilibili 狂神说Java零基础学Java

### 知识总览（学弟口述）

变量声明、数组、字符串、流程控制语句、类与对象、继承、封装、多态、接口、常用api、异常处理、**”多线程”、输入输出IO流、泛型与容器、内部类与匿名内部类λ表达式、注解与反射、可视化编程GUI、JDBC**。

--------------------------------

#### 基本知识：

    三个版本
    JavaSe：标准版（桌面程序、控制台开发）
    JavaME：嵌入式开发（手机、小家电）
    JavaEE：企业级开发（web端，服务器开发）

#### JDK、JRE、JVM

    JDK：开发工具包
    JRE：编译器
    JVM：虚拟机

#### 基础：

注释、关键字、强数据类型、弱数据类型、类型转换、变量、常量、作用域、运算符、package机制、JavaDoc文档

#### 流程控制

Scanner、顺序结构、if选择结构、Switch选择结构、While循环、DoWhile循环、For循环、break、continue、goto、

#### 方法

定义、调用、重载、命令行传参、可变参数、递归

#### 数组

声明、创建、下标越界、二维数组、冒泡排序

--------------------------------

#### 直接冲到面向对象

01. 什么是面向对象
    01. 面向对象编程(Object-Oriented Programming,OOP)
    02. 本质：以类的方式组织代码，以对象的组织封装数据
    03. 从认识论角度考虑是先有对象后有类。对象是具体的事物；类是对对象的抽象。
    04. 从代码运行角度考虑是先有类后有对象。****类是对象的模板。

02. 方法的定义
    01. 修饰符
    02. 返回类型 （break：跳出switch）和（return：结束方法，返回值）的区别
    03. 方法名：规范：驼峰
    04. 参数列表(参数类型，参数名)，可变参数
    05. 异常抛出

03. 方法的调用
    01. 静态方法
    02. 非静态方法 若想调用非静态方法，需要先实例化。
    03. 形参和实参
    04. 值传递和引用传递
    05. this关键字

04. 类与对象的创建

05. 构造器详解
    01. 构造器  
       和类名相同  
       没有返回值

    02. 作用:  
       new本质在调用构造方法  
       初始化对象的值

    03. 注意点:  
       定义有参构造之后， 如果想使用无参构造，显示的定义一个无参的构造  
       构造器快捷键：ALt +Insert

06. 创建对象内存分析

07. 简单小结类与对象

08. 封装详解
    01. 高内聚，低耦合
    02. 通常应禁止直接访问一个对象中数据的实际表示，而应通过操作接口来访问，这称为信息隐藏。
    03. 属性私有，get/set
09. 什么是继承
    01. 继承的本质是对某一批类的抽象。
    02. extends的意思是“扩展”。子类是父类的扩展。
    03. JAVA中类只有单继承，没有多继承!
    04. 继承是类和类之间的一种关系。除此之外,类和类之间的关系还有依赖、组合、聚合等。
    05. 继承关系的俩个类，一个为子类(派生类),一个为父类(基类)。子类继承父类,使用关键字extends来表示。子类和父类之间,从意义上讲应该具有”is a”的关系.
    06. object类
    07. super
    08. 方法重写

10. Super详解
    01. Super:  
       super调用父类的构造方法，必须在构造方法的第一个  
       super必须只能出现在子类的方法或者构造方法  
       super和 this不能同时调用构造方法!

    02. this:  
       代表的对象不同:  
       this:本身调用者这个对象  
       super:代表父类对象的应用前提  
       this:没有继承也可以使用  
       super:只能在继承条件下才可以使用构造方法  
       this():本类的构造  
       super():父类的构造!

11. 方法重写
    01. 因为静态方法是类的方法，而非静态是对象的方法
    02. 有static时，b调用了B类的方法，因为b是用b类定义的
    03. 重写:需要有继承关系，子类重写父类的方法!  
       方法名必须相同  
       参数列表列表必须相同

    04. 修饰符:范围可以扩大但不能缩小:public>Protected>Default>private
    05. 抛出的异常:范围，可以被缩小，但不能扩大; classNotFoundException –> Exception(大)重写，子类的方法和父类必要一致;方法体不同!
    06. 为什么需要重写:父类的功能，子类不一定需要，或者不一定满足!Alt +Insert ; 选择override;
12. 什么是多态
    01. 同一方法可以根据发送对象的不同而采用多种不同的行为方式。
    02. 一个对象的实际类型是确定的，但可以指向对象的引用的类型有很多(父类，有关系的类)
    03. 多态存在的条件  
       有继承关系  
       子类重写父类方法  
       父类引用指向子类对象  
       注意: 多态是方法的多态，属性没有多态性。  
       instanceof:(类型转换)引用类型

    04. 一个对象的实际类型是确定的
        

```
            new Student();
            new Person();
        ```

    05. 可以指向的引用类型就不确定了:父类的引用可以指向子类
    06. Student能调用的方法都是自己的或者继承父类的!
        

```
            student s1 = new Student();
        ```

    07. Person父类型，可以指向子类，但是不能调用子类独有的方法
        

```
            Person s2 = new Student();
            object s3 = new Student();
        ```

    08. 对象能执行哪些方法，主要看对象左边的类型，和右边关系不大!

    09. 子类重写了父类的方法，执行子类的方法
        

```
            ( (student) s2).eat();
         ```

13. instanceof和类型转换
    01. 父类引用指向子类的对象
    02. 把子类转换为父类，向上转型;
    03. 把父类转换为子类，向下转型;强制转换
    04. 方便方法的调用，减少重复的代码!简洁
14. static关键字详解
    01. 顺序：静态代码块>匿名代码块>构造方法
    02. 静态代码块：只执行一次
    03. 匿名代码块：赋初始值
    04. 静态导入包import
15. 抽象类
    01. Java的类是单继承，接口可以多继承
    02. 抽象类可以没有抽象方法，有抽象的必须是抽象类
16. 接口的定义与实现 3.
    01. 普通类:只有具体实现
    02. 抽象类:具体实现和规范(抽象方法)都有!
    03. 接口:只有规范!自己无法写方法~
    04. 接口就是规范，定义的是一组规则。
    05. OO的精髓，是对对象的抽象，最能体现这一点的就是接口。为什么我们讨论设计模式都只针对具备了抽象能力的语言(比如c++、java、c#等)，就是因为设计模式所研究的，实际上就是如何合理的去抽象。
    06. 声明类的关键字是class,声明接口的关键字是interface
    07. interface定义的关键字，接口都需要有实现类
    08. 接口中的所有定义的方法其实都是抽象的public abstract
    09. implements可以实现多个接口
    10. 必须要重写接口中的方法~

17. N种内部类
    01. static代码块第一加载 然后是匿名代码块 然后才是构造方法

18. 异常
    01. 处理运行时异常时，采用逻辑去合理规避同时辅助try-catch处理
    02. 在多重catch块后面，可以加一个catch (Exception）来处理可能会被遗漏的异常
    03. 对于不确定的代码，也可以加上 try-catch，处理潜在的异常
    04. 尽量去处理异常，切忌只是简单地调用printStackTrace()去打印输出
    05. 具体如何处理异常，要根据不同的业务需求和异常类型去决定
    06. 尽量添加finally语句块去释放占用的资源
