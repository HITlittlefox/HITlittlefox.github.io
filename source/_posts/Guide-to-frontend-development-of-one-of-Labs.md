---
title: Guide-to-frontend-development-of-one-of-Labs  
date: 2021-08-29 00:00:00  
tags:  
category: Java
---

#### Guide to frontend development of one of Labs

##### 利益相关：A frontend developer of this laboratory

(出于某种原因，暂简称为Lab)
-------------------------------------

#### **请注意：前端考核方式：（2021.8.30暂定）**

一. 限定时间内独立完成Web平台中所在项目的一个页面

1. 数据的添加、删除、编辑、多条件搜索
2. 若干前后端交互变量绑定
3. JavaScript相关代码解释（如request、if判断（如权限检验）、console.log、）
4. 熟练运用F12 DevTools查看网页情况（Console、Application、Network）

二. 可以看懂Service中所作页面对应的apis与module（如字段缺失或有错误），并及时反馈给后端。  
三. 能够使用Navicat图形化界面对数据库进行操作。  
备注：低代码平台的学习与mysql学习同步进行。
-------------------------------------

### 前置知识：

1. HTML、CSS、JavaScript（提醒：JavaScript将会是你在本项目担任Web前端时的主要编程工具，请务必看懂，并尝试使用js编程。）  
   参考资料：MDN-Web_technology_for_developers、菜鸟教程、Bilibili
2. Vue.js（可选，提醒：如果不学习Vue也可完成当前项目工作） 参考资料：MDN-Vue_getting_started、菜鸟教程-Vue.js、Bilibili
3. 提示：Web前端暂时不需要Git，但是如果可以在闲暇时间学习，必大有脾益，且有助于后续编程类工作开展。

### 主要内容：

1. 如果实验室项目前端部分有问题，可以联系我，联系时间：非就餐时间、非午休晚休时间。其他时间联系不到我就是“在忙”，请耐心等待或者将问题求助转接给其他前端人员。
2. 该实验室前端内容目前需要编写代码的内容为JavaScript; HTML、CSS、Vue.js内容均可由便捷化的低代码平台完成
3. 目前实验室可分为三块，前端web、后端service、数据库。 前端web需要能独立完成页面设计（会有规范），并了解后端service的一些过程，以及可以使用相关数据库软件清晰查看数据（mysql、navicat等）。

### 所需材料：

1. Lab Web前端 相关技术栈.zip（请找相关学长领取）
2. 最新规范（请找相关学长领取） 提醒：（前端规范跟随项目进度而实时变化，故采用在线文档，请不要修改）（如若修改，后果自负（且我拥有实时备份，可随时还原））
3. Web 系统账号密码（请找相关学长领取） 解释：考虑到入门之难度，故先将旧项目之一分配于新鲜血液，供以熟悉项目所用低代码平台与所用框架之细节。

### 学习顺序：

1. 先熟悉前端基础知识，
2. 然后看文件“前端编辑器”，同时看B站form和list视频，
3. 此时应该已经有了练手项目的账号密码，我会给每个人分配几个页面的任务，此时应该同时去看“前端修正记录.md”熟悉规范。

### 8.30前端知识点讲解

1. 从web系统中查看下列内容
    * request
        * 向后端请求
        * 获取方式
    * 绑定数据
    * html v-model（vue.js(可不学)），绑定变量
    * mdn：github有源码（最好能看看）
    * css class、id
    * js
    * js考核方式
    * 低代码平台
    * 前端编辑器
    * action（部分js）
    * 属性、事件
    * input table（绑定变量）
    * service navicat（后续需要下载）
    * date-selector
    * F12
2. 任务
    * 加快前端三剑客的学习进度
    * 登录德令哈前端并打开德令哈项目
    * 查看企业信息目录下的各项列表
    * 根据最新规范思考如何改造（暂不修改等通知）

### 8.30晚，低代码平台service讲解

* axios、request前后端交互演示
    * 向后端请求内容
    * then（请求成功后的操作）
    * if() 则...
    * else...
* params 低代码平台可实现省略自己写前后端联结的内容 直接在params 处输入字段

### 8.31前端知识

* 目的 优化DLH页面
    * DLH原有目录：
        * add:从0到1（从有到无）
        * edit：在之前存在的内容基础上进行修改
        * show：只能查看，不能修改
        * list  
          add、edit、show三个功能各自一个表单，表单内容完全相同，但一旦修改任一功能内的内容就要同时修改另外两个页面的内容，使其保持一致

    * 原有版本缺陷：重复性工作、修改负担
* 优化后DLH:
    * xxx_form
    * xxx_form_import
    * xxx_list  
      add、edit、show都指向一个表单，因此这三个功能的操作都是对同一个表单进行的
    * add：一共三个参数（page，xxx_form，{op:"add",title:""}
    * edit、show与add的参数几乎一致（title不同），在{}内部多了id（类似身份证，实则为主键通过SQL定位到后端被操作的数据）这一内容
* 必填且不可修改内容（请查看最新规范）
    * 必填：校验（NotNull NotEmpty）
    * 不可修改：除了add功能时其他情况只读  
