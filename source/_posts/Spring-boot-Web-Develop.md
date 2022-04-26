---
title: Spring-boot-Web-Develop  
category: Java  
date: 2021-09-07 08:01:15  
tags:
---

### The class was taught by a charismatic professor.

1. 框架应用、较为主流、市场需求强烈 R \ spring boot\
2. 难度大；**三次作业**；大量作业；仅有32学时但是课下要补很多知识。
3. 结构

web开发：前端、后端、链接  
前端：（HTML5 CSS3 JS6）
> 页面结构HTML  
> 是页面变得好看的技术CSS  
> 页面动起来JavaScript  
> 懒人推动社会进步jQuery

前端升级：
> 设计困难解决方法：BootStrap  
> 解耦合、数据和表现分开Vue

后端：
> 首先要学会基础**java**  
> 数据放在数据库MySQL  
> 最基本的B/S两层架构JSP  
> 再多加一层，把数据取出来JSP  
> 页面刷新Ajax

链接：
> 一场旷日持久的战争--解耦合框架Framework  
> 千呼万唤始出来，spring boot  
> 层次越多越高级，mybatis plus

    B/S C/S架构区分
    Browser Client 
    表现层、（前端）
    业务层、（后端）
    数据库层（后端）
    所有业务逻辑的处理和数据存储都是**后端**做的
    （都有连接方式axios ajax吧啦吧啦）

工业标准：普遍采用的实现方法

JSP-structs-spring-springboot-docker

考核方式：交作业

小组交作业：2~3次作业  
（一个组最多2个人：前端、后端：各一个）

1. 第一节结束就要做：开始写代码
2. JSP开发
3. SpringBoot作业


1. HTML 页面元素的摆放布局
2. CSS 装修

网站：mdn w3school runoob  
HTML与HTML5区别

flash： 安全隐患  
性能要求高（2010移动互联网）

文本/文件在哪里？ B/S Sever Browser 在浏览器端打开的一定是一张html页面

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8">
		<meta http-equiv="X-UA-Compatible" content="IE=edge">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>Document</title>
	</head>
	<body>
		Hello world!
	</body>
</html>
```

14 September,2021  
内联样式表、外联样式表、JS、吧啦吧啦

16 September,2021  
**JSP(Java Server Pages)**
JSP全称Java Server Pages，是一种动态网页开发技术。它使用JSP标签在HTML网页中插入Java代码。标签通常以<%开头以%>结束。

JSP的基础(菜鸟教程)

26 September,2021  
数据库链接数据库:  
Connection-->Statement-->ResultSet

### 2021-10-05 做完作业啦~

1. 做完作业webShop
2. JavaScript Asynchronous JS异步编程
   1. 异步不一定多线程 多线程不一定异步
   2. 异步 只是把事情交给别人去处理， 实际上 事情本身所花的时间并不会减少，只是花费的时间转移到别的人身上了，但是同时能做别的事，所以提高了并发
   3. 多进程内存开销太大
   4. 异步是目的，多线程是方法

3. 还讲了讲Ajax

### 2021-10-11 提交作业
Ajax演示

### 2021-10-14 spring boot 开讲
1. jsp 耦合程度高 ---> 所以要学习spring boot
2. 概念解释：MVC
    1. Model（模型） - 模型代表一个存取数据的对象或 JAVA POJO。它也可以带有逻辑，在数据变化时更新控制器。
    2. View（视图） - 视图代表模型包含的数据的可视化。
    3. Controller（控制器） - 控制器作用于模型和视图上。它控制数据流向模型对象，并在数据变化时更新视图。它使视图与模型分离开。
3. 母公司：Pivotal
4. spring boot 配置
   1. 历史
      1. spring--框架--有很多变种
      2. 这之前有hibernate、structs
      3. 后二者结合诞生spring（SSH框架）
      4. 为了简化，出现了spring mvc
      5. 为了简化，出现了spring boot
   2. 配置
      1. 新建
      2. 包导入（导入依赖）
      3. .yml
      4. structure  web.xml(\src\main\webapp)
      5. .yml
      6. mappersource
      7. tip：约定>配置

### 2021-10-19 vue开讲、json开讲
jQuery使用ajax
前端vue适配
双向绑定

### 2021-10-21 操作数据库
springboot+mybatis plus  操作数据库
做一个添加商品的页面
1个jsp+1个controller

点击后ajax可以连续添加

link

springboot获得地址栏内容

添加、修改、

### 2021-10-26 mybatisplus封装好的方法
超链接修改、按钮删除

HttpSession
session.setAttribute
判断有无值
Redis共享Session


### 总结
前端
   1. CSS HTML JavaScript jQuery Vue JSON
   2. 表现、动作、数据
后端
   1. MVC架构  controller    
   2. mybatisPlus、mysql

又讲了JSP（五重要对象，request、response···）

Java

spring boot



### 作业：
1. JSP功能全部用spring boot实现，再在这个原来的基础之上：商品的增删改
2. 基于spring boot + mybatis plue + vue + Ajax + bootstrap(美化、加分项)
3. 作业时间：11月30日 晚上之前；12月1日凌晨之前 交给DLN。