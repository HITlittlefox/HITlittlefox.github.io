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

1. 搭建环境
    1. 数据库
        ```sql
        CREATE DATABASE `mybatis`;


        CREATE TABLE `users`(
        `id` INT(20) NOT NULL PRIMARY KEY,
        `name` VARCHAR(30) DEFAULT NULL,
        `pwd` VARCHAR(30) DEFAULT NULL

        )ENGINE=INNODB DEFAULT CHARSET=utf8;


        INSERT INTO `users` (`id`,`name`,`pwd`) VALUES
        (1,'小红','123456'),
        (2,'小明','783456'),
        (3,'小蓝','893456');
        ```
    2. 依赖
        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <project xmlns="http://maven.apache.org/POM/4.0.0"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
            <modelVersion>4.0.0</modelVersion>

            <groupId>org.lxl</groupId>
            <artifactId>mybatis</artifactId>
            <packaging>pom</packaging>
            <version>1.0-SNAPSHOT</version>
            <modules>
                <module>mybatis-01</module>
            </modules>

            <properties>
                <maven.compiler.source>8</maven.compiler.source>
                <maven.compiler.target>8</maven.compiler.target>
            </properties>
            <dependencies>
                <!--junit依赖-->
                <dependency>
                    <groupId>junit</groupId>
                    <artifactId>junit</artifactId>
                    <version>4.12</version>
                </dependency>
                <!--mysql依赖-->
                <dependency>
                    <groupId>mysql</groupId>
                    <artifactId>mysql-connector-java</artifactId>
                    <version>5.1.47</version>
                </dependency>
                <!--mybatis依赖-->
                <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
                <dependency>
                    <groupId>org.mybatis</groupId>
                    <artifactId>mybatis</artifactId>
                    <version>3.5.2</version>
                </dependency>
            </dependencies>
            <build>
                <resources>
                    <resource>
                        <directory>src/main/java</directory>
                        <includes>
                            <include>**/*.xml</include>
                            <include>**/*.properties</include>
                        </includes>
                    </resource>

                    <resource>
                        <directory>src/main/resources</directory>
                        <includes>
                            <include>**/*.xml</include>
                            <include>**/*.properties</include>
                        </includes>
                    </resource>
                </resources>
            </build>
        </project>
        ```
2. 创建一个模块
    1. mybatis-config.xml 编写 mybatis 核心配置文件
        ```xml
        <?xml version="1.0" encoding="UTF-8" ?>
        <!DOCTYPE configuration
                PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
                "http://mybatis.org/dtd/mybatis-3-config.dtd">
        <configuration>
            <environments default="development">
                <environment id="development">
                    <transactionManager type="JDBC"/>
                    <dataSource type="POOLED">
                        <property name="driver" value="com.mysql.jdbc.Driver"/>
                        <property name="url"
                                value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=utf-8"/>
                        <property name="username" value="root"/>
                        <property name="password" value="root"/>
                    </dataSource>
                </environment>
            </environments>

            <mappers>
                <mapper resource="com/lxl/dao/UserMapper.xml"/>
            </mappers>

        </configuration>
        ```
    2. MybatisUtils 编写 mybatis 工具类
        ```java
        package com.lxl.utils;
        import org.apache.ibatis.io.Resources;
        import org.apache.ibatis.session.SqlSession;
        import org.apache.ibatis.session.SqlSessionFactory;
        import org.apache.ibatis.session.SqlSessionFactoryBuilder;

        import java.io.IOException;
        import java.io.InputStream;

        //编写 Mybatis 工具类 获取SqlSessionFactory
        public class MybatisUtils {

            private static SqlSessionFactory sqlSessionFactory = null;

            static{//静态代码块封装   从一开始就会加载
                String resource = "mybatis-config.xml";
                try {
                    InputStream inputStream =  Resources.getResourceAsStream(resource);
                    sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            //获取sqlSession  对象
            public static SqlSession getSqlSession(){
                return sqlSessionFactory.openSession();
            }
        }
        ```
3. 编写代码
    1. User 编写实体类
        ```java
        package com.lxl.pojo;

        public class User {
            private int id;
            private String name;
            private String pwd;

            public User() {
            }

            public User(int id, String name, String pwd) {
                this.id = id;
                this.name = name;
                this.pwd = pwd;
            }

            public int getId() {
                return id;
            }

            public void setId(int id) {
                this.id = id;
            }

            public String getName() {
                return name;
            }

            public void setName(String name) {
                this.name = name;
            }

            public String getPwd() {
                return pwd;
            }

            public void setPwd(String pwd) {
                this.pwd = pwd;
            }

            @Override
            public String toString() {
                return "User{" +
                        "id=" + id +
                        ", name='" + name + '\'' +
                        ", pwd='" + pwd + '\'' +
                        '}';
            }
        }
        ```
    2. UserMapper 编写接口
        ```java
        package com.lxl.dao;

        import com.lxl.pojo.User;

        import java.util.List;

        public interface UserMapper {
            public abstract List<User> getUserList();
        }
        ```
    3. UserMapper.xml 编写配置文件
        ```xml
        <?xml version="1.0" encoding="UTF-8" ?>
        <!DOCTYPE mapper
                PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
                "http://mybatis.org/dtd/mybatis-3-mapper.dtd">


        <!--namespace 命名空间 ： 这里等价于之前缩写的 UserDaoImp  指向一个Mapper接口-->
        <mapper namespace="com.lxl.dao.UserMapper">
            <!--    id 表示的是实现 namespace 中所对应接口的方法   resultType 表示的是返回值类型  -->
            <select id="getUserList" resultType="com.lxl.pojo.User">
                select *
                from mybatis.users
            </select>
        </mapper>
        ```
4. 测试
    ```java
    package com.lxl.dao;

    import com.lxl.pojo.User;
    import com.lxl.utils.MybatisUtils;
    import org.apache.ibatis.session.SqlSession;
    import org.junit.Test;

    import java.util.List;

    public class UserMapperTest {
        @Test
        public void test() {
            //获取 SqlSession 对象
            SqlSession sqlSession = MybatisUtils.getSqlSession();

            //从接口的反射类 获得相应的 mapper
            UserMapper mapper = sqlSession.getMapper(UserMapper.class);
            List<User> userList = mapper.getUserList();

            for (User user : userList) {
                System.out.println(user);
            }
            //关闭资源
            sqlSession.close();
        }
    }
    ```
5. 可能遇到的问题
    1. 配置文件没有配置
    2. 绑定接口错误
    3. 方法名不对
    4. 返回类型不对
    5. Maven 导出资源问题
    6. 数据库连接问题
    7. 标签不要写错
    8. namespace 必须是.
    9. resource 中必须是 / 隔开
    10. 程序配置文件必须符合规范
    11. 空指针异常问题，sqlSessionFactory
    12. 输出的 xml 文件中存在中文乱码问题

### 3 CRUD
1. namespace : namespqce 中的包名要和接口的包名一致。
2. select, insert, update, delete
    1. id：就是对应的 namespace 中的方法名；
    2. resultType：sql 语句的返回值 类型在包中的位置
    3. parameter：参数类型
    4. 步骤(以select为例):
        1. 编写接口
            ```java
            public interface UserMapper {
                // 查询全部用户
                List<User> getUserList();
            }
            ``` 
        2. 编写 sql 
            ```xml
            <!--namespace 命名空间:这里等价于之前缩写的 UserDaoImp  指向一个Mapper接口-->
            <mapper namespace="com.lxl.dao.UserMapper">
                <!--id 表示的是实现 namespace 中所对应接口的方法
                resultType 表示的是返回值类型  -->
                <select id="getUserList" resultType="com.lxl.pojo.User">
                    select *
                    from mybatis.users
                </select>
            ```
        3. 测试
            ```java
            @Test
            public void test() {
                //获取 SqlSession 对象
                SqlSession sqlSession = MybatisUtils.getSqlSession();
                //从接口的反射类 获得相应的 mapper
                UserMapper mapper = sqlSession.getMapper(UserMapper.class);
                
                List<User> userList = mapper.getUserList();
                for (User user : userList) {
                    System.out.println(user);
                }
                
                //关闭资源
                sqlSession.close();
            }
        ```
3. 万能的 Map : 假设我们实体类或数据库中的字段过多，我们应当考虑使用 Map ,可以用来若干字段CRUD 
    1. 编写接口
        ```java
        // 万能的Map，添加用户
        int addUser2(Map<String, Object> map);
        ```
    2. 编写 sql 
        ```java
        <insert id="addUserByMap" parameterType="map">
            insert into mybatis.users (id, name, pwd)
            values (#{userid}, #{username}, #{userpwd});
        </insert>
        ```
    3. 测试
        ```java
        // 万能Map，增删改需要提交事务
        @Test
        public void addUserByMap() {
            SqlSession sqlSession = MybatisUtils.getSqlSession();
            UserMapper mapper = sqlSession.getMapper(UserMapper.class);

            Map<String, Object> map = new HashMap<>();
            map.put("userid", 6);
            map.put("username", "小华");
            mapper.addUserByMap(map);
            // 提交事务
            sqlSession.commit();

            sqlSession.close();
        }
        ```
    4. 小知识点
        1. Map 传递参数，直接在 sql 中取出 Key 即可
        2. 对象传递参数，直接在 sql 中取对象的即可
        3. 只有一个基本数据类型，可以不写，可以直接在 sql 中取到
        4. 多个参数使用 Map，或者注解