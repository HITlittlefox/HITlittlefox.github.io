---
title: mall-notes
category: 大三下
date: 2022-06-19 18:37:36
tags:
---

备注：
macrozheng/mall: mall项目是一套电商系统，包括前台商城系统及后台管理系统，基于SpringBoot+MyBatis实现
https://github.com/macrozheng/mall

1. 防火墙状态
   1. systemctl status firewalld
   2. systemctl start firewalld
   3. systemctl stop firewalld
   4. firewall-cmd --reload
2. docker启动过程：
   1. systemctl start docker
   2. docker images
   3. docker start elasticsearch
      1. http://192.168.138.128:9200/
   4. docker start rabbitmq
      1. http://192.168.138.128:15672/
   5. docker start kibana
      1. http://192.168.138.128:5601/


