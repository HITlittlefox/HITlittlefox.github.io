---
title: springboot笔记
category: 我要就业
date: 2022-08-15 10:15:52
tags:
---

### run方法流程分析
![run方法流程分析](https://raw.githubusercontent.com/HITlittlefox/pictures/master/images/20220815101619.png)

### 配置文件
1. application.properties
    1. 语法结构 ：key=value
2. application.yml
    1. 语法结构 ：key：空格 value
3. 场景
    1. 字面量：普通的值  [ 数字，布尔值，字符串  ]
    2. 对象、Map（键值对）
    3. 数组（ List、set ）
    4. 修改SpringBoot的默认端口号
    5. 给实体类直接注入匹配值

### [以HttpEncodingAutoConfiguration（Http编码自动配置）为例解释自动配置原理；](https://mp.weixin.qq.com/s?__biz=Mzg2NTAzMTExNg==&mid=2247483766&idx=1&sn=27739c5103547320c505d28bec0a9517&scene=19#wechat_redirect)
1. 一句话总结 ：根据当前不同的条件判断，决定这个配置类是否生效！
    1. 一但这个配置类生效；这个配置类就会给容器中添加各种组件；
    2. 这些组件的属性是从对应的properties类中获取的，这些类里面的每一个属性又是和配置文件绑定的；
    3. 所有在配置文件中能配置的属性都是在xxxxProperties类中封装着；
    4. 配置文件能配置什么就可以参照某个功能对应的这个属性类
2. 精髓
    1. SpringBoot启动会加载大量的自动配置类
    2. 我们看我们需要的功能有没有在SpringBoot默认写好的自动配置类当中；
    3. 我们再来看这个自动配置类中到底配置了哪些组件；（只要我们要用的组件存在在其中，我们就不需要再手动配置了）
    4. 给容器中自动配置类添加组件的时候，会从properties类中获取某些属性。我们只需要在配置文件中指定这些属性的值即可；
        1. xxxxAutoConfigurartion：自动配置类；给容器中添加组件
        2. xxxxProperties:封装配置文件中相关属性；