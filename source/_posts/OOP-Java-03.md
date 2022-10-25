---
title: OOP-Java-03
category: Java
date: 2021-10-26 16:11:58
tags:
---
### Java语言基础

#### 数据类型
1. ![数据类型](https://pic.imgdb.cn/item/617d06ac2ab3f51d91510613.jpg)
2. 编码方式：
   1. 编码方式：ASCII码（字符）
   2. GB2312国标编码（汉字）
   3. Unicode新的国际标准编码（中英文）
      1. Unicode字符采用\u0000 ----\uFFFF之间的十六进制表示。
      2. Unicode字符表的前128个刚好是ASCII表。


#### 关键字与标识符
1. **关键字(保留字、都是小写)**
2. 标识符：用来表示变量名、类名、方法名、数组名和文件名的有效字符序列 。 规定：
   1. 可以由字母、数字、下划线( _ )、美元符号($)组合而成。
   2. 必须以字母、下划线或美元符号开头，不能以数字开头。
   3. 关键字不能当标识符使用。
   4. 区分大小写。
3. 编码习惯：**类名首字母大写**，**变量、方法及对象首字母小写。**

#### 常量\变量
1. 常量：存储的是在程序中不能被修改的固定值。
   1. 整型常量
   2. 浮点型常量（单精度后加f或F，双精度后加d或D可省略）
   3. 布尔（逻辑）型常量
   4. **字符型常量 ：单引号。**（转义字符见教材表3.6）
   5. **字符串常量 ：双引号。**
2. 变量：变量的声明、初始化、赋值（Java语言程序中可以随时定义变量，不必集中在执行语句之前。）
#### 数据类型的转换规则
1. **数值型**不同类型数据的转换
   1. 自动类型转换
      1. 转换前的数据类型与转换后的类型兼容。
      2. 转换后的数据类型的表示范围比转换前的类型大。（条件②说明不同类型的数据进行运算时，需先转换为同一类型，然后进行运算。转换从“短”到“长”的优先关系为：byte→short→char→int→long→float→double）   
   2. 强制类型转换 
      1. 如果要将较长的数据转换成较短的数据时（不安全），
      2. 就要进行强制类型转换。强制类型转换的格式如下：
   3. 格式：`（欲转换的数据类型）变量名`
   4. **字符串型**数据与整型数据相互转换 
      1. 字符串转换成数值型数据
            ```java
            String MyNumber = "1234.56";
            float MyFloat = Float.parseFloat(MyNumber);
            ```
      2. 数值型数据转换成字符串 
         1. 在Java语言中，字符串可用加号“+”来实现连接操作。所以若其中某个操作数不是字符串，该操作在连接之前会自动将其转换成字符串。所以可用加号来实现自动的转换。   
            ```java
            int MyInt=1234；               //定义整形变量MyInt
            String  MyString=""+MyInt；    //将整型数据转换成了字符串 
            ```
#### 从键盘输入数据
1. 利用键盘输入数据，Java语言提供了两种方式
   1. 方式1：利用键盘输入数据
        ```java
        //方式1：利用键盘输入数据
        //由键盘输入的数据，不管是文字还是数字，Java皆视为字符串，因此若是要由键盘输入数字则必须再经过转换。 
        import java.io.*;
        public class class_name {  //类名称
        public static void main(String[] args) throws IOException{
            ……
            String str;
            BufferedReader buf;
            buf=new BufferedReader(new InputStreamReader(System.in));
            ……
            str=buf.readLine(); 
            ……
        }
        }
         
        //输入字符串
        import java.io.*;    //加载java.io类库里的所有类
        public class App3_3{
        public static void main(String[] args) throws IOException{
            BufferedReader buf;
            String str;
            buf = new BufferedReader (new InputStreamReader (System.in));
            System.out.print("请输入字符串；");
            str = buf.readLine();        //将输入的文字指定给字符串变量str存放
            System.out.println("您输入的字符串是："+str);   //输出字符串
        }
        }

        //输入数值:由于从键盘输入的数据均被视为字符串，所以从键盘上输入的数据，必须先利用表3.7中所提供的方法进行转换后，字符串的内容才会变成数值。 
        //App3_4.java         由键盘输入整数
        import java.io.*;
        public class App3_4{
        public static void main(String[] args) throws IOException{
            float num;
            String str;
            BufferedReader buf;
            buf=new BufferedReader(new InputStreamReader(System.in));
            System.out.print("请输入一个实数：");
            str=buf.readLine();         //将输入的文字指定给字符串变量str存放
            num= Float.parseFloat(str);   //将str转换成float类型后赋给num
            System.out.println("您输入的数为："+num);
        }
        }

        //输入多个数据
        import java.io.*;
        public class App3_5{
        public static void main(String[] args) throws IOException{
            int num1,num2;
            String str1,str2;
            InputStreamReader in;
            in= new InputStreamReader(System.in);
            BufferedReader buf;
            buf=new BufferedReader(in);
            System.out.print("请输入第一个数：");
            str1=buf.readLine();         //将输入的内容赋值给字符串变量str1
            num1=Integer.parseInt(str1);   //将str1转成int类型后赋给num1
            System.out.print("请输入第二个数：");
            str2=buf.readLine();         //将输入的内容赋值给字符串变量str2
            num2=Integer.parseInt(str2);   //将str2转成int类型后赋给num2
            System.out.println(num1+"*"+num2+"="+(num1*num2));
        }
        }
        ```
   2. 方式2：为了简化输入操作，在java.util类库中新增了一个类**专门用于输入操作的类Scanner**，可以使用该类输入一个对象。
        ```java
        //方式2：为了简化输入操作，在java.util类库中新增了一个类专门用于输入操作的类Scanner，可以使用该类输入一个对象。
        import java.util.*;
        public class class_name  {
        public static void main(String[] args) {
            Scanner reader=new Scanner(System.in); 
            double num;      
            ……
            num=reader.nextDouble();  
            ……
        }
        }
        // 在该结构中用创建的reader对象调用nextDouble()方法来读取用户从键盘上输入的double型数据，也可用reader对象调用下列方法，读取用户在键盘上输入的相应类型的数据：
        //nextByte()      nextDouble()       nextFloat()
        //nextInt()         nextLong()          nextShort()
        //next()              nextLine()  


        //利用Scanner输入多个数据
        import java.util.*;    //加载java.util类库里的所有类
        public class App3_6{
        public static void main(String[] args){
            int num1;
            double num2;
            Scanner reader=new Scanner(System.in);
            System.out.print("请输入第一个数：");
            num1= reader.nextInt();       //将输入的内容做int型数据赋值给变量num1
            System.out.print("请输入第二个数：");
            num2= reader.nextDouble();    //将输入的内容做double型数据赋值给变量num2
            System.out.println(num1+"*"+num2+"="+(num1*num2));
        }
        }
        //上例中，reader对象还可以调用nextByte()、nextFloat()、nestDouble()、nextInt()等。
        //next×××()被调用后，则等待用户在命令行输入数据并按回车键（或空格键、Tab键）确认。
        //next()和nextLine()方法表示等待用户在键盘上输入一行文本，然后返回一个String类型的数据。


         //利用Scanner类，使用next()和nextLine()方法接收从键盘输入字符串型数据。 
         import java.util.*;    //加载java.util类库里的所有类
         public class App3_7{
         public static void main(String[] args){
            String s1,s2;
            Scanner reader=new Scanner(System.in);
            System.out.print("请输入第一个数：");
            s1= reader.nextLine();       //将输入的内容作为字符型数据赋值给变量s1
            System.out.print("请输入第二个数：");
            s2= reader.next();           //按Enter键后next()方法将回车符和换行符去掉
            System.out.println("输入的是"+s1+"和"+s2);
         }
         }
        ```
   3. Scanner类，next()和nextLine()方法区别
      1. next()：一定要读取到有效字符后才可以结束输入，对输入有效字符之前遇到的空格键、Tab键或Enter键等结束符，它将自动将其去掉，只有在输入有效字符之后，该方法才将其后输入的这些符号视为分隔符。
      2. nextLine()：结束符为Enter键，即返回Enter之前的所有字符。

#### 运算符与表达式
1. 按照运算符功能来分，基本的运算符有下面几类。
   1. 算术运算符  +、-、*、/、%、++、--
   2. 关系运算符  >、<、>=、<=、==、!=
   3. 逻辑运算符  !、&&、||、&、| 、^
   4. 位运算符    >>、<<、>>>、&、|、^、~
   5. 赋值运算符  =、扩展赋值运算符，如+=、/=等。
   6. 条件运算符  `? :`
   7. 其他运算符 包括分量运算符.、下标运算符[ ]、实例运算符instanceof、内存分配运算符new、强制类型转换运算符(类型)、方法调用运算符()等。    
2. 算术运算
   1. ＋  －   *   /   %   ＋（取正）  －（取负）  ++   --
   2.  两个整数相“/”，结果为整数。对于两个整数之间的除法和取模运算，则式子(a/b)*b+(a%b)==a是恒成立的。
   3.  对取模运算符“%”来说，其操作数可以为浮点数。即a % b与a-((int)(a/b)*b)的语义相同，这表示a % b的结果是除完后剩下的浮点数部分。如37.2%10=7.2。(默认双精度)
   4.  值得注意的是Java语言**对加运算符进行了扩展**，使它能够进行字符串的连接，如"abc"+"de"，得到字符串"abcde"。 
3. 关系运算
   1.  `>、<、>=、<=、==、!=`
   2.  用于比较两个值之间的大小，结果为true或false；
   3.  不能在浮点数之间作“==”的比较，因为浮点数在表达上有难以避免的微小误差，精确的相等比较无法达到，所以这类比较没有意义。 
4. 逻辑运算
   1.  !、&&、||、&、|、^（异或）
   2.  逻辑运算和关系运算的关系非常紧密，关系运算的结果为布尔型，逻辑运算的操作数与运算结果都是布尔型。
   3.  **简洁运算(&&、||)与非简洁运算(&、|)的区别在于：**
       >1. 非简洁运算在必须计算完左右两个表达式之后，才取结果值；
       >2. 而简洁运算可能只计算左边的表达式而不计算右边的表达式，
       >3. 即对于&&，只要左边表达式为false，就不计算右边表达式，则整个表达式为false；
       >4. 对于||，只要左边表达式为true，就不计算右边表达式，则整个表达式为true。
5. 位运算和赋值运算
   1. 位运算符： >>、<<、>>>、&、|、^、~  
   2. 赋值运算符： =、扩展赋值运算符（+=等）
      1. 自动类型转换
      2. 右结合性
6. 条件运算与字符串运算
   1.  条件运算符：表达式1  ? 表达式2 : 表达式3
   2.  字符串运算符
       1. 字符串运算符“+“是以String为对象进行的操作。运算符“+“完成字符串连接操作，如果必要，则系统自动把操作数转换为String型。 
            ```java
            float a=100.0；      //定义变量a为浮点型
            print("The value of a is"+a+"\n")； //系统自动将a转换成字符串
            String s1+=a；//s1=s1+a，若a非String型，自动转换为String型。
            ```
   3. 表达式及运算符的优先级、结合性
      1. 见教材表3.14
      2. >练习p38   3.18
