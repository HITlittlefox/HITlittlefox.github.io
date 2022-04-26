---
title: OOP-Java-08plus
category: Java
date: 2021-10-17 17:02:36
tags:
---
### java基础类库
0. 介绍
   1. Java提供了用于语言开发的类库，称为**Java基础类库**(**JFC**，Java Foundational Class) ，也称**应用程序编程接口**(**API**，Application Programming Interface)，分别放在不同的包中。
   2. Java提供的包主要有：
       >java.lang，java.io，java.math，java.util
       >java.applet，java.awt，java.awt.event，java.awt.image
       >java.net，java.rmi，java.sql，java.text
       >javax.swing等
   3. 语言包(java.lang)：语言包java.lang提供了Java语言最基础的类
      1. Object类
      2. 基本数据类型包裹类(the Data Type Wrapper)
      3. 字符串类(String、StringBuffer，StringBuilder)
      4. 数学类(Math)
      5. 系统和运行时类(System、Runtime)
      6. 类操作类(Class，ClassLoader)
      7. 错误和异常处理类（Throwable,Exception,Error）
      8. 线程类（Thread）、进程类（Process）

#### 语言包(java.lang)

1. 基本数据类型包裹类(the Data Type Wrapper)
    1. 对应Java的每一个**基本数据类型**(primitive data type)都有一个数据包裹类。
    2. Java 的包装类有两个主要的目的：
        1. Java包装类将基本数据类型的值“包装”到对象中，对基本数据类型的操作**变为了对对象进行操作**
        2. 更加方便**类型的转换**
    3. ![基本数据类型及其数据包裹类](https://pic.imgdb.cn/item/616be81c2ab3f51d9198fe13.jpg)
    4. 生成数据类型包裹类对象的方法：
        1. 从基本数据类型的变量或常量生成包裹类对象
            ```java
            double x = 1.2;
            Double a = new Double(x);
            Double b = new Double(-5.25); 
            ```
        1. 从字符串生成包裹类对象：
            <!-- todo:发生了什么，为什么要用double处理"-2.34" -->
            ```java
            Double c = new Double("-2.34");
            Integer i = new Integer("1234"); 
            ``` 
        1. 已知字符串，可使用valueOf方法将其转换成包裹类对象：
            ```java
            Integer.valueOf("125");
            Double.valueOf("5.15");
            ```
    5. 得到基本数据类型数据的方法：
        1. 每一个包裹类都提供相应的方法将包裹类对象转换回基本数据类型的数据：
            ```java
            anIntegerObject.intValue()   // 返回 int类
            aCharacterObject.charValue() // 返回 char类型的数据
            ```
    6. 字符串转化为数值类型：
        1. Integer、Float、Double、Long、Byte 及Short 类提供了特殊的方法能够**将字符串类型的对象直接转换成对应的int、float、double、long、byte或short类型数据**：
            ```java
            Integer.parseInt("234") // 返回int类型数据
            Float.parseFloat("234.78")  // 返回float类型数据
            ```
    7. 自动装箱、拆箱：
       1. Java SE5之后提供了自动装箱和拆箱机制。基本数据类型可以和与其对应的包装类之间自动进行转换；
            ```java
            Integer i = 10; 
            int index = i;
            ```
       2. **装箱**就是**自动将基本数据类型转换为包装器类型**，通过自动调用Integer的`valueOf(int)`方法实现；
       3. **拆箱**就是**自动将包装器类型装换为基本数据类型**，通过自动调用Integer的`intValue`方法实现。
 
2. 字符串类(String、StringBuffer，StringBuilder)
   1. 常量字符串类String:该类字符串对象的值和长度都不变化，称为常量字符串
      1. 生成String类对象的方法：
         1. 可以这样生成一个常量字符串：
             ```java
             String aString;
             aString = "This is a string" ;
             ```
         2. 调用构造方法生成字符串对象：
             ```java
             new String();           
             new String(String value); 
             new String(char[] value); 
             new String(char[] value, int offset, int count); 
             new String(StringBuffer buffer);
             ```
      2. String类常用方法
         1. ![String类常用方法](https://pic.imgdb.cn/item/616c0ae02ab3f51d91b61883.jpg)
   2. 变量字符串类StringBuffer：
      1. 其对象是可以修改的字符串
         1. 字符的个数称为对象的长度(length)；
         2. 分配的存储空间称为对象的容量(capacity)；
      2. 与String类的对象相比，执行效率要低一些。
      3. 该类的方法不能被用于String类的对象
      4. 生成StringBuffer类的对象：
         ```java
         1. new StringBuffer(); //生成容量为16的空字符串对象
         2. new StringBuffer(int size); //生成容量为size的空字符串对象
         3. new StringBuffer(String aString); //生成aString的一个备份，容量为其长度 +16
         ```
      5. ![StringBuffer类常用方法](https://pic.imgdb.cn/item/616c1ac92ab3f51d91c60b5c.jpg)
      6. >例:已知一个字符串，返回将字符串中的非字母字符都删除后的字符串

   3. 变量字符串类StringBuilder
      1. StringBuilder 类在 Java SE5中被提出，方法与StringBuffer 类似；
      2. **StringBuilder与StringBuffer区别**
         1. 两者最大的不同在于 StringBuilder 的方法不是线程安全的（不能同步访问）。
         2. StringBuilder 有速度优势，所以多数情况下建议使用 StringBuilder 类。
         3. 在应用程序要求线程安全的情况下，必须使用 StringBuffer 类。
      3. String、StringBuffer、StringBuilder适用场合：
         1. 在字符串不经常发生变化的业务场景优先使用String(代码更清晰简洁)。如常量的声明，少量的字符串操作(拼接，删除等)；
         2. 在单线程情况下，如有大量的字符串操作情况，应该使用StringBuilder来操作字符串。不能使用String的“+”来拼接而是使用StringBuilder 的append()方法，避免产生大量无用的中间对象，耗费空间且执行效率低下（新建对象、回收对象花费大量时间），如JSON的封装等；
         3. 在多线程情况下，如有大量的字符串操作情况，应该使用StringBuffer，如HTTP参数解析和封装等。

3. 数学类(Math)
   1. 提供一组常量和数学函数，例如
      1. E和PI常数；
      2. 求绝对值的abs方法；
      3. 计算三角函数的sin方法和cos方法；
      4. 求最小值、最大值的min方法和max方法；
      5. 求随机数的random方法等；
   2. 其中所有的变量和方法都是静态的(static)；
   3. 是终结类(final)，不能从中派生其他的新类。
4. 系统类System
   1. 访问系统资源:
      1. arraycopy() //复制一个数组
      2. exit() //结束当前运行的程序
      3. currentTimeMillis() //获得系统当前日期和时间等
   2. 访问标准输入输出流:
      1. System.in       //标准输入，表示键盘
      2. System.out     //标准输出，表示显示器
      3. System.err     //错误输出，表示显示器
      4. ![System主要方法](https://pic.imgdb.cn/item/616c1da42ab3f51d91c8b9bd.jpg)
      5. >例:记录程序执行的时间。
      6. >例:访问JVM的环境属性。
5. 运行时类Runtime
   1. Runtime类封装了运行时环境；
   2. 用户一般不实例化一个Runtime对象。但是可以通过调用静态方法Runtime.getRuntime( )而获得对当前Runtime对象的引用；
   3. 一旦获得了对当前对象的引用，就可以调用几个控制Java虚拟机的状态和行为的方法。 
   4. ![Runtime 常用的方法](https://pic.imgdb.cn/item/616c1e1d2ab3f51d91c92a48.jpg)
   5. >例:使用Runtime执行其他程序。
6. 类操作类Class、ClassLoader
   1. Class类
      1. 提供运行时信息，如名字、类型以及父类；
      2. Object类中的getClass方法返回当前对象所在的类，返回类型是Class；
      3. 它的getName方法返回一个类的名称，返回值是String；
      4. 它的getSuperclass方法可以获得当前对象的父类。
   2. ClassLoader类
      1. 提供把类装入运行时环境的方法
      2. >例:Class类应用举例。

#### 工具包(java.util)
0. 介绍
   1. 数据输入类Scanner
   2. 日期类：描述日期和时间
      1. Date
      2. Calendar
      3. GregorianCalendar
   3. 伪随机数发生器类Random
   4. StringTokenizer类
      1. 允许以某种分隔标准将字符串分隔成单独的子字符串
   5. 集合类
      1. Collection(无序集合)、Set(不重复集合)
      2. List (有序不重复集合) 、Enumeration (枚举)
      3. LinkedList (链表) 、Vector (向量)
      4. Stack (栈) 、Hashtable (哈希表) 、TreeSet (树)

1. Date类
   1. 构造方法
      1. `Date()`    获得系统当前日期和时间值；
      2. `Date(long date)`  以date创建日期对象，date表示从GMT（格林威治）时间1970-1-1 00:00:00开始至某时刻的毫秒数。
      3. ![Date类常用方法](https://pic.imgdb.cn/item/616c20482ab3f51d91cb90f0.jpg)
      4. >例5-6:Date的例子。
2. Calendar类
   1. 一个抽象的基础类，支持将Date对象转换成一系列单个的日期整型数据集，如YEAR、MONTH、DAY、HOUR等常量；
   2. 它派生的GregorianCalendar类实现标准的Gregorian日历；
   3. 由于Calendar是抽象类，不能用new方法生成Calendar的实例对象，可以使用getInstance()方法创建一个GregorianCalendar类的对象。
   4. Calendar类中声明的常量：很多...
   5. ![Calendar类中的主要方法](https://pic.imgdb.cn/item/616c20dd2ab3f51d91cc5158.jpg)
3. GregorianCalendar类
   1. 是Calendar的子类;
   2. 用于查询及操作日期;
   3. GregorianCalendar定义了两个域：AD(公元）和BC（公元前）。它们代表由公历定义的两个纪元。
   4. GregorianCalendar的构造函数:
         ```java
         GregorianCalendar(int year, int month, int date)
         GregorianCalendar(int year, int month, int date, int hours,int minutes)
         GregorianCalendar(int year, int month, int date, int hours,int minutes, int seconds)
         // 三种形式中，都设置了日，月和年。这里，year指定了从1900年起的年数。month指定了月，以0表示一月。月中的日由date指定，从1开始。第一种形式以午夜设置时间。第二种形式以小时和分钟设置时间，第三种形式增加了秒。
         ```
   5. getTime()方法    返回Date对象，显示日历
         ```java
         System.out.println(new GregorianCalendar().getTime());        
         System.out.println(new GregorianCalendar(1999, 11, 31).getTime());    
         System.out.println(new GregorianCalendar(1968, 0, 8, 11, 55).getTime()); 
         ```
   6. >例:日历的使用。
4. Random类
   1. Random类模拟了一个伪随机数发生器，产生的伪随机数服从均匀分布，可以使用系统时间或给出一个长整型数作为“种子”构造出Random对象，然后使用对象的方法获得一个个随机数。
   2. 构造方法和常用方法见表8.8和8.9。
5. StringTokenizer类
   1. 允许以某种分隔标准将字符串分隔成单独的子字符串，如可以将单词从语句中分离出来；
   2. 术语分隔符（delimeter）是指用于分隔单词（也称为标记，tokens）的字符。
   3. 常用方法：
        ```java
        int countTokens()  //返回单词的个数
        String nextToken()   //返回下一个单词
        boolean hasMoreTokens() //是否还有单词
        ```
   4. 生成StringTokenizer类对象的三种方法：
      1. `new StringTokenizer(String aString);`指定了将被处理的字符串，没有指定分隔符(delimeter)，这种情况下**默认的分隔符为空格**;
      2. `new StringTokenizer(String aString, String delimiters);` 除了指定将被处理的字符串，还指定了分隔符字符串，如分隔符字符串可以为“,:;|_()”
      3. `new StringTokenizer(String  aString, String  delimiters, boolean  returnDelimiters);`第三个参数如果为true，则分隔符本身也作为标记返回
      4. >例:字符串分割类的使用。
      <!-- TODO: 4. >例:字符串分割类的使用。 -->
      

#### 对象数组(java.util)
0. 介绍
   1. 数组元素是类的对象；
   2. 所有元素具有相同的类型；
   3. 每个元素都是一个对象的引用。
1. 数组初始化
   1. 静态初始化：在声明和定义数组的同时对数组元素进行初始化，例如：
        ```java
        BankAccount[] accounts = { 
        new BankAccount("Zhang", 100.00), 
        new BankAccount("Li", 2380.00),
        new BankAccount("Wang", 500.00),
        new BankAccount("Liu", 175.56),
        new BankAccount("Ma", 924.02)};
        ```
   2. 动态初始化：使用运算符new，需要经过两步：
        ```java
        //首先给数组分配空间
        BankAccount accounts[ ]=new BankAccount[5];
        //然后给每一个数组元素分配空间
        accounts[0]=new BankAccount("Zhang", 100.00);
        //…
        accounts[4]=new BankAccount ("Ma", 924.02);
        ```
2. 数组存储对象
   <!-- 1. TODO: 数组、信息、成绩、查找、增加、删除 -->
   1. >例:使用数组存储一个班的学生信息及考试成绩。学生信息包括学号、姓名、三门课（英语、数学、计算机）的成绩及总成绩。
3. 数组元素的查找
   1. 思想:对所存储的数据从第一项开始（也可以从最后一项开始），依次与所要查找的数据进行比较，直到找到该数据或将全部元素都找完还没有找到该数据为止。
   2. 已知学生的学号，查找此学生是否存在。如果存在，返回其在数组中的下标位置；如果不存在，返回-1.
   3. >例：为班级类添加查找方法。
4. 数组元素的增加
   1. 在数组的末尾增加一个学生对象：
      1. 增加之前需先判断数组中是否还有空间，并且在数组中查找将要增加的学号是否已经存在；
      2. 增加成功，返回true；否则，返回false。    
      3. >例：为班级类添加增加方法。
5. 数组元素的删除
   1. >例：为班级类编写删除方法
6. 对数组元素进行排序
   1. 常用的排序算法有：
      1. 选择排序
         1. **先在未排序序列中选一个最大元素，作为已排序子序列；**
         2. **然后再重复地从未排序子序列中选取一个最大元素，把它加到已经排序的序列中，作为已排序子序列的最后一个元素；**
         3. **直到把未排序子序列中的元素处理完为止。**
         4. 工作原理：首先在未排序序列中找到最小（大）元素，存放到排序序列的起始位置，然后，再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。以此类推，直到所有元素均排序完毕。
         5. >升序排列 https://segmentfault.com/a/1190000023910314
            ```java
            package test;

            import java.util.Arrays;

            //选择排序
            public class test8 {

               //选择排序
               public static void selectSort(int[] arr) {
                  //遍历所有的数
                  for (int i = 0; i < arr.length; i++) {
                        int min = i;
                        //把当前遍历的数和后面所有的数依次进行比较，并记录下最小的数的下标
                        for (int j = i + 1; j < arr.length; j++) {
                           //如果后面比较的数比记录的最小的数小
                           if (arr[j] < arr[min]) {
                              //记录最小的那个数的下标
                              min = j;
                           }
                        }
                        //如果最小的数和当前遍历数的下标不一致，说明下标为min的数比当前遍历的数更小
                        if (i != min) {
                           int temp = arr[i];
                           arr[i] = arr[min];
                           arr[min] = temp;
                        }
                  }
               }

               public static void main(String[] args) {
                  int[] arr = new int[]{5, 8, 6, 3, 9, 2, 1, 7};
                  selectSort(arr);
                  System.out.println(Arrays.toString(arr));
               }

            }
            ```
      2. 插入排序
         1. 将待排序的数据按一定的规则逐一插入到已排序序列中的合适位置处，直到将全部数据都插入为止。
         2. 插入的规则不同，便形成了不同的插入排序方法。其中，算法最简单的为**直接插入排序方法**
         3. **直接插入排序方法先以未排序序列的第一个元素作为已排序子序列，然后从原来的第二个元素起，将各元素逐一插入到已排序子序列中合适的位置，直到把全部元素都插入为止。**
         4. ![直接插入排序的步骤](https://pic.imgdb.cn/item/616c281e2ab3f51d91d5bc26.jpg)
         5. >插入排序 http://data.biancheng.net/view/118.html
            ```java
            package test;

            import java.util.Arrays;

            public class test9 {
               //    public class InsertSort {
               public static void insertSort(int[] a) {
                  int i, j, insertNote;// 要插入的数据
                  for (i = 1; i < a.length; i++) {// 从数组的第二个元素开始循环将数组中的元素插入
                        insertNote = a[i];// 设置数组中的第2个元素为第一次循环要插入的数据

                        // 移动"比insertNote大"的元素
                        j = i - 1;
                        while (j >= 0 && insertNote < a[j]) {
                           a[j + 1] = a[j];// 如果要插入的元素小于第j个元素,就将第j个元素向后移动
                           j--;
                        }

                        // 安放"insertNote"元素
                        a[j + 1] = insertNote;// 直到要插入的元素不小于第j个元素,将insertNote插入到数组中
                  }
               }

               public static void main(String[] args) {
                  int[] a = {38, 65, 97, 76, 13, 27, 49};
                  insertSort(a);
                  System.out.println(Arrays.toString(a));
               }
            //    }
            }
            ```
   2. >以降序为例进行介绍

7. 在已排序的数组元素中查找
   1. 一批Integer类型的数据已按升序排列好，a1＜a2＜…＜an ，存储在数组a[0]、a[1]、 …、a[n-1]中，现在要对该数组进行查找，看给定的数据x是否在此数组中。
   2. 方法举例：
      1. 顺序查找：按从左向右的顺序查找，当x小于a[i]时就应该停止查找：
            ```java
            public int seqSearch(int x){
                for (int i = 0; (i < n) && (x >= a[i].intValue()); i++)
                    if (a[i].intValue() == x) return i;
                return -1;
            } 
            ```
      2. 二分法查找：在0到n-1中间选一个正整数k，用k把原来的有序序列分为三个有序子序列
            >a[0]，a[1]，…，a[k-1]  
            >a[k]  
            >a[k+1]，a[k+2]，…，a[n-1]   
      3. >二分法举例 
         ```java
         package test;

         //在已排序的数组元素中查找：>二分法举例
         public class test7 {
            static int[] rep = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};

            //二分法
            //在给定的数组范围内查找某一元素，
            //方法重载 overload
            private static int search(int i, int lower, int upper) {
               int index = lower;
               // 里面是个递归(中间值然后左右递归)(参数1是你要找的数,参数2是起始位置,参数3是末尾位置,rep是个int数组)
               if (upper >= lower) {
                     int middle = (upper + lower) / 2;
                     //取出数组中间的那个元素
                     int current = rep[middle];

                     //把insert的数字与已有的数组中最中间的那个数进行比较
                     //如果相同，就返回中间这个数的下标
                     if (current == i) {
                        index = middle;
                     } else if (current < i) { //如果insert的数字大于中间数字，就再来一遍，把insert的数 和 数组中大于中间数字的数的中间数进行比较！
                        index = search(i, middle + 1, upper);
                     } else { //如果insert的数字小于中间数字，也再来一遍，把insert的数 和 数组中小于中间数字的数的中间数进行比较！
                        index = search(i, lower, middle - 1);
                     }
               }
               return index;
            }

            public static void main(String[] args) {

               int searchNumber = 9;
               System.out.println("the number \"" + searchNumber + "\" appears in the location of " + search(searchNumber, 1, 9));
            }
         }

         ```
   3. 具有排序数组的类SortedIntArray
      1. **search方法运用二分查找算法：****在给定的数组范围内查找某一元素，如果存在，返回元素所在的下标位置，如果不存在，则返回元素应该在的位置（如果要将此元素插入到数组中，且保持数组仍然有序的位置）**
      2. **将此功能与插入功能相结合，实现对数组元素进行排序。**
