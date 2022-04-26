---
title: DesignPatterns-03
category: Java
date: 2021-11-08 17:33:15
tags:
---
## Chapter 3 
Event
类图√ 活动图√ 用例(本章)
USE Case(用例)
1. Overview
   1. Waiters on Call
   2. 怎么找use cases
      1. user goal
      2. event decomposition
   3. S.A.
      1. business process(chapter3)-events
      2. information(chapter4)-things
2. **用例和用户目标** (定义、发现)Use Cases and User Goals
   1. 什么是用例？an activity that the system performs, usually in response to a request by  a user
   2. 两种定义用例的技术：**用户目标技术**、**事件分解技术**。
   3. **用户目标技术8步骤** User Goal Technique: Specific Steps--8步骤
      1. 动名词短语
      2. Detail(第5章)
3. **事件分解技术** Event Decomposition Technique
   1. **基本业务流程** EBP
   2. **事件** Event
   3. **事件类型** Types of Events
      1. **外部事件** External Events:an event that occurs outside the system, usually initiated by an external agent
      2. **临时事件** Temporal Events:an event that occurs as a result of reaching a point in time
      3. **状态事件** state event:
         1. an event that occurs when something happens inside the system that triggers some process
         2. reorder point is reached for inventory item(到达一个水平线的时候，重新下单)
   4. **外部事件清单** External Event Checklist
      1. **外部事件清单** External Event Checklist:
         1. External agent or actor wants something resulting in a transaction
            1. Customer buys a product
         2. External agent or actor wants some information
            1. Customer wants to know product details
         3. External data changed and needs to be updated
            1. Customer has new address and phone
         4. Management wants some information
            1. Sales manager wants update on production plans
      2. **临时事件清单** Temporal Event Checklist
         1. Internal outputs needed at points in time
            1. Management reports (summary or exception)
         2. Operational reports (detailed transactions)
            1. Internal statements and documents (including payroll)
         3. External outputs needed at points of time
            1. Statements, status reports, bills, reminders
   5. **定义事件** Identifying Events
      1. **事件/前提条件和响应** Events versus Prior Conditions and Responses
      2. **事件序列**：追踪事务处理的生命周期 The Sequence of Events: Tracing a Transaction’s Life Cycle
      3. **技术依赖和系统控制** Technology-Dependent Events and System Controls
         1. 系统控制是什么？
      4. **理想技术假设**
         1. 理想技术假设是什么？
      5. **事件分解技术**--7步骤
4. **用例、参与者和符号** Use Cases and CRUD Technique(Create, Report, Update, and Delete增删改查)(信息工程方法)
   1. **参与者**、**自动化边界**
   2. **用例图**
   3. For Customer domain class(对于客户域类), verify that there are use cases that create, read/report, update, and delete (archive) the domain class
   4. CRUD Technique Steps
5. RMO案例中的use cases
   1. 子系统（用例相关性）、架构
6. 用例图(UC actor )
   1. 方向（单向、双向）（可能有个单向箭头）
   2. 子系统用例图，显示所有参与者
   3. 子系统用例图，显示所有顾客参与者
   4. 用例之间的关系（包含关系 <<includes>> relationship）
      1. UML有四种关系：关联、依赖、泛化、实现
      2. >作业：第三章课后题19题可不做，+问题与练习3+11