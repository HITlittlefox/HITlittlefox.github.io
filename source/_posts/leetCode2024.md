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

一、定长滑动窗口

1. 定长滑窗套路：总结成三步：**入-更新-出**
    1. 入：下标为 i 的元素进入窗口，更新相关统计量。如果 i<k−1 则重复第一步。
    2. 更新：更新答案。一般是更新最大值/最小值。
    3. 出：下标为 i−k+1 的元素离开窗口，更新相关统计量。
2. 
