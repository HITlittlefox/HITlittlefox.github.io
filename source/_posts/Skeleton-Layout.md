---
title: Skeleton Layout
tags: Skeleton Layout
category: Android
date: 2025-01-17 23:34:23
---

## Skeleton Layout

· 最近研究了recyclerView与viewPager2同步滑动
· 最近研究了使用骨架屏优化加载

涉及链接:

1. https://github.com/Faltenreich/SkeletonLayout
2. https://github.com/bumptech/glide

### 提取核心问题：

1. 如何使用 recyclerView 展示A内容，并在滑动A内容的时候，同步切换放在 viewPager2 的B内容
    1. 确认二者信息可以通过某种关系映射
    2. 使用 RecyclerView.OnScrollListener 来监听 RecyclerView 的滚动
    3. 根据 RecyclerView 的滚动位置，设置 ViewPager2 显示相应的页面
2. recyclerView 如何搭配 SkeletonLayout 使用
    1. adapter 中，初始数据如果为 `map.isEmpty() == true` ,建议配置一个虚假 key to null
    2. 这样的话，能默认骨架屏loading一个空的单个的内容
    3. adapter 的 current item 的值如果非空，则进入 `Glide` 逻辑
3. 如何避免 adapter 疯狂声明初始化
    1. **注意**，当 `adapter == null`，才有必要配置 adapter
    2. 假的解决方案：这种解决方案的map放在adapter局部变量，仍然有时会导致复用错误数据 ~~如果是多个嵌套
       recyclerView，可以通过配置一个 adapterMap 的形式，减少adapter过量加载~~，
    3. 真实解决方案：删除adapter的局部变量（除了入参），在bind内获取已有的recycler
       view的adapter（也就是说，如果非null，直接cast出来）
    4. **注意**，请一定要为 adapter update 内容，不能通过判断空列表，就不更新（否则会导致骨架屏没地方更新）
    5. **注意**，减少闪烁：adapter 里的 update 函数，建议进行 `equalTo()` 内容比较。只有在更新内容时才
       `notifyDataSetChanged`，
        1. 这里还需要注意的是，如果采用的kotlin的`?.`写法，比如
           ~~`bean?.equalTo(inputBean) == false`~~
           ，当
           `bean==null`的时候，不会进代码块。所以正确写法为：
           `bean == null || bean?.equalTo(inputBean) == false`
4. **数据存储应放在单例中** 可以减少频繁请求
    1. 注意，在获取到url时就可以进行判断并从单例中读取已有数据，无需等到发送请求时
    2. 注意，请求失败等异常情况，需要把url对应的是否已请求状态改为false
    3. 建议增加map `<url, 是否已请求>`
    4. 建议增加map `<url, url对应详情>`
5. viewPager2 如何搭配 SkeletonLayout 使用
    1. 类似 2.
6. 在使用 Glide 加载在线图片链接时，成功后才停止骨架屏

```kotlin
// 默认显示骨架屏
skeletonLayout.showSkeleton() // 隐藏 Skeleton
// 假设这是要加载的图片 URL
val imageUrl = "https://example.com/image.jpg"

// 使用 Glide 加载图片
Glide.with(this).load(imageUrl).placeholder(R.drawable.placeholder) // 可选的占位图
    .listener(object : RequestListener<Drawable> {
        override fun onLoadFailed(
            e: GlideException?, model: Any?, target: Target<Drawable>?, isFirstResource: Boolean
        ): Boolean {
            // 图片加载失败时，Skeleton 动画可以保持显示或做其他处理
            return false // 返回 false，允许 Glide 执行默认的错误处理逻辑
        }

        override fun onResourceReady(
            resource: Drawable?,
            model: Any?,
            target: Target<Drawable>?,
            dataSource: DataSource?,
            isFirstResource: Boolean
        ): Boolean {
            // 图片加载成功后，隐藏 Skeleton 动画
            skeletonLayout.showOriginal() // 隐藏 Skeleton
            return false // 返回 false，允许 Glide 执行默认的资源显示逻辑
        }
    }).into(imageView) // 这里是最终加载的目标 ImageView
}
```