---
title: DesignPatterns-04
category: Java
date: 2021-11-15 16:13:39
tags:
---
## Chapter 4 
0. 事物 Things
   1. 数据实体 Data entities
   2. 域类 Domain classes
1. Overview
2. 问题域中的“事物”(Things)
   1. 问题域是什么 problem domain(specific area)
   2. 事物是什么 Things(need to be remembered))
   3. Examples
   4. modeled as domain classes or data entities
   5. 名称
      1. 设计模式中叫domain classes
      2. 数据库中叫data entities
   6. 两种定义问题域中的事物的方法 Two Techniques for Identifying them
      1. **头脑风暴法** Brainstorming Technique
         1. 步骤 steps
      2. **名词技术** Noun Technique
         1. 步骤 steps
         2. **名词列表**
      3. 属性 Attribute
         1. 标识符、关键字
         2. 复合属性
      4. 事物间的联系 Associations among things(事件之间的关系、关联)(关联、泛化、依赖、实现)
         1. 关系：是指类与类的关系link链接
         2. 关联（联系）
         3. 基数（重数）
         4. 基数限制
         5. 二元关系、一元关系、三元关系、n元关系
         6. **实体联系图**（ER图）
         7. called relatoinship on ERD(Entities relationship diagram ER图，数据库) in database class
         8. association and relationships apply in two directions
            1. customer --> order
            2. customer <-- order
            3. Minimunm and Maximum Multiplicity
               1. 一个订单的实例 不可以 两个不同的客户下单 (1 to 1)
               2. 一个客户 可以 下多个订单 (1 to many)
         9.  Types of Associations
             1.  Binary Association
             2.  Unary Association
             3.  Ternary Association
             4.  N-ary Association
3. **域模型类图** The Domain Model Class Diagram
   1. 类 Class
   2. 域类 Domain Class
   3. 类图 Class Diagram
   4. **域模型类图** Domain Model Class Diagram
      1. 驼峰符号
      2. 域模型类图符号
      3. **关系** association(有方向、可以有名称、多重性)
      4. key关键字
      5. 双向多重关联
      6. Association Class：关联类：虚线(ppt28解决grade应该在哪里，多对多问题)
   5. **有关对象类的更复杂的问题** More Complex Issues about Classes:Generalization/Specialization Relationships
      1. 方向的含义：先有同学再有班级，班级依赖于同学。A依赖于B，A实线空箭头指向B。A是子类，B是父类。 
      2. **泛化/特化联系** 继承、继承联系 Generalization/Specialization(泛化、具体) 
         1. 父类、子类
         2. abstract class 抽象类
         3. concrete class 具体类
      3. **整体/局部联系** Whole Part Relationships(整体类、部分类)
         1. **聚合** aggregation 实线空心菱形
         2. **组合** composition 实线填充菱形
      4. UML图总结：
         1. 从静态角度、从动态角度去看
         2. use case diagram：用例图
         3. activity diagram：活动图
         4. domain model class diagram：域模型类图(静态)
         5. **必考!(4~5个类)** 4-23 名称、属性、关系（方向、名字、多重性）、三大more关系
         6. >课后题22~34；问题和练习：3+10

------
1. 第一章总览 1 2 3用例 4域模型 5
2. 第二部分：核心活动流第3个流
3. 第三部分：第六章讲完了，第4个核心流：设计  第7章：标题
4. 第四部分：8 9
5. 第五部分：10 11 12系统的实现


(判断题10个、单项选择题20)教材要点部分、
简答题10（5分）（课后复习题找的，比较重要的）、
两个大题（一个题10分，文字分析-->分析+画图）、
第九章可能有计算题

平时作业按时提交