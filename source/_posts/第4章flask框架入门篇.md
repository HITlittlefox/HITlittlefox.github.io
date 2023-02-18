---
title: 第4章flask框架入门篇
category: PythonFlask构建微信小程序订餐系统
date: 2023-02-12 17:17:01
tags:
---

### Flask

1.  hello world
2.  路由规划
    1. 蓝图
3.  [链接管理器(封装)url_for](https://flask.net.cn/api.html#flask.url_for)
    1.  根据视图方法名找到对应链接 UrlManager.buildUrl("/api")
4.  版本管理
5.  日志 app.logger.error()
6.  错误处理器
    1. 捕获修复
7.  数据库 ORM
    1. Flask-SQLAlchemy
8.  ```markdown
    |-- application.py # flask 中的全局变量，包括 APP，数据库等
    |-- common # 相当于 utils，存放公共部分
    | |-- **init**.py
    | |-- libs # 公共方法或者类
    | |-- models # MVC 中的 models 层
    |-- config # 配置文件
    | |-- base_setting.py # 基础设置
    | |-- **init**.py
    | |-- local_setting.py # 本地开发环境
    | `-- production_setting.py	# 生产环境
    |-- docs	# 文档存放部分
    |   `-- mysql.md # 所有数据库变更记录
    |-- jobs # 定时任务
    | |-- bash_jobs # 脚本文件
    | |-- **init**.py
    | |-- launcher.py # 自定义命令行启动
    | |-- readme.md
    | `-- tasks	# 定时任务
    |-- manager.py	# 启动入口
    |-- readme.md
    |-- requirements.txt	# 后端所需包
    |-- uwsgi.ini	# 部署配置文件
    |-- web		# 交互
    |   |-- controllers	# MVC中的C，控制器部分
    |   |-- __init__.py
    |   |-- interceptors	# 拦截器部分
    |   |-- static	# 静态文件
    |   `-- templates # 模板文件
    `-- www.py # HTTP 模块相关初始化
    ```
9.  flask_script 扩展命令行
10. 加载不同环境的配置
