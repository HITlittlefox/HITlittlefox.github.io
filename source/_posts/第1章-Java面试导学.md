---
title: 第1章 Java面试导学
category: 我要就业
date: 2022-08-20 23:54:24
tags:
---
<!-- ![20220820235433](https://raw.githubusercontent.com/HITlittlefox/pictures/master/images/20220820235433.png)
![20220820235631](https://raw.githubusercontent.com/HITlittlefox/pictures/master/images/20220820235631.png) -->
#### 基础概念与常识
1. Java 语言有哪些特点?
    1. 简单易学；
    2. 面向对象（封装，继承，多态）；
    3. 平台无关性（ Java 虚拟机实现平台无关性）；
    4. 支持多线程
        1. C++ 语言没有内置的多线程机制，因此必须调用操作系统的多线程功能来进行多线程程序设计.(C++11 开始（2011 年的时候）,C++就引入了多线程库)
        2. Java 语言却提供了多线程支持；
    5. 可靠性；
    6. 安全性；
    7. 支持网络编程并且很方便（ Java 语言诞生本身就是为简化网络编程设计的，因此 Java 语言不仅支持网络编程而且很方便）；
    8. 编译与解释并存；
2. JVM vs JDK vs JRE
    1. Java 虚拟机（JVM）是运行 Java 字节码的虚拟机。JVM 有针对不同系统的特定实现（Windows，Linux，macOS），目的是使用相同的字节码，它们都会给出相同的结果
    2. 字节码和不同系统的 JVM 实现是 Java 语言“一次编译，随处可以运行”的关键所在
3. 什么是字节码?采用字节码的好处是什么?
    1. JVM 可以理解的代码就叫做字节码，只面向虚拟机
    2. 高效（解释型语言缺点）、可移植（解释型语言优点）
    3. Java 程序无须重新编译便可在多种不同操作系统的计算机上运行
4. 为什么说 Java 语言“编译与解释并存”？
    1. 因为 Java 语言既具有编译型语言的特征，也具有解释型语言的特征。
    2. 因为 Java 程序要经过**先编译，后解释**两个步骤，
        1. 由 Java 编写的程序需要先经过编译步骤，生成字节码（.class 文件），
        2. 这种字节码必须由 Java 解释器来解释执行
5. Java 和 C++ 的区别?
    1. Java 和 C++ 都是面向对象的语言，都支持封装、继承和多态
    2. Java 不提供指针来直接访问内存，程序内存更加安全
    3. Java 的类是单继承的，C++ 支持多重继承；虽然 Java 的类不可以多继承，但是接口可以多继承。
    4. Java 有自动内存管理垃圾回收机制(GC)，不需要程序员手动释放无用内存。
    5. C ++同时支持方法重载和操作符重载，但是 Java 只支持方法重载（操作符重载增加了复杂性，这与 Java 最初的设计思想不符）
#### 基本语法
1. 注释有哪几种形式？
    1. Java 中的注释有三种：
    2. 单行注释 ：通常用于解释方法内某单行代码的作用。
    3. 多行注释 ：通常用于解释一段代码的作用。
    4. 文档注释 ：通常用于生成 Java 开发文档。
2. 标识符和关键字的区别是什么？
    1. 标识符就是一个名字
    2. 关键字是被赋予特殊含义的标识符
3. Java 语言关键字有哪些？
    1. 访问控制 private protected public default   
    2. 类，方法和变量修饰符 
        1. abstract class extends final implements interface native
        2. new static strictfp synchronized transient volatile enum default
    3. 程序控制
        1. break continue return do while if else
        2. for instanceof switch case default assert 
        3. default
    4. 错误处理 try catch throw throws finally  
    5. 包相关 import package     
    6. 基本类型 boolean byte char double float int long short      
    7. 变量引用 super this void    
    8. 保留字 goto const  
    9. default 这个关键字很特殊，既属于程序控制，也属于类，方法和变量修饰符，还属于访问控制
4. 自增自减运算符
    1. ++
    2. --
5. continue、break 和 return 的区别是什么？
    1. continue ：指跳出当前的这一次循环，继续下一次循环。
    2. break ：指跳出整个循环体，继续执行循环下面的语句。
    3. return 用于跳出所在方法，结束该方法的运行。return 一般有两种用法：
        1. return; ：直接使用 return 结束方法执行，用于没有返回值函数的方法
        2. return value; ：return 一个特定值，用于有返回值函数的方法