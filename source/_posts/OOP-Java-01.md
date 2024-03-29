---
title: OOP-Java-01
category: Java
date: 2021-10-26 16:11:51
tags:
---

### Java语言的特点
1. 简单易学。
2. 面向对象。是一种以对象为中心，以消息为驱动的面向对象的编程语言。面向对象的三大特点：**封装、继承和多态**。
3. 平台无关性。Java程序不需要修改可以在不同的软硬件平台上支行。平台无关分为源代码级（需重新编译源代码，如C/C++）和目标代码级(Java)。
4. 分布式。数据分布是指数据可以分散在网络的不同主机上；操作分布指把一个计算分散在不同的主机上处理。
5. 可靠性。Java解释器运行时实施检查，可发现数组和字符串访问的越界；提供了异常处理机制；数据类型需显式说明；不支持指针，避免了对内存的非法访问；自动内存回收防止内存丢失等动态内存分配导致的问题。
6. 安全性。
7. 支持多线程。线程是比进程更小的可并发执行的单位。C++没有内置的多线程机制，需调用操作系统的多线程功能来进行多线程序设计。Java提供了多线程支持。
8. 支持网络编程。Java的小程序（Applet）是动态、安全、跨平台的网络应用程序。
9. 编译和解释并存。由编译器将Java源程序编译成字节码文件，然后再由Java运行系统解释执行字节码文件（解释器将字节码再翻译成二进制码运行） 。

### Java程序的运行过程：先编译，后解释
![Java程序的运行过程](https://pic.imgdb.cn/item/617c1aaa2ab3f51d917b116e.jpg)

*Java应用程序与Java小程序的区别：*
>小程序和应用程序之间的技术差别在于运行环境。
>由于小程序和应用程序的执行环境不同，它们的最低要求也不同。在应用方面，WWW使小程序的发布十分便利，因此小程序更适合在Internet上使用；相反，非网络系统和内存较小的系统更适合使用Java应用程序。
>Java 小程序可以直接利用浏览器或appletviewer 提供的图形用户界面，而Java应用程序则必须另外书写专用代码来营建自己的图形界面。
>小程序的主类（程序执行的入口点）必须是一个继承自系统类Applet的子类，且该类必须是public类。

```java
package ch01;          //定义该程序属于ch01包
import java.io.*;      //导入java.io类库中的所有类
public class App1_1{    //定义类：App1_1
  public static void main(String[] args) {
    char c= ' ';
    System.out.print("请输入一个字符：");
    try{
          c=(char)System.in.read();
     }catch(IOException s){  }
    System.out.println("您输入的字符是："+c);
  }
} 
```