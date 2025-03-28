---
title: onCreateViewHolder
tags: onCreateViewHolder
category: Android
date: 2025-02-17 22:17:07
---

## 记录一次onCreateViewHolder频繁调用的问题

### 场景：

1. 一个父recycler view内有多个子item，每个item有其对应的自定义ViewHolder，而有某两个ViewHolder分别有自己的一个recycler
   view。
2. 把父recycler view命名为rvParent
3. 把这两个ViewHolder命名为vhA和vhB
3. 把这两个recycler view命名为rvA和rvB

### 问题：假设vhA和vhB都加载完毕。每次滑动rvParent滑出再滑入rvA和rvB时，表现不同。

1. rvA流畅
2. rvB总是卡一下

### 定位问题

1. 通过大量的时间戳判断以及bind判断。定位到是rvB每次滑出再滑入时，rvB的adapter总会走很多次onCreateViewHolder与onBindViewHolder

### 额外信息

1. 针对adapter的`notifyItemDataSetChanged`，在本场景中，是通过多种数据更新后再进行needNotify的判断。
2. 使用“开发者选项--Profile GPU Rendering（GPU呈现模式分析）”发现
    1. 每次滑入，都会有大量的“layout/measure”发生，也就是视图重绘
    2. 每次滑入，主线程都会有很多事在做

### 需要知道的知识：每次notifyItemDataSetChanged后

1. **整个列表重新绑定**：
    1. RecyclerView 不会计算哪些项发生了变化，而是所有可见项的 onBindViewHolder() 方法都会被调用，导致数据重新绑定到
       ViewHolder。
       由于 RecyclerView 不会执行增量更新，它不会提供动画效果，而是会直接刷新整个列表。
2. **视图重绘 & UI 性能影响**：
    1. RecyclerView 可能会导致整个列表重新布局和重绘，影响性能，尤其是当列表较长时。
       由于所有 ViewHolder 都会重新绑定数据，会增加 onBindViewHolder() 的调用次数，可能引发不必要的 UI
       刷新。
3. **不会重新创建 ViewHolder（除非被回收）**：
    1. RecyclerView 仍然会尽量复用 ViewHolder，但所有绑定的 ViewHolder 都会重新绑定数据。

### 对比rvA和rvB得出结论：

1. 每次滑入rvA，不需要notifyItemDataSetChanged
2. 每次滑入rvB，都会notifyItemDataSetChanged
   所以可以定位到问题出现在rvB的adapter的update导致的notifyItemDataSetChanged的判断条件上

### 进一步分析代码，发现

1. 从vhB传入rvBadapter的是一个`(position)->Unit?`，每次传入都会变化。
2. vhB的 onBindViewHolder 中每次都会重新赋值
   在 RecyclerView 适配器的 onBindViewHolder 方法中，如果 vhB 传递的回调函数不是稳定的（例如，每次
   onBindViewHolder 时都创建一个新的 Lambda），就会导致 rvBAdapter 内部存储的回调一直变化。