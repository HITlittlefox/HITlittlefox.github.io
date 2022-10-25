---
title: OOP-Java-09
category: Java
date: 2021-10-15 18:02:10
tags:
---
### 异常处理

#### 异常处理的基本概念
0. 基本概念
   1. 异常（exception） ：**在程序运行中由代码产生的一种错误**。
   2. 在不支持异常处理的程序设计语言中，每一个运行错误必须由程序员手动控制。
   3. Java语言：异常处理机制，将程序运行时的管理带到面向对象的世界。
1. 错误与异常
   1. 按照*错误的性质*分类：
      1. **语法错(编译时发现，编译错)**：**是由于违反Javau的语法规则而产生的错误，当没有编译错误，才可生成字节码。**
      2. **语义错(运行时发现，运行错)**：**程序在语法上正确，但在语义上存在错误。**如输入数据格式错、除数为0错、给变量赋值超出其允许范围等，这类错误只能在运行时发现，有的还需进行异常处理。
      3. **逻辑错**：**程序编译通过，也可运行，但运行结果与预期不符。**如由于循环条件不正确而没有结果，循环次数不对等因素导致的计算结果不正确等。
   2. 根据*错误严重程度*的不同将运行错分类：
      1. **错误**：**是指程序在执行过程中所遇到的硬件或操作系统的错误，是致命的，需外界干预。**如：内存溢出、虚拟机错等。
      2. **异常**：**是指在硬件和操作系统正常时，程序遇到的运行错。**如数组越界、除数为0、操作数超出数据范围等，异常不是致命的，但会导致程序非正常终止，异常处理机制使程序自身能够捕获和处理异常。
2. Java异常处理机制
   1. **异常（类）**：是指程序在运行过程中发生由于算法考虑不周或软件设计错误等导致的程序异常事件。
   2. **抛出异常**：**产生一个代表该异常的对象，并把它提交给运行系统的过程**（异常对象可由应用程序本身产生，也可能由JVM产生）。
   3. **捕获异常**：**异常抛出后，运行系统从生成异常对象的代码开始，沿方法的调用栈逐层回溯查找，直到找到包含相应异常处理的方法，并把异常对象提交给该方法为止，这个过程称为捕获(catch)异常。**
   4. **Java异常处理机制**：**每当Java程序运行过程中产生一个可识别的运行错误时，系统都会产生一个相应的该异常类的对象。一旦一个异常对象产生了，系统中就一定有相应的机制来处理它，从而保证整个程序运行的安全性。**（Java中定义了很多异常类，每个异常类代表一种运行错误，类中包含了该运行错误的信息和处理错误的方法等内容。）
   5. In another word: 发现异常的代码可以“抛出”一个异常，运行系统“捕获”该异常，并交由程序员编写的相应代码进行异常处理。

#### 异常处理类
1. 在“异常”类层次上的最上层有一个单独的类叫做`Throwable`，它是`java.lang`包中的一个类。
2. `java.lang.Error`：由系统保留，通常Java程序不对这种错误进行直接处理，必须交由操作系统处理。
3. `java.lang.Exception`：供应用程序使用的，它是用户程序能够捕捉到的异常情况。
4. **Error类及其子类的对象，代表了程序运行时Java系统内部的错误。（非检查型异常）** 
5. **RuntimeException运行时异常应`通过程序调试尽量避免`而不是使用try-catch-finally语句去捕获它**
6. **Exceptino子类则是供应用程序使用的，是用户程序能够捕捉到的异常情况。（检查型异常）**
7. Exception构造方法：
    ```java
    public Exception（）；
    public Exception（String s）;
    ```
8. Exception常用方法：
    ```java
    public String toString()：//该方法返回描述当前Exception类信息的字符串。
    public void printStackTrace()：//该方法没有返回值，它的功能是完成一个输出操作，在当前的标准输出设备（一般是屏幕显示器）上输出当前异常对象的堆栈使用轨迹，即程序先后调用并执行了哪些对象或类的哪些方法，使得运行过程中产生了这个异常对象。
    ```
9. 异常类的层次结构如图如教材P156图9.1所示。
   1. ![异常类的层次结构](https://pic.imgdb.cn/item/616ccf102ab3f51d91603d77.jpg)
10. 程序对错误与异常的处理方式有三种：
   1. 一是**程序不能处理的错误，交操作系统处理**；
   2. 二是**程序应避免而可以不去捕获的运行时异常（RuntimeException）**；(老师解释：需要trycatch解决runtime异常，为了让程序不中断) (举个例子:别人调取你接口,理论上只应该有两种结果,获取成功、获取失败，但是实际生活当中，你可能会遇到访问失败、程序奔溃等等意外因素，这些意外因素，你能考虑到的地方，就尽量自己写代码去处理，而不是用**捕获**去处理，只有实在你想不到为什么会出现异常的情况，才需要使用**捕获**)
   3. 三是**必须捕获（使用try-catch-final）的非运行时异常**。

#### 异常的处理
1. 异常类异常处理是通过try、catch、finally、throw、throws五个关键字来实现的。
2. 异常的产生 
   1. >(教材P157例9.1)
      ```java
      package JavaBook.chap9;

      import java.io.IOException;

      public class App9_1 {
         public static void main(String[] args) throws IOException {
            int i;
            int[] a = {1, 2, 3, 4};
            try {
                  for (i = 0; i < 5; i++)
                     System.out.println("a[" + i + "]=" + a[i]);
            } catch (Exception e) {
                  e.printStackTrace();
            } finally {
                  System.out.println("finally!");
            }
            System.out.println("5/0=" + 5 / 0);
            System.out.println("main() end!");
         }
      }
      ```
3. 使用try-catch-finally语句捕获和处理异常
   1. 捕获异常
      1. **意义**：**能让程序来接收和处理异常对象，从而不影响其他语句的执行。**
      2. **过程**：**当一个异常被抛出时，有专门的语句来接收这个被抛出的异常对象。**
      3. 当一个异常类的对象被捕获或接收后，用户程序就会发生流程跳转，系统终止当前的流转而跳转到专门的异常处理语句块，或直接跳出当前程序和JVM回到操作系统。
   2. try-catch-finally语句语法格式：
        ```java
        try {
            要检查的语句序列  ；//可能产生异常的代码
        }
        catch (异常类名 形参对象名){
            异常发生时的处理语句序列；//捕获到某种异常对象时进行
                                                            //处理的代码
        }finally{
            一定会运行的语句序列
        }
        ```
   3. try-catch-finally语句捕获和处理异常的顺序：
      1. try块中代码抛出异常，若发生异常，则程序的运行便中断，并抛出由“异常类”所产生的“对象”。同时，该代码块也指定了它后面的catch语句所捕获的异常的范围，每个catch块都应该与一个try语句块相对应，这个try语句块用来启动Java的异常处理机制。
      2. catch用来指定需要捕获的异常类型，捕获到异常，然后流程自动跳过产生异常的语句后面的所有尚未执行的语句，系统就直接跳到catch语句中，查看是否有匹配的异常类，若有就执行相应语句。
      3. 无论try程序块是否捕获到异常，或者捕获到的异常是否与catch后面括号里的异常相同，最后一定会运行finally块里的程序代码；
      4. finally块的代码运行结束后，程序再转到try-catch-finally块之后的语句继续运行;
      5. 若try块中所有的语句都没有引发异常，则所有的catch块都会被忽略而不执行。
   4. 多异常处理
      1. 实现：**通过一个try块后面定义若干catch块来实现的，每个catch块用来接收和处理一种特定的异常对象**。
      2. 若try块产生的异常对象被第一个catch块所接收，则程序的流程将直接跳转到这个catch语句块中，try块中尚未执行的语句和其他的catch块将被忽略。若try块产生的异常
      3. 对象与第一个catch块不匹配，系统将自动转到第二个catch块进行匹配，依次类推，直到找到一个可以接收该异常对象的catch块，即完成流程的跳转。
      4. >见P教材例9.2,见教材中的说明
         ```java
         package JavaBook.chap9;

         import java.io.IOException;

         public class App9_2 {
            public static void main(String[] args) throws IOException {
               int i;
               int[] a = {1, 2, 3, 4};

               for (i = 0; i < 5; i++) {
                     try {
                        System.out.println("a[" + i + "]/" + i + "=" + (a[i] / i));
                        // 从小到大捕获！
                     } catch (ArrayIndexOutOfBoundsException e) {
                        System.out.println("ArrayIndexOutOfBoundsException");
                     } catch (ArithmeticException e) {
                        System.out.println("name" + e);
                     } catch (Exception e) {
                        System.out.println("catch " + e.getMessage() + " Exception!");
                     } finally {
                        System.out.println("  finally  i = " + i);
                     }
               }
               System.out.println("GOON");

            }
         }
         ```
#### 抛出异常
0. 根据异常类型的不同，抛出异常的方法也不同：
   1. 系统自动抛出的异常
   2. 指定方法抛出异常
   3. 所有系统定义的运作时异常都可以由系统自动抛出，指定方法抛出异常需要使用关键字throw或throws来明确指定在方法内抛出异常。
1. 抛出异常的方法
   1. 在方法体内使用throw语句抛出异常对象`throw  由异常类所产生的对象；`
   2. 在方法头部添加throws子句表示方法将抛出异常。`[修饰符] 返回值类型 方法名([参数列表]) throws 异常类列表`
2. 处理异常的方法
   1. 使用throw语句在方法内抛出异常，并在同一方法内进行相应的异常处理。
3. 抛出异常的方式：
   1. 使用throw语句抛出的异常：throw语句来定义何种情况算是产生了此种异常对应的错误，并抛出这个异常类的对象。使用throw语句抛出异常对象的语法格式为：`throw  由异常类所产生的对象；`
   2. >见教材 例9.3、9.4
      ```java
      package JavaBook.chap9;

      public class App9_3 {
         public static void main(String[] args) {
            int a = 5;
            int b = 0;
            try {
                  if (b == 0) {
                     System.out.println("1");
                     //抛出异常
                     throw new ArithmeticException();
                  } else {
                     System.out.println(a + "/" + b + "=" + a / b);
                  }
            }//捕获异常
            catch (ArithmeticException e) {
                  System.out.println("Exception: " + e + " is thrown!");
                  e.printStackTrace();
            }
         }
      }
      ```
      ```java
      package JavaBook.chap9;

      public class App9_4 {
         public static double multi(int n) {
            if (n < 0) {
                  throw new IllegalArgumentException("Find negative factorial exception");
            }
            double s = 1;
            for (int i = 1; i < n; i++) {
                  s = s * i;
            }
            return s;
         }

         public static void main(String[] args) {
            try {
                  args = new String[]{"-5"};

                  int m = Integer.parseInt(args[0]);
                  System.out.println(m + "!=" + multi(m));
            } catch (ArrayIndexOutOfBoundsException e) {
                  System.out.println("without input!");
            } catch (NumberFormatException e) {
                  System.out.println("need a Integer!");
            } catch (IllegalArgumentException e) {
                  System.out.println("Find an Exception named:" + e.toString());
            } finally {
                  System.out.println("end!");
            }
         }
      }

      ```
4. 在方法头使用throws抛出异常
   1. 如果在一个程序中的异常没有用try-catch语句捕获异常和处理异常的代码，则可以在程序代码所在的方法声明的后面用throws关键字声明该方法要抛出异常，将该异常抛出到该方法的调用方法中，一直可追溯到main()方法，由JVM处理。在方法声明中添加throws子句表示方法将抛出异常。带有throws子句的方法其声明格式如下：`[修饰符] 返回值类型 方法名([参数列表]) throws 异常类列表`
   2. >见教材 例9.5
      ```java
      package JavaBook.chap9;

      public class App9_5 {
         //方法后面那个是声明会抛出异常:我如果说我会抛出，但是实际ide没拿到这个异常，他就会说你为嘛说话不算数了
         static void check(String str1) throws NullPointerException {

            if (str1.length() > 2) {
      //            str1 = null;
      //            System.out.println(str1.length());
                  throw new NullPointerException();
            }
            char ch;
            for (int i = 0; i < str1.length(); i++) {
                  ch = str1.charAt(i);
                  if (!Character.isDigit(ch)) {
                     throw new NullPointerException();
                  }
            }
         }

         public static void main(String[] args) throws Exception {
            int num;
            try {
                  args = new String[]{"100"};
                  check(args[0]);
                  num = Integer.parseInt(args[0]);
                  if (num > 60) {
                     System.out.println("GoOn");
                  } else {
                     System.out.println("you need learn more!");
                  }
            } catch (NullPointerException e) {
                  System.out.println("NullPointerException:" + e.toString());
            } catch (NumberFormatException e) {
                  System.out.println("NumberFormatException:" + e.toString());
            } catch (Exception e) {
                  System.out.println("Exception:" + e.toString());
            }
         }
      }

      ```
5. 由方法抛出异常交系统处理
   1. 对于程序需要处理的异常，一般编写try-catch-finally语句捕获并处理，而对于程序中无法处理必须交由系统处理的异常，由于系统直接调用的是主方法main()，所以可以在主方法中使用throws子句声明抛出异常交由系统处理。
   2. >见教材 例9.6

#### 自动关闭资源的try语句
1. 自动关闭资源的try语句称为**try-with-resources语句**，也称为**自动资源管理语句**
2. **try-with-resources语句可以自动关闭在try-catch语句块中使用的资源。**
3. try-with-resources语句的格式如下：
   ```java
   try(声明或初始化资源的代码){
      使用资源对象res的语句
   }
   ```
4. **需强调一点并非所有的资源都可以自动关闭，只有实现java.lang.AutoCloseable接口的那些资源才可以自动关闭。**
5. **自动关闭资源的try语句相当于包含了隐式的finally语句块**，如果程序需要，后面也可以带catch块和finally块。
6. >见教材 例9.7

#### 自定义异常类
1. 系统定义的异常类主要用来处理系统可以预见且较常见的运行错误。
2. 用户自定义异常类主要用来处理用户程序中可能产生的逻辑错误，使得这种错误能够被系统及时识别并处理，而不致扩散产生更大的影响，从而使用户程序有更好的容错性能，并使整个系统更加稳定。
3. 创建用户自定义异常时，一般需完成如下工作：
   1. 声明一个新的异常类，**用户自定义的异常类必须是Throwable类的直接或间接子类**（Exception）。
   2. 为用户自定义的异常类**定义属性和方法**，或**覆盖父类的属性和方法**，使这些属性和方法能够体现该类所对应的错误信息。
   3. 用户自定义异常类不能由系统自动抛出，因而必须用throw来抛出。
   4. >见教材例9.8
      ```java
      package JavaBook.chap9;

      //App9_8.java
      class CircleException extends Exception  //自定义异常类，继承自Exception
      {
         double radius;

         CircleException(double r) {
            radius = r;
         }

         public String toString() {
            return "radius = " + radius + " ,which is not a positive number";
         }
      }

      class Circle    //定义Circle类
      {
         private double radius;

         public void setRadius(double r) throws CircleException   //由方法抛出自定义异常
         {
            if (r < 0)
                  throw new CircleException(r);   //抛出异常
            else
                  radius = r;
         }

         public void show() {
            System.out.println("Circle area=" + 3.14 * radius * radius);
         }
      }

      public class App9_8 {
         public static void main(String[] args) {
            Circle cir = new Circle();
            try {
                  cir.setRadius(-2.0);  //捕获由setRadius()方法抛出的异常
            } catch (CircleException e) {
                  System.out.println("Custom exception:" + e + "");
            }
            cir.show();
         }
      }
      ```
#### 总结：
1. 异常类：系统定义异常类、用户自定义异常类；
2. 异常对象的产生：
   1. 程序运行时由系统自动抛出
   2. 在方法体内用throw语句抛出
   3. 在方法头用throws语句抛出
3. 异常处理的两种方式：
   1. **使用try-catch-filnally(或 try-with-resources语句)处理**
   2. **在方法声明的头部使用throws语句抛出，将它送往上一层调用者处理。**
