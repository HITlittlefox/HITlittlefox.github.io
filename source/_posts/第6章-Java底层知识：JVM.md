---
title: 第6章-Java底层知识：JVM
category: 我要就业
date: 2022-08-29 22:26:51
tags:
---
1. 谈谈你对Java的理解
    1. 平台无关性 -- 一次编译到处运行
    2. GC -- 垃圾回收机制
    3. 语言特性 -- 泛型、反射、lambda表达式
    4. 面向对象 -- 封装、继承、多态
    5. 类库 -- 集合、并发库、网络、IO、NIO
    6. 异常处理
2. 平台无关性如何实现
    1. Compile Once，Run AnyWhere如何实现
        1. 编译时 使用javac指令编译java源码，即将源码编译生成字节码并存入到对应的.class文件中
        2. 运行时 
        3. 答：Java源码首先被编译成字节码，再由不同平台的JVM进行解析，Java语言在不同的平台上运行时不需要进行重新编译，Java虚拟机在执行字节码的时候，把字节码转换成具体平台上的机器指令
        4. ![20220829223104](https://raw.githubusercontent.com/HITlittlefox/pictures/master/images/20220829223104.png)
    2. 为什么JVM不直接将源码解析成机器码去执行
        1. 准备工作：每次执行都需要进行各种检查，如语法校验
        2. 兼容性：也可以将别的语言解析成字节码
    3. 如何查看.class字节码：使用javap -c指令
3. JVM 如何加载class文件
    1. JVM是内存中的虚拟机
    2. Java虚拟机：JVM内存结构模型、GC垃圾回收机制
    3. JVM架构![20220831000936](https://raw.githubusercontent.com/HITlittlefox/pictures/master/images/20220831000936.png)
        1. Class Loader：依据指定格式，加载class文件到内存
        2. Execution Engine：对命令进行解析
        3. Native Interface：融合不同开发语言的原生库为Java所用
        4. Runtime Data Area：JVM内存空间结构模型
    4. 答：JVM通过Class Loader将符合其格式要求的class文件加载到内存里，并通过Execution Engine去解析class文件里边的字节码，并提交给操作系统去执行。
    5. native 方法 : Class.forname
4. 什么是反射
    1. Java反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意方法和属性；这种动态获取信息以及动态调用对象方法的功能称为Java语言的反射机制
    2. getDeclaredMethod:可以获取所有(包括私有方法)自定义的方法，不能获取继承或者实现接口的方法
    3. getMethod:只能获取public方法，但是可以获取继承或接口的方法
    4. getDeclaredField:私有属性
5. 谈谈ClassLoader
    1. 类从编译到执行的过程：
        1. 编译器将Robot.java源文件编译为Robot.class字节码文件
        2. ClassLoader将字节码转换为JVM中的Class对象
        3. JVM利用Class对象实例化为Robot对象
    2. 谈谈什么是ClassLoader
        1. ClassLoader在Java中有着非常重要的作用，它主要工作在Class装载的加载阶段，
        2. 其主要作用是从系统外部获取Class二进制数据流。他是Java的核心组件，
            1. 所有的Class都是由ClassLoader负责通过将Class文件里的二进制数据流装载进系统，
            2. 然后交给Java虚拟机进行连接、初始化等操作。
    3. ClassLoader的种类：
        1. BootStrapClassLoader：C++编写，加载核心库java.*
        2. ExtClassLoader：Java编写，加载扩展库javax.*
        3. AppClassLoader：Java编写，下载程序所在目录
        4. 自定义ClassLoader：Java编写，定制化加载
    4. 自定义ClassLoader的实现
        1. Wali.java
        2. ClassLoaderChecker.java
        3. MyClassLoader.java
6. ClassLoader的双亲委派机制
    1. 当一个类收到了加载请求时，它是不会先自己去尝试加载的，而是委派给父类去完成，比如我现在要 new 一个 Person，这个 Person 是我们自定义的类，如果我们要加载它，就会先委派 App ClassLoader ，只有当父类加载器都反馈自己无法完成这个请求（也就是父类加载器都没有找到加载所需的 Class）时，子类加载器才会自行尝试加载。
    2. 这样做的好处是，加载位于 rt.jar 包中的类时不管是哪个加载器加载，最终都会委托到 BootStrap ClassLoader 进行加载，这样保证了使用不同的类加载器得到的都是同一个结果。
    3. 其实这个也是一个隔离的作用，避免了我们的代码影响了 JDK 的代码，比如我现在自己定义一个 java.lang.String ：
        ```java
        package java.lang;
        public class String {
            public static void main(String[] args) {
                System.out.println();
            }
        }
        // 尝试运行当前类的 main 函数的时候，我们的代码肯定会报错。
        // 这是因为在加载的时候其实是找到了 rt.jar 中的java.lang.String，然而发现这个里面并没有 main 方法。
        ```
    4. ![20220902003347](https://raw.githubusercontent.com/HITlittlefox/pictures/master/images/20220902003347.png)
    5. 为什么要使用双亲委派机制去加载类：
        1. 避免多份同样字节码的加载，内存是相当宝贵的，没有必要保存两份一样的类对象，即Class对象。
7. loadClass和forName的区别
    1. 类的加载方式：
        1. 隐式加载：new
            1. 通过隐式加载则无需调用Class对象的newInstance方法即可获取对象的实例，并且new支持带参数的构造器生成对象实例，而Class对象的newInstance方法则不支持传入参数，需要通过反射调用构造器的newInstance方法才能支持参数。
        2. 显式加载：loadClass，formName等
            1. 显式加载当获取到Class对象之后需要调用Class对象的newInstance方法来生成对象的实例
    2. 类的装载过程：
        1. 加载：通过ClassLoader加载class文件字节码，生成Class对象
        2. 链接：检验：检查加载的class的正确性和安全性，如检查class文件的格式是否正确 准备：为类变量分配存储空间并设置类变量初始值，类变量随类型信息存放在方法区中，生命周期很长。 解析：JVM将常量池内的符号引用转换为支持引用
        3. 初始化：执行类变量赋值和静态代码块
    3. loadClass和forName
        1. 联系： 他们都能够在运行时对任意一个类进行动态加载，都能够知道该类的所有属性和方法，对于任意一个对象都能够调用它的任意方法和属性。
        2. 区别： 
            1. Class.forName得到的class是已经初始化完成的，即已经完成装载的整个过程 
            2. ClassLoader.loadClass得到的class是还没有链接的，即只完成装载的第一步
    4. 区别产生的作用： 
        1. 例如程序中需要使用MySQL需要加载driver，这里只能使用forName，而不能使用loadClass
    5. 有了forName装载类，为什么还要使用loadClass呢？ 
        1. 在Spring IOC中，在资源加载器获取要读入的资源的时候，即读取Bean的配置文件的时候，如果是以ClassPath的方式来加载就需要使用ClassLoader.loadClass来加载。
        2. 这是因为SpringIOC使用了lazy loading延迟加载，Spring ICO为了加快初始化速度因此大量使用了延迟加载技术，而使用ClassLoader不需要执行类中的初始化代码和链接步骤，从而加快了加载速度，把类的初始化工作留到实际使用到这个类的时候再做。
8. Java内存模型之线程独占部分-1
    1. 内存简介：  
        1. 32位处理器：2^32的可寻址范围 
        2. 64位处理器：2^64位可寻址范围
    2. 地址空间划分： 
        1. 内核空间：内核是主要操作系统程序和运行时空间，包含用于连接计算机调度程序以及提供联网，虚拟内存等服务的逻辑和进程 
        2. 用户空间：Java进程实际运行时的内存空间
    3. 你了解Java的内存模型么
        1. JVM内存模型-JDK8  
            1. 线程私有：程序计数器、虚拟机栈、本地方法栈 
            2. 线程共享：MetaSpace、Java堆
        2. 程序计数器（Program Counter Register）
            1. 当前线程所执行的字节码行号指示器（逻辑）
            2. 改变计数器的值来选取下一条需要执行的字节码指令，包括分支、循环、跳转、异常处理、线程恢复等基础功能
            3. 和线程是一对一的关系，即“线程私有”
            4. 对Java方法技术，如果是Native方法则计数器值为Undefined
            5. 不会发生内存泄漏
            6. 程序计数器是逻辑计数器，而非物理计数器；为了线程切换后都能恢复正确的执行位置，每个线程都有一个独立的程序计数器，是线程独立的，只对Java方法计数，对Native方法则为Undefined，不会发生内存泄漏。
    4. Java虚拟机栈（Stack）
        1. Java方法执行的内存模型
        2. 包含多个栈帧，方法运行期间的基础数据结构，用于存储局部变量表、操作栈、动态链接、返回地址等。
    5. 局部变量表和操作数栈
        1. 局部变量表：包含方法执行过程中的所有变量
        2. 操作数栈：入栈、出栈、复制、交换、产生消费变量



9.  Java内存模型之线程独占部分-2
    1. 递归为什么会引发java.lang.StackOverflowError异常？
        1. 递归过深，栈帧数超过虚拟机栈深度。限制递归次数，使用循环替代。
    2. 虚拟机栈过多会引发java.lang.OutOfMemoryError异常
        ```java
        public static void stackLeakByThread() {
            while (true) {
                new Thread() {
                    public void run() {
                        while (true) {
                        }
                    }
                }.start();
            }
        }
        ```
    3. 虚拟机栈也是Java虚拟机自动管理的，栈类似于一个集合，但是有固定的容量，是由多个栈帧合起来的。
    4. 每调用一个方法Java虚拟机就会在内存中分配对应的一块空间，这块空间也就是一块栈帧，当方法调用结束后，对应的栈帧就会被自动释放掉。
    5. 栈的内存不需要通过GC去回收，而会自动释放。
    6. 本地方法栈：与虚拟机栈相似，主要作用于标注了native的方法。
10. Java内存模型之线程共享部分
    1. 元空间(MetaSpace)和永久代(PermGen)的区别：
        1. 元空间使用本地内存，而永久代使用的是jvm的内存
    2. MetaSpace相比PermGen的优势：
        1. 字符串常量池存在于永久代中，容易出现性能问题和内存溢出
        2. 类和方法的信息大小难以确定，给永久代的大小指定带来困难
        3. 永久代会为GC带来不必要的复杂性，并且回收效率低
        4. 方便HotSpot与其他JVM如Jrockit的集成
    3. Java堆（Heap）：
        1. 对象实例的分配区域
        2. GC管理的主要区域-新生代、老年代
11. Java内存模型之常考题解析-1
    1. JVM三大性能调优参数-Xms、-Xmx、-Xss的含义： java -Xms128m -Xmx128m -Xss256k -jar xxx.jar
        1. Xss：规定了每个线程虚拟机栈（堆栈）的大小，256k足够。影响并发线程数的大小。
        2. Xms：堆的初始值，
        3. Xmx：堆能扩展达到的最大值，
        4. 一般讲Xms和Xmx设置成一样的，因为当Heap不够用发生扩容时会发生内存抖动，从而影响程序运行的稳定性。
    2. Java内存模型中堆和栈的区别-内存分配策略
        1. 静态存储：编译时确定每个数据目标在运行时的存储空间需求，不允许有可变数据结构、嵌套、递归存在
        2. 栈式存储：数据区需求在编译时未知，运行时模块入口前确定
        3. 堆式存储：编译时或运行时模块入口都无法确定，动态分配
    3. Java内存模型中堆和栈的区别： 
        1. 联系：引用对象、数组时，栈里定义变量保存堆中目标的首地址 
        2. 区别：
            1. 管理方式：栈自动释放，堆需要GC 
            2. 空间大小：栈比堆小 
            3. 碎片相关：栈产生的碎片远小于堆 
            4. 分配方式：栈支持动态和静态分配，而堆只支持动态分配 
            5. 效率：栈的效率比堆高
    4. ![20220903012836](https://raw.githubusercontent.com/HITlittlefox/pictures/master/images/20220903012836.png)
    5. 元空间、堆、线程独占部分间的联系-内存角度
    6. 不同JDK版本之间的intern()方法的区别
        1. JDK6使用intern()向字符串常量池添加的是字符串的副本；
        2. 而JDK7+添加的是字符串的引用
12. Java内存模型之常考题解析-2
    1. ![20220903013252](https://raw.githubusercontent.com/HITlittlefox/pictures/master/images/20220903013252.png)
13. 彩蛋之找工作的最佳时期
