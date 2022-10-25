---
title: DesignPatterns-05
category: Java
date: 2021-11-22 16:52:16
tags:
---
## Chapter 5
第3章:use cases
第4章:domain classes
第5章:additional techniiques and models to extend the requirement models to show more detail
*developed use case descriptions*
*activity diagrams*
1. *developed use case descriptions*
2. *activity diagrams*
3. System Sequence Diagram(SST)
4. State Machine Diagram(动态机图，状态图)
---
1. 用例描述 Use Case Description (Table Chart) (use case 动词短语(动名词))
   1. **简单的用例描述** Brief use case description
   2. **完全展开的用例描述** Fully Developed Use Case Description(p93图5-3)
      1. **用例描述包含什么、含义、给一段文字会写用例描述**
      2. use case name
      3. 场景 scenario （可能场景不同--导致活动流不同）
      4. 触发事件 triggering event 
      5. 参与者 actor 
      6. 相关用例
      7. 利益相关者
      8. **前置条件** preconditions
      9. **后续条件** postconditions
      10. **活动流** flow of activities 两列(Actor,System) 交互
      11. 业务 business--
      12. 异常 Exception(针对前面正常的流程)
      13. >习题:1~8、问题与练习1
   3. **用例活动图** use case activity diagram 用活动图来描述活动流
   4. **系统顺序图** system sequence diagram(SSD)
      1. **系统顺序图符号**
      2. 参与者、系统
      3. **生命线、对象生命线**
      4. 循环框架
      5. 真/假条件
      6. 一条信息的完整符号
      7. 针对一个用例的！不是针对一个系统的！
      8. 一个[关于系统的]UML的顺序图
      9. 顺序图的一例
         1. 只显示参与者actor和一个对象object
         2. 一个对象代表着全部系统
         3. 为用例，显示输入输出信息的需求
      10. object 命名(Name)  
          1. :System 匿名对象
          2. A:System 对象名字是A 
      11. steps for developing SSD
          1. 识别输入信息
          2. 用消息语法来描述外部参与者传递给系统的信息
          3. 识别输入语法的特殊条件
          4. 识别并且添加输出返回值
   5. **开发系统顺序图**
      1. 步骤
   6. **状态机图** State Machine Diagram (SMD)
      1. 复合状态和并发性 composite state
         1. 并发、并发状态
         2. 复合状态：嵌套状态和转换路径
         3. 路径
         4. 复合状态图
      2. 针对一个对象！（依赖于某个class）
      3. 状态机图
         1. 一种UML图，展示着对象的生命状态和转变
      4. 状态
         1. 当符合某些标准，表现某些行动，或者等待
      5. 转移
         1. 从一个状态到另一个状态的移动
      6. 行为描述
         1. 一部分转变活动的描述
      7. 伪状态：起始点
      8. 初始状态：转变前的最初的状态
      9. 目的条件：转变后的状态
      10. 判定条件：判定转变是否发生的条件
   7. 开发SMD的步骤（大概有个了解）
      1. 看类图class diagram并找出需要状态机图描述的类图
      2. 为每个类创造状态条件的清单
      3. 通过识别可以造成对象离开已识别状态的转变，来构造表
      4. Sequence these states in the correct order and aggregate combinations into larger fragments
      5. Review paths and look for independent, concurrent paths
      6. Look for additional transitions and test both directions
      7. Expand each transition with appropriate message event, guard condition, and action expression
      8. Review and test the state machine diagram for the class
   8. extending and integrating requirements models
      1. use cases
         1. use casse diagram
            1. use case description
            2. activity diagram
            3. SSD
      2. Domain Classes
         1. Domain model class diagram
            1. SMD
            2. >复习题：全做，18与10重复。+问题与练习：2+3+读懂6状态机图（模仿打印机）**（可能会考！）**