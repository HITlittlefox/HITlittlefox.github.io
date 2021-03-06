---
title: algorithm01
category: 大三下
date: 2022-06-23 10:00:06
tags:
---

## 1. 位运算、算法、简单排序

1. 位运算与正负数
2. 算法到底是什么
   1. 明确知道怎么解
   2. 明确知道怎么尝试（图灵）
   3. 案例：阶乘的和
3. 简单排序
   1. selectionSort
   2. bubbleSort
   3. insertSort及其优化



##　2. 数据结构、前缀和、对数器

1. 数据结构分类
   1. 数组：连续结构
      1. 便于寻址；不便于增删数据
   2. 单链表、二叉树、图：跳转结构
      1. 不便于寻址；便于增删数据
2. 前缀和数组（为了解决需求：数组中[L...R]之间的sum）
   1. 制作HELP数组，每一个值，是本下缀的值与前一个下缀的值的和
   2. H[i]=sum(arr[0...i])（HELP数组第i个值：是arr数组从0累加到i）
   3. 例：求3-7的和：H[7]-H[5]
   4. [L...R]之间的sum
      1. L==0，H[R]
      2. L!=0，H[R]-H[L-1]
3. Math.random()
   1. 返回[0,1)的一个小数,[0,x)范围上的数出现概率是x²
4. **从1~5随机到1~7随机**（黑盒）
   1. 题目：
      1. 条件函数`f`，可以等概率返回1-5的数
      2. 目标函数`g`，可以等概率返回1-7的数
   2. 题解：
      1. 先用条件函数`f`获得一个`f2()`=0-1等概率发生器：
         1. 如果得到1、2就返回0，
         2. 如果得到4、5，就返回1，
         3. 如果得到3，就重新调用f。
      2. `f3()`=0~7等概率发生器：需要三个`f2()`=0-1等概率发生器：
         1. _ _ _ 才能8个结果等概率
      3. `f4()`=0~6等概率发生器 
         1. 如果遇到7，就重新调用`f3()`
         2. 如果得到0 1 2 3 4 5 6，就可以了
      4. `0~6`+1 ==> `1~7`
         1. `f4()`+1
5. **从a~b随机到c~d随机**（黑盒）
   1. 常见题目：
      1. 条件函数`f`，可以等概率返回3-19的数
      2. 目标函数`g`，可以等概率返回17-56的数
   2. 题解：
      1. 获得01等概率发生器：
         1. 3-10：0 
         2. 11 ：重做
         3. 12-19：1
      2. 56-17=39也就是去制作0~39等概率发生器+17
         1. 看看需要几个二进制位
         2. \_ _ _ _ _
         3. 2^6>=39 n=5
         4. 6个位时,是0-63>39,可以做到0-63位等概率返回
         5. 若大于39，就重做
6. **01不等概率随机到01等概率随机**
   1. 题目
      1. 条件函数`f`，0：p概率，1：(1-p)概率
      2. 目标函数`g`，可以等概率返回0和1
   2. 题解：
      1. f*f
         1. 00:重做
         2. 11:重做
         3. 01:0
         4. 10:1

##　3. 二分、复杂度、动态数组、哈希表
1. 二分法
   1. 有序数组中找到num
   2. 有序数组中找到>=num最左的位置
   3. 有序数组中找到<=num最右的位置 
   4. 局部最小值问题
      1. 有一个数组，无序。（任意两个相邻数字不相等）
      2. 整体无序，但是可以二分
      3. 局部最小：
         1. [0]<[1] 0
         2. [N-2]>[N-1] N-1
         3. 左<[i]<右 i
2. 时间复杂度