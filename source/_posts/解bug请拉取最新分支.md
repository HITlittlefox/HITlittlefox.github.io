---
title: 解bug请拉取最新分支
tags: DEBUG
category: Android
date: 2025-01-20 22:19:26
---

## 该 BUG 是在某些场景下, 会引发崩溃

1. 所打印出的日志,仅仅提示了所在 activity
2. 已知该 BUG 能否复现,在多个代码版本的表现不同
   1. 老版本没问题
   2. 新版本有问题
   3. 我本地代码没问题

此时就应该敏感的**先确认自己本地代码是否拉取新代码**

但是因为到晚上了注意力下降，并没有从这方面发掘。反复阅读代码仍未发现问题！！！
最终结果：同事在他那里发现是新的提交造成的问题

而我本地代码没有拉取这个提交，自然如何 code review 也找不到原因。

## 还有个，logcat 中的 `getString()` 描述

这个 bug 的描述一开始说是资源丢失。最关键的 `getString()`，我一度认为是在读取文本资源等内容的时候资源索引不到。

但是最终发现，确实是 `getString()` 的格式化的问题。

**在 Kotlin 中使用 getString() 替换占位符：**

```xml
<resources>
    <string name="greeting_message">Hello, %1$s! You have %2$d new messages.</string>
</resources>
```

```kotlin
val name = "John"
val newMessages = 5

// 使用 getString() 和占位符
val greetingMessage = getString(R.string.greeting_message, name, newMessages)

println(greetingMessage)  // 输出：Hello, John! You have 5 new messages.
```

在 getString() 方法中

1. 第一个参数：是资源 ID，表示你要获取的字符串资源的位置（如 R.string.greeting_message）。
2. 后续参数：是你传递给该字符串的替代值，用来替换字符串中的占位符。

## 关于占位符

### 关键点：

- **占位符和参数数量不匹配** 时可能会导致崩溃。
- **占位符的数量和顺序** 与你传入的参数数量必须匹配。

### 详细解释：

```xml
<!-- 两个占位符，第一个是字符串，第二个是整数 -->
<string name="greeting_message">Hello, %1$s! You have completed %2$d%% of the task.</string>
```

```kotlin
    private fun testGetString() {
        // 获取字符串资源，传入两个占位符的值
        val name = "John"
        val percentage = 75

        // 双参数
        println(
            getString(
                R.string.greeting_message, name, percentage
            )
        )

        try {
            // 单参数
            println(
                getString(
                    R.string.greeting_message, name
                )
            )
        } catch (e: Exception) {
            println("单参报错")
        }

        try {
            // 三参数
            println(
                getString(
                    R.string.greeting_message, name, name, name
                )
            )
        } catch (e: Exception) {
            println("三参报错")
        }
    }
```
