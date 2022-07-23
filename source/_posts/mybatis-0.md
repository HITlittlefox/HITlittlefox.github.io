---
title: mybatis
category: 大三下
date: 2022-07-23 11:03:24
tags:
---
### 1 Mybatis

最好的学习方式：看官方文档。

### 1.2 简介

1. 什么是 Mybatis
    1. MyBatis 是一款优秀的**持久层框架**
    2. 它支持自定义 SQL、存储过程以及高级映射。
    3. MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。
    4. MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。
    5. [MyBatis](https://baike.baidu.com/item/MyBatis) 本是 apache 的一个 开源项目 iBatis, 2010 年这个项目由 apache software foundation 迁移到了 [google code](https://baike.baidu.com/item/google code/2346604)，并且改名为 MyBatis 。

### 1.3 如何获得 Mybatis？
1. Maven  
    ```java
    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.2</version>
    </dependency>
    ```
2. Github [GitHub - mybatis/mybatis-3: MyBatis SQL mapper framework for Java](https://github.com/mybatis/mybatis-3)
3. 中文文档 [mybatis – MyBatis 3 | 简介](https://mybatis.org/mybatis-3/zh/index.html)


### 1.4 持久化层
数据持久化  
持久化就是将程序的数据在持久化状态和顺时状态转化的过程  
内存：断电即失  
数据库（Jdbc），io 文件持久化  
生活：冷藏，罐头  
为什么需要持久化？  
有一些对象不能让它丢失  
内存太贵  

### 1.5 持久化层
Dao 层，Service 层，Controller 层  
完成持久化工作的代码  
层界限十分明显  

### 1.6 为什么需要 Mybatis？以及**优点**  
帮助程序员将数据存入到数据库中。  
方便  
传统的 JDBC 代码太复杂了。简化，框架。自动化  
不用 Mybatis 也可以。更容易上手。技术没有高低之分。  

1. 简单易学：本身就很小且简单。没有任何第三方依赖，最简单安装只要两个 jar 文件 + 配置几个 sql 映射文件。易于学习，易于使用。通过文档和源代码，可以比较完全的掌握它的设计思路和实现。
2. 灵活：mybatis 不会对应用程序或者数据库的现有设计强加任何影响。 sql 写在 xml 里，便于统一管理和优化。通过 sql 语句可以满足操作数据库的所有需求。
3. 解除 sql 与程序代码的耦合：通过提供 DAO 层，将业务逻辑和数据访问逻辑分离，使系统的设计更清晰，更易维护，更易单元测试。sql 和代码的分离，提高了可维护性。
4. 提供映射标签，支持对象与数据库的 orm 字段关系映射。
5. 提供对象关系映射标签，支持对象关系组建维护。
6. 提供 xml 标签，支持编写动态 sql。
7. 使用的人多


### 2 第一个Mybatis程序
思路：搭建环境–> 导入 Mybatis–> 编写代码–> 测试！

### 2.1 搭建环境
搭建数据库