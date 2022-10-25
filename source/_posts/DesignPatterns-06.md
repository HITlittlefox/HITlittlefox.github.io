---
title: DesignPatterns-06
category: Java
date: 2021-11-29 16:31:28
tags:
---
3 uc
4 domain model class

0. Outline
   1. 设计要素
   2. 系统设计的输入和输出

1. Overview
分析-设计-实现
分析与实现的桥梁是设计

2. 什么是系统设计
   1. 主要目的
   2. 网络图   
   3. 设计的主要组件和层次
      1. 系统界面、系统接口√
      2. 数据库的设计
      3. 用户界面√
      4. 应用程序的设计√
      5. 环境设计√
      6. 安全与控制
   4. 架构设计、细节设计
3. 系统设计的输入、输出
4. 系统设计活动（系统开发周期的6个活动流）
   1. 第3个活动流发掘和理解细节 8 9 ；第4个活动流是设计系统元件。6 7 10 11
   2. 环境：硬件、软件、网络
   3. 应用：分系统的子系统、架构设计、每一个用例的细节设计
   4. 系统界面、系统接口（交互的形式，提前规定好的格式）如XML
   5. 用户界面UI（看到的界面）
   6. 数据库 Database
   7. 系统控制和安全
5. 设计环境
   1. 设计内部部署：Design for Internal Deployment
      1. 单机软件系统
      2. 基于网络的内部系统 LAN(Local area netword)，客户机-服务器架构
      3. 桌面程序、基于浏览器的程序
      4. 三层客户端/服务器架构：
         1. 界面层（视图）
         2. 业务逻辑层（域层）（domain层）（model层）
         3. 数据层（data层）
   2. 设计外部部署：Design for External Deployment
      1. 为互联网部署进行的配置 Configuration for Internet Deployment
         1. Advantages
         2. Potential Problems
         3. Security
      2. 为互联网部署做出的托管选择（场地出租） Hosting Alternatives for Internet Deployment
         1. Hosting
         2. Issues when considering hosting alternatives
         3. Colocation
         4. 可管理的服务 Managed Services
         5. Virtual servers
         6. Cloud Computing
         7. Service Level Agreement
      3. 带有互联网部署的客户设备的多样性 Diversity of Client Devices with Internet Deployment
         1. Full size devices
         2. Mid level tablet devices
         3. Small mobile computing devices
      4. 设计远程和分散的环境 Design for Remote, Distributed Environment
         1. Two interfaces to same Web app for internal vs. external access
         2. Virtual private network (VPN)
         3. >第六章复习题剩余做完
   3. 术语
      1. LAN
      2. 客户机-服务器架构
      3. 客户机电脑
      4. 服务器电脑
      5. 基于网页的互联网架构
      6. >课堂作业：第六章1-12 结构-->架构
   4. 