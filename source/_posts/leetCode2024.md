---
title: leetCode2024
tags: leetCode
category: Backend
date: 2024-09-08 23:25:18
---

# 链接集合

1. [分享｜如何科学刷题？](https://leetcode.cn/circle/discuss/RvFUtj/)
    1. [X]  [「新」动计划 · 编程入门](https://leetcode.cn/studyplan/primers-list/)
    2. [ ]  [编程基础 0 到 1](https://leetcode.cn/studyplan/programming-skills/)

## [分享丨【题单】滑动窗口与双指针（定长/不定长/单序列/双序列/三指针）](https://leetcode.cn/circle/discuss/0viNMK/)

### 一、定长滑动窗口

1. 定长滑窗套路：总结成三步：**入-更新-出**
    1. 入：下标为 i 的元素进入窗口，更新相关统计量。如果 i<k−1 则重复第一步。
    2. 更新：更新答案。一般是更新最大值/最小值。
    3. 出：下标为 i−k+1 的元素离开窗口，更新相关统计量。
2. 可以使用IDEA leetCode插件，可以直接获取list
    1. https://leetcode.cn/problem-list/IXxZMHkv/

### 二、二分查找 红蓝染色法

1. 保证闭区间 [L,R] 内的颜色都是不确定的，且 L-1 和 R+1 的颜色是确定的
2. 循环不变量
    1. L-1 始终是红色
    2. R+1 始终是蓝色
    3. R+1 是我们找的答案，循环结束时，R+1=L
3. 防止溢出: mid = left + (right-left)/2

####                    

### 解题思路：二分查找low_bound 【时间复杂度O(lgn),n是数组长度】

- 核心要素
- 注意区间开闭，三种都可以
- 循环结束条件：当前区间内没有元素
- 下一次二分查找区间：不能再查找(区间不包含)mid，防止死循环
- 返回值：大于等于target的第一个下标（注意循环不变量）

- 有序数组中二分查找的四种类型（下面的转换仅适用于数组中都是整数）

1. 第一个大于等于x的下标： low_bound(x)
2. 第一个大于x的下标：可以转换为`第一个大于等于 x+1 的下标` ，low_bound(x+1)
3. 最后一个一个小于x的下标：可以转换为`第一个大于等于 x 的下标` 的`左边位置`, low_bound(x) - 1;
4. 最后一个小于等于x的下标：可以转换为`第一个大于等于 x+1 的下标` 的 `左边位置`, low_bound(x+1) - 1;

### [“红蓝染色法”关键：](https://www.bilibili.com/video/BV1AP41137w7/?spm_id_from=333.788&vd_source=81e0efefbe43fe7e2e9028448296460d)

1. right 左移使右侧变蓝 (判断条件为 true )
2. left 右移使左侧变红 (判断条件为 false )
3. 故确定二分处 ( mid ) 的染色条件是关键

### [可以用二分的原因有两个：1.相邻元素不等；2.一个数组必定有峰（有序）](https://www.bilibili.com/video/BV1QK411d76w/?spm_id_from=pageDriver&vd_source=81e0efefbe43fe7e2e9028448296460d)

