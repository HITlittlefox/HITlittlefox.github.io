---
title: git-note  
date: 2021-08-25 00:00:00  
tags:  
category: Java
---

#### 令我写下这篇文章的，是2021夏项目前期的前后端、运维之间缺乏沟通而导致的代码版本控制一塌糊涂。

#### 目的：不多事、不复杂、简化操作，让不懂git的也能懂版本控制。

场景：项目-master  
— dev-coder1  
-coder2  
本地有两个branch，一个dev，一个coder1

如果coder1想要提交自己已完善的代码到dev，我目前已知两种方法。    
方法1：把dev分支`git pull`更新最新版本到本地，在命令行中`git merge coder1`到dev，从dev `git add .` `git commit -m ""` `git push`
，完成dev的最新版本的更新。(gitlab的mr有在合并后自动删除分支的功能)(最好是这样的:coder1每次改一个功能都创建一个分支,改完，合并后就删掉)  
方法2：把coder1分支`git add .` `git commit -m ""` `git push`，完成coder1分支的最新版本的更新，再从网页上如gitlab进行`pull request`
或者merge申请，指定上游审计代码并完成merge。

请记住，使用第二种会让你少很多事。