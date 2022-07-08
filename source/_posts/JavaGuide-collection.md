---
title: JavaGuide-collection
category: 大三下
date: 2022-06-27 16:13:08
tags:
---
##　知识点/面试题总结 ：
### Java 集合常见知识点&面试题总结(上) (必看 👍)
1. - Java集合
2. 集合概述
   1. Java 集合概览
   2. 说说 List, Set, Queue, Map 四者的区别？
   3. 集合框架底层数据结构总结
      1. List
      2. Set
      3. Queue
      4. Map
   4. 如何选用集合?
   5. 为什么要使用集合？
3. Collection 子接口之 List
   1. Arraylist 和 Vector 的区别?
   2. Arraylist 与 LinkedList 区别?
      1. 补充内容:双向链表和双向循环链表
      2. 补充内容:RandomAccess 接口
   3. 说一说 ArrayList 的扩容机制吧
4. Collection 子接口之 Set
   1. comparable 和 Comparator 的区别
      1. Comparator 定制排序
      2. 重写 compareTo 方法实现按年龄来排序
   2. 无序性和不可重复性的含义是什么
   3. 比较 HashSet、LinkedHashSet 和 TreeSet 三者的异同
5. Collection 子接口之 Queue
   1. Queue 与 Deque 的区别
   2. ArrayDeque 与 LinkedList 的区别
   3. 说一说 PriorityQueue


---

### Java 集合常见知识点&面试题总结(下) (必看 👍)
1. - Java集合
2. Map 接口
   1. HashMap 和 Hashtable 的区别
   2. HashMap 和 HashSet 区别
   3. HashMap 和 TreeMap 区别
   4. HashSet 如何检查重复
   5. HashMap 的底层实现
      1. JDK1.8 之前
      2. JDK1.8 之后
   6. HashMap 的长度为什么是 2 的幂次方
   7. HashMap 多线程操作导致死循环问题
   8. HashMap 有哪几种常见的遍历方式?
   9. ConcurrentHashMap 和 Hashtable 的区别
   10. ConcurrentHashMap 线程安全的具体实现方式/底层具体实现
    1. JDK1.7（上面有示意图）
    2. JDK1.8 （上面有示意图）
3. Collections 工具类
 1. 排序操作
 2. 查找,替换操作
 3. 同步控制

---
### Java集合使用注意事项总结
1. - Java集合
2. 集合判空
3. 集合转 Map
4. 集合遍历
5. 集合去重
6. 集合转数组
7. 数组转集合

### 源码分析 ：
1. ArrayList 源码+扩容机制分析
   1. 简介
      1. 动态数组，
      2. 继承cloneable
      3. 实现List,RandomAccess,Cloneable,java.io.Serializable
   2. arraylist和vector的区别
      1. arraylist线程不安全
      2. vector线程安全
   3. Arraylist和LinkedList的区别
      1. 都不保证线程安全
      2. 底层数据结构
         1. Arraylist 底层Object数组
         2. LinkedList 底层双向链表
      3. 插入和删除是否受元素位置的影响
         1. arraylist数组,受影响
         2. linkedlist链表,插入删除不受影响;但是如果指定的话,那就受影响
      4. 是否支持快速随机访问
         1. arraylist支持
      5. 内存空间占用:
         1. arraylist在list结尾预留
         2. linkedlist每一个元素都多消耗
2. HashMap(JDK1.8)源码+底层数据结构分析
3. ConcurrentHashMap 源码+底层数据结构分析