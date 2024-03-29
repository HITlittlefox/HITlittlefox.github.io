---
title: OOP-Java-06&07    
category: Java  
date: 2021-10-13 21:39:54  
tags:
---
## 第6、7章 java面向对象技术基础

### 类与对象
-----------------------------------------
1. 类和对象的基本概**类(Class)**念
   1. **类(Class)**和**对象（Object）**是面向对象程序设计方法中最核心的概念。
   2. **类**是对某一类事物的描述(共性)，是抽象的、概念上的定义；
   3. 而**对象**则是实际存在的属该类事物的具体的个体，因而也称为**实例(Instance)**
   4. 类描述了对象的属性（静态特征）和对象的行为（动态特征）。
   5. 类是对象的模板、图纸。
   6. 对象(Object)则是类(Class)的一个实例(Instance)，是个实实在在的个体。（如果将对象比做汽车，那么类就是汽车的设计图纸。
   7. **面向对象程序设计思想的重点是*类的设计*，而不是对象的设计。**
   8. **类的构成:**类由**数据成员**与**函数成员**封装而成。
      1. Java语言把**数据成员**称为**域变量**、**属性**、**成员变量**等；而把**函数成员**称为**成员方法**，简称为**方法**。举例：圆柱体类。
         ![img_1.png](https://pic.imgdb.cn/item/616acf5e2ab3f51d91cf1e7c.jpg)
2. 类的声明
   1. 声明形式
         ```java
         [public] [abstract | final] class 类名称 
         [extends 父类名称][implements 接口名称列表]{
            　　　变量成员声明及初始化；
               　　　方法成员声明及方法体；
         }
         ```
      
   2. 关键字
      `class` 表明其后声明的是一个**类**。
      `extends` 声明的类是从某一**父类**派生而来，父类的名字写在extends之后
      `implements` 声明的类要实现某些**接口**，接口的名字写在implements之后
3. **类的修饰符**（可以有多个，用来限定类的使用方式）
      `public` 表明此类为**公有类**
      `abstract` 指明此类为**抽象类**
      `final` 指明此类为**终结类**
   1. 类声明体
      数据成员声明及初始化，可以有多个
      方法成员声明及方法体，可以有多个
   2. 实例：圆柱体类的定义
      ```java
      class Cylinder{   //定义圆柱体类Cylinder
         double radius;     //声明成员变量radius
         int height;        //声明成员变量height
         double pi=3.14;   //声明数据成员pi并赋初值
         void area( ) { //定义成员方法area()，用来计算底面积
               System.out.println("圆柱底面积="+ pi*radius* radius);
         }
         void volume( ) {  //定义成员方法volume ()，用来计算体积
               System.out.println("圆柱体体积="+((pi*radius* radius)*height);
            }
      }
      ```
4. 对象的创建与使用(对象之间靠互相传递消息而相互作用)
   1. 创建对象的步骤
      1. **声明指向“由类所创建的对象”的变量；**
      2. **利用new创建新的对象，并指派给前面所声明的变量。**
      3. >举例：
         ```Java
         //创建圆柱体类Cylinder的对象，可用下列的语法来创建：
         Cylinder volu; //声明指向对象的变量
         volu volu = new Cylinder();//利用new创建新的对象，并让变volu指向它
         
         //volu变量是指向由Cylinder类所创建的对象，所以可将它视为“对象的名称”，简称**对象**。事实上，volu只是对象的名称，它是指向对象实体的**引用变量**，而非对象本身。
         //在一个方法内部的变量必须进行初始化。除基本类型之外的变量都是引用类型。
         ```
   2. 在类定义内调用方法
      1. 在同一个类的定义里面，某一方法可以直接调用本类的其他方法而不需加对象名。见教材例6.3
      2. **若要强调是“对象本身的成员”的话，则可以在成员名前加`this`关键字**，即`this.成员名`。此时**this即代表调用此成员的对象**。
   3. 匿名对象
      1. 以当一个对象被创建之后，在调用该对象的方法时，也可以不定义对象的引用变量，而直接调用这个对象的方法，这样的对象叫做匿名对象。
         ```java
         //例如，若将
         Cylinder volu=new Cylinder();
         volu.SetCylinder(2.5, 5,3.14);
         //改写为：
         new Cylinder().SetCylinder(2.5, 5,3.14);
         //则Cylinder()就是匿名对象。
         ```
      2. *使用匿名对象的情况：*
         1. **如果对一个对象只需要进行一次方法调用。**
         2. **将匿名对象做为实参传递给一个方法调用。**
5. 成员变量
   1. 表示Java类的状态
      1. 声明数据成员必须给出变量名及其所属的类型，同时还可以指定其他特性；
      2. 在一个类中成员变量名是唯一的；
      3. 数据成员的类型可以是Java中任意的数据类型(简单类型、类、接口、数组)。
   2. 声明格式:
      ```java
      [public | protected | private]
      [static][final][transient][volatile]
      变量数据类型  变量名1[=变量初值], 
                  变量名2[=变量初值], … ;
      ```
   3. **变量的访问控制符：**格式说明：
      1. **public、protected、private 为访问控制符**
      2. `static`指明这是一个静态成员变量
      3. `final`指明变量的值不能被修改
      4. `transient`指明变量是临时状态
      5. `volatile`指明变量是一个共享变量
   4. **区分** *分为实例变量和静态（类）变量*  
      1. 实例变量
         1. 实例变量：**没有static修饰**的变量，用来存储所有实例都需要的属性信息，不同实例的属性值可能会不同。
         2. 可通过下面的表达式**访问实例变量的值：**`<对象名>.<实例变量名>`
      2. 静态变量（也叫类变量）
         1. 声明时需**加static修饰符**,不管类的对象有多少，**类变量只存在一份**，在整个类中只有一个值，类初始化的同时就被赋值。
         2. 适用情况：
            类中所有对象都相同的属性；
            经常需要共享的数据；
            系统中用到的一些常量值。
         3. 引用格式`<类名|对象名>.<类变量名>`
   5. `成员变量(静态变量、类变量)与局部变量（实例变量）的`**区别**
      1. 从语法形式上看，**成员变量属于类**，而**局部变量是方法中定义的变量或方法的参数**；
      2. 再从语法形式上看，**成员变量可以被public、private和static等修饰**，**而局部变量则不能**，**二者都可以被final修饰**。
      3. 从变量在内存中的存储方式看，**成员变量是对象的一部分，对象是存储在堆内存的**，**局部变量存于栈**。
      4. 从变量在内存中的生存时间上看，**成员变量是对象的一部分，它随着对象的创建而存在**；**局部变量随着方法的调用而产生，随着方法调用的结束而消失**。
      5. **成员变量若没有被赋初值，则自动初始化默认为0**（用final修饰的但没有被static修饰的成员变量必须显式赋值）；**局部变量不会自动赋值，必须显式赋值**。


6. 成员方法
   1. 成员方法：
      1. 包括**实例方法**与**静态方法**（其中静态方法又称作类方法）；
      2. 类的方法是用来定义对类的成员变量进行操作的，是实现类内部功能的机制，同时也是类与外界进行交互的重要窗口。可以没有，也可以有多个。
   2. 声明格式:
      ```java
      [public | protected | private] 
		[static][final | abstract][native][synchronized]
		返回类型  方法名([参数列表]) [throws exceptionList]{
		    方法体
		}
      ```
   3. 格式说明
      1. **方法的存取控制符与修饰符**
         1. `public`、`protected`、`private` 为**存取控制符**
         2. `static`指明方法是一个类方法
         3. `final`指明方法是一个终结方法
         4. `abstract`指明方法是一个抽象方法
         5. `native`用来集成java代码和其它语言的代码
         6. `synchronized`用来控制多个并发线程对共享数据的访问
      2. `返回类型`:可以是Java的任意数据类型,当不需要返回值时为`void`；
      3. `参数类型`:可以是Java的任意数据类型，可以有多个参数，也可以没有参数，方法声明时的参数称为`形式参数`；
      4. `方法体`：方法的实现，包括局部变量的声明以及所有合法的Java指令；
      5. `throws exceptionList`：用来处理异常。
      6. 分为`实例方法`和`静态方法(类方法)`
   4. 方法调用
      1. **给对象发消息**意味着调用对象的某个方法：
         从对象中取得信息 
         修改对象的状态或进行某种操作 
         进行计算及取得结果等
      2. **参数传递**：
         值传递：参数类型为基本数据类型时
         引用传递：参数类型为引用类型或数组时
7. 实例方法
   1. 特征：
      1. **实例方法：声明时前面不加static修饰符;**
      2. 表示特定对象的行为;
      3. 使用时需要发送给一个类实例。
   2. 引用格式`<对象名>.<方法名>([参数列表])`

8. 静态方法（类方法）
   1. **静态方法：表示类中对象的共有行为，声明时前面需加static修饰符；**
   2. static方法可以在不建立对象的情况下用类名直接调用，也可用类实例调用：`<类名称｜对象名>.<方法名>([参数列表])`
   3. static方法只能访问static成员变量或static方法。
   4. 在静态方法中不能使用this或super。

**Q:静态方法中能否调用实例变量或实例方法?**
>1. 静态方法加载时间快于实例;
>2. 如果要在静态方法中引用实例方法、实例变量，需要先实例化对象，然后通过`对象名.实例变量名`和`对象名.实例方法名()`

**Q:main方法的访问权限为何必须为public,static？**
>1. 由于JVM需要在类外调用main方法，
>2. 而且JVM运行main方法时，并没有创建main方法所在的类的一个实例对象，所以它只能通过类名来调用main方法作为程序的入口，因而该方法必须是static。
>3. jvm不会主动创建一个自定义类对象
>4. 调用实例方法必须要有一个已经创建过的类。但是执行你的程序前你是什么都没有的。所以 main 方法只能是静态的。
>5. 静态方法是类加载时就加载进去的一个地址 jvm调用只要知道地址就行。如果是非静态方法 那就必须创建实例后才会创建内部的方法函数，这个时候才知道函数具体调用入口

### 方法重载

1. **方法重载：一个类中名字相同的多个方法；**
2. 这些方法的参数必须不同，Java可通过**参数列表的不同**来辨别重载的方法：
   1. **参数列表**的不同
   2. 或者**参数个数**不同；
   3. 或者**参数类型**不同；
   4. **返回值**可以相同，也可以不同。
3. Java中不允许参数个数和参数类型完全相同，而只有返回值类型不同的重载。
4. 方法的重载是实现“多态”的方法之一，重载的价值在于**它允许通过使用一个方法名来访问多个方法**（**因为参数列表不同**）。
5. 见教材例7.3
   ```java
   int  add(int x, int y);
   int  add(int x, int y, int z);
   float  add(float f1, float f2);
   float add(float f1, int y);
   float add(int y, float f1);
   float  add(int x, int y);
   int add(int u, int v);
   ```

### 包(package)
1. 当声明多个类时，容易出现类名冲突。用包管理类名空间，它将各种类组织在一起，使得程序功能清楚、结构分明。
2. 利用包来管理类，可实现类的**共享**与**复用**；
3. 同一包中的类在默认情况下可以互相访问，通常把需要在一起工作的类放在一个包里，同一包中类名不能重复。

1. 包的声明
   1. 完整格式：`package pkg1[.pkg2[.pkg3…]];`
   2. Java源文件的第一条语句， 前面只能有注释或空行；
   3. 一个文件中最多只能有一条；
   4. 如果源文件中没有，则文件中声明的所有类属于一个默认的无名包，默认包为当前文件夹；
   5. 包名与对应文件夹名的大小写应一致。
   6. 包层次的根文件夹是由ClassPath来确定。
2. 包的命名
   1. **Java中包名使用小写字母表示；**
   2. 每个包的名称必须是“独一无二”的。
   3. 命名方式建议：
      1. 将机构的Internet域名反序，作为包名的前导；
      2. 若包名中有任何不可用于标识符的字符，用下划线替代；
      3. 若包名中的任何部分与关键字冲突，后缀下划线；
      4. 若包名中的任何部分以数字或其他不能用作标识符起始的字符开头，前缀下划线
3. 包与目录
   1. Java使用文件系统来存储包和类;
   2. 包名就是文件夹名，即目录名；
   3. 目录名并不一定是包名；
   4. 用javac编译源程序时，如遇到当前目录(包)中没有声明的类，就会以环境变量classpath为相对查找路径，按照包名的结构来查找。因此，要指定搜寻包的路径，需设置环境变量classpath。
4. 引入包
   1. 格式：`import package1[.package2…]. (classname |*);`
   2. 其中`package1[.package2…]`表明包的层次，它对应于文件目录；
   3. `classname`则指明所要引入的类名；
   4. 如果要引入一个包中的所有类，则可以使用星号（*）来代替类名；
   5. Java编译器为所有程序自动引入包`java.lang.*`。


5. 编译单元、编译及运行
   1. 编译单元：
      1. 一个Java源代码文件称为一个编译单元，由三部分组成：
         1. 所属包的声明(省略则属于默认包)；
         2. import (引入)包的声明，用于导入外部的类；
         3. 类和接口的声明。
      2. 一个编译单元中只能有一个public类，该类名与文件名相同，编译单元中的其他类往往是public类的辅助类，经过编译，每个类都会产一个class文件。
   2. 编译：
      1. 编译的过程是由  javac.exe这个程序来完成的。 虚拟机按以下顺序搜索并装载所有需要的类: 
         1. 引导类: 组成 java 平台的类, 包含在 tools.jar中的类;
         2. 扩展类: 使用 java 扩展机制的类, 该类位于扩展目录($JAVA_HOME%  /jre/lib/ext)中的 .jar 压缩文件中； 
         3. 用户类: 用户定义的类或者没有使用 java 扩展机制的第三方产品。用户使用 classpath 环境变量来确定这些类的位置。
   3. 运行:
      1. 运行一个包中的类时，必须指明包含这个类的包，而且要在适当的目录下运行，同时正确地设定环境变量CLASSPATH，使解释器能够找到指定的类。 

### 类及其成员的访问权限（p65）

1. 类的访问权限
   1. 有public（公共类）及无修饰符（缺省类）两种
   2. 访问权限符与访问能力之间的关系如表
   3. 不能访问 没有public的不同包中的类
   4. ![关系表](https://pic.imgdb.cn/item/61867a162ab3f51d913427db.jpg)
2. 类成员的访问权限
   1. **公有**(`public`)：可以被其他任何对象访问(前提是对类成员所在的类有访问权限) ;
   2. **保护**(`protected`)：只可被同一类及其子类、同一包内其他类的实例对象访问;
   3. **私有**(`private`)：只能被这个类本身访问，在类外不可见;
   4. **默认**(`default`)：仅允许同一个包内的访问；又被称为“包（package)访问权限”。
   5. ![关系表](https://pic.imgdb.cn/item/61867a2b2ab3f51d91344c2d.jpg)
3. get方法
   1. 功能是取得属性变量的值；get方法名以“get”开头，后面是实例变量的名字
   2. 一般具有以下格式：
      ```java
      public <fieldType> get<FieldName>(){ 
         return <fieldName>; 
      }
      ```
   3. 对于实例变量radius，声明其get方法如下：
      ```java
      public int getRadius(){
         return radius;
      } 
      ```
4. set方法
   1. 功能是修改属性变量的值；set方法名以“set”开头，后面是实例变量的名字。
   2. 一般具有以下格式：
      ```java
      public void set<FieldName>(<fieldType> <paramName>) { 
         <fieldName> = <paramName>; 
      }
      ```
   3. 声明实例变量radius的set方法如下：
      ```java
      public void setRadius(int r){  
         radius = r;  
      }
      ```

### final、this...

1. *final修饰符*
   1. **final修饰成员变量**
      1. 实例变量和类变量都可被声明为final；
      2. **如果一个成员变量前面有final修饰，这个成员变量就变成了常量，不允许在程序的其他地方修改；**
      3. final实例变量必须在每个构造函数结束之前赋初值，以保证使用之前会被初始化；
      4. final类变量必须在声明的同时初始化。
      5. 定义方式如下：
         ```java
         final [static]type variableName；
         ```
   2. **final修饰方法**
      1. 带有final修饰符的方法称为最终方法。不能被子类覆盖。把方法声明为最终方法有时可增加代码的安全性。
      2. 使用方式如下:
         ```java
         final  returnType  methodName(paramList){  }
         ```
   3. **final类**
      1. **final类不能被继承。**由于安全性的原因或者是面向对象的设计上的考虑，有时候希望一些类不能被继承。例如，Java中的String类，它对编译器和解释器的正常运行有很重要的作用，不能轻易改变它，因此把它修饰为final类，使它不能被继承，这就保证了String类型的唯一性。同时，如果你认为一个类的定义已经很完美，不需要再生成它的子类，这时也应把它修饰为final类。
      2. 定义一个final类的格式如下：
         ```java
         final class finalClassName{  ……   }
         ```
2. this
   1. **关键字this是用来指向当前对象的。**
   2. 当形式参数与成员变量名称相同时this不能省略。
3. super
   1. **`super`关键字指明是对父类的引用**。
4. null关键字
   1. **在Java语言规范中，null表示类或者变量是空，不代表任何对象或实例。**看下面的例子
      ```java
      SomeClass  aSomeClass=null；
      //上面的语句中，只定义了类SomeClass的实例aSomeClass，但并没有为之创建任何对象。
      ```
5. instanceof 运算符
   1. instanceof 运算符是双目运算符，左面的操作数是一个**对象**，右面是一个**类**。**当左面的对象是右面的类创建的对象时**,该运算符运算的结果是true ,否则是false。
      ```java
      //例：getClass和instanceof方法的使用。
      class SuperClass{
      }

      class SubClass extends SuperClass{
      }
      public class ClassAndInstance {
         static void test(Object x) {
            System.out.println("Testing x of type " + x.getClass());
            System.out.println("x instanceof SuperClass " + (x instanceof SuperClass));
            System.out.println("x instanceof SubClass " + (x instanceof SubClass));
         }
         public static void main(String[] args) {
            ClassAndInstance.test(new SuperClass()); 
            ClassAndInstance.test(new SubClass());
         }
      }
      //程序运行结果：如下：
      //Testing x of type class SuperClass
      //x instanceof SuperClass true
      //x instanceof SubClass  false
      //这里是因为匿名实例化出来了一个SuperClass()，它“是”SuperClass类的实例化，但是它“不是”SubClass类的实例化。

      //Testing x of type class SubClass
      //x instanceof SuperClass true
      //x instanceof SubClass true
      //这里是因为匿名实例化出来了一个SubClass()，它“不是”SuperClass类的实例化，但是它“是”SubClass类的实例化。      
      ```
6. java.lang.Object类（**p85**）
   1. 类java.lang.Object处于java开发环境的类层次的根部，其它所有的类都是直接或间接地继承了此类。该类定义了一些最基本的状态和行为。
   2. equals方法
      1. 两个对象,**同类型、同属性**，则称二者**相等**(equal)；
      2. 如果**两个引用变量指向的是同一个对象**，则称这两个变量(对象)**同一**(identical)。
      3. 两个对象同一，则肯定相等；
      4. 两个对象相等，不一定同一；
      5. 比较运算符“==” 判断的是这两个对象是否同一（若是基本数据类型则是判断是否相等）。
      6. **equals()**。
         1. Object类中的 `equals()` 方法的定义如下：
            ```java
            public boolean equals(Object x) { 
               return this == x; 
            }
            //可见， equals() 方法也是判断两个对象是否同一。
            ``` 
         2. 由于Object是类层次结构中的树根节点，因此所有其他类都继承了equals()方法。
      7. equals方法的重写
         1. 要判断同一个类的两个对象各个属性域的值是否相同(即两对象是否**相等**)，则不能使用从Object类继承来的equals方法，而需要在类声明中对equals方法进行重写。
         2. 重写前：equal判断是否**同一**
         3. 重写后：equal判断是否**相等**
         4. String类中已经重写了Object类的equals方法，可以判别两个字符串是否内容相同。
            ```java
            public boolean equals(Object x) { 
                  if (this.getClass() != x.getClass()) 
                     return false;      
                  Circle b = (Circle) x;     
                  return 
                  (this. radius == b. radius);
            }
            ```
7. 命令行参数的输入
8. JAR文件
9.  静态初始化器
   1. 是由关键字static修饰的{ }括起来的语句组，它的作用与类的构造方法有些相似，都是用来初始化工作的。

#### 对象初始化和回收

1. 对象初始化
   1. **系统在生成对象时，会为对象分配内存空间，并自动调用构造方法对实例变量进行初始化。**
2. 对象回收
   1. 对象不再使用时，系统会调用**垃圾回收程序**将其占用的内存回收。

3. **构造方法**：
   1. 构造方法(**constructor**)是一种特殊的方法，它是在对象被创建时初始化对象的成员的方法；
   2. Java中的每个类都有构造方法，没有定义构造方法的类，系统自动提供默认的构造方法。
   3. *构造方法的特点*：
      1. **方法名与类名相同；**
      2. **没有返回类型**，修饰符void也不能有（不含返回值的概念 不同于void，因为构造方法的返回值就是该类本身）；
      3. 通常被声明为公有的(**public**)；
      4. 可以有任意**多个参数**，还可以完成赋值之外的其他复杂操作；
      5. **不能在程序中显式的调用**，而是用new来调用；
      6. 在生成一个对象时，系统会**自动调用**该类的构造方法为新生成的对象初始化。
   4. *默认构造方法*
      1. 如果在类的声明中没有声明构造方法，则Java编译器会提供一个默认的构造方法；
      2. 默认的构造方法没有参数，其方法体为空；
      3. 使用默认的构造方法初始化对象时，如果在类声明中没有给实例变量赋初值，则对象的属性值为零或空。
   5. *自定义构造方法*
      1. 可在生成对象时给构造方法传送初始值，使用希望的值给对象初始化；
      2. 构造方法可以被**重载**，**构造方法的重载和方法的重载一致**。
      3. 说明：用户在进行类声明时，如果没有声明任何构造方法，系统会赋给此类一个默认（无参）的构造方法。但是，只要用户声明了构造方法，即使没有声明无参的构造方法，系统也不再赋默认的构造方法。
      4. 自定义无参的构造方法
         1. 无参的构造方法对其子类的声明很重要。如果在父类中不存在无参的构造方法，则要求其子类构造方法中显式调用父类构造方法，否则在子类构造方法会出错。
         2. 在声明构造方法时，好的声明习惯是
            1. 不声明构造方法；
            2. 如果声明，至少声明一个无参构造方法。
   6. 从一个构造方法内调用另一个构造方法
      1. 可以使用this关键字在一个构造方法中调用另外的构造方法；
      2. 代码更简洁，维护起来也更容易；
      3. 通常用参数个数比较少的构造方法调用参数个数最多的构造方法。
      4. >例:使用this关键字，修改BankAccout类中无参数和二参数的构造方法。
         ```java
         public BankAccount(String initName, int 
            initAccountNumber, float initBalance){ 
                  ownerName = initName; 
                  accountNumber = initAccountNumber; 
                  balance = initBalance; 
         }
         public BankAccount() { 
               this("李四", 999999, 0.0f); 
         } 
         public BankAccount(String initName, int initAccountNumber) { 
            this(initName, initAccountNumber, 0.0f);    
         }
         ```
   7. 公共构造方法与私有构造方法
      1. **构造方法一般都是public**，因为它们在创建对象时，是在类的外部被系统自动调用的。
      2. 构造函数若被声明为private，则无法在构造方法所在的类以外的地方被调用，但在该类的内部还是可以被调用。
      3. >见教材例7.7
   8. 构造方法执行顺序。
      1. >ex3_15
      2. 说明：
         1.**构造方法执行前先执行成员变量的声明；**
         2.**在一个构造函数中通过this关键字调用其他的构造函数的语句放在第一行。**

   9. 静态初始化器
      1. 是由关键字static修饰的{ }括起来的语句组，它的作用与类的构造方法有些相似，都是用来初始化工作的。
      2. *静态初始化器与构造方法区别*：
         1. 初始化对象不同：构造方法是对每个新创建的**对象**初始化，而静态初始化器对整个**类**自身进行初始化，包括static成员变量赋初值。
         2. 执行时机不同：构造方法是在用new创建新对象时由系统自动执行，而静态初始化器一般不能由程序来调用，它是在所属的类被加载入内存时由系统调用执行。
         3. 执行次数不同：用new创建多少个新对象，构造方法就调用多少次，但静态初始化器则在类被加载入内存时只执行一次。
         4. 静态初始化器不是方法，它没有方法名、返回值和参数。
         5. 如果有多个静态初始化器，则它们在类的初始化时会依次执行。

4. 内存回收技术
   1. 当一个对象在程序中不再被使用时，就成为一个无用对象：
      1. **当前的代码段不属于对象的作用域**；
      2. **把对象的引用赋值为空**。
   2. Java运行时系统通过垃圾收集器**周期性地**释放无用对象所使用的内存；
   3. Java运行时系统会在对对象进行自动垃圾回收前，**自动调用对象的`finalize()`方法**。
   4. finalize()方法
      1. 在类java.lang.Object中声明，因此Java中的每一个类都有该方法；
      2. 用于释放系统资源，如关闭打开的文件或socket等；
      3. 声明格式
         ```java
         protected void finalize() throws throwable
         ```
      4. 如果一个类需要释放除内存以外的资源，则需在类中重写finalize()方法。
   5. 垃圾收集器
      1. 自动扫描对象的动态内存区，对不再使用的对象做上标记以进行垃圾回收；
      2. 作为一个线程运行
         1. 通常在系统空闲时异步地执行。
         2. 当系统的内存用尽或程序中调用System.gc()要求进行垃圾收集时，与系统同步运行。

#### 6.7 应用举例
>对银行帐户类BankAccount进行一系列修改和测试  
   声明BankAccount类  
   声明toString()方法  
   声明存取款方法  
   使用DecimalFormat类  
   声明类方法生成特殊的实例  
   声明类变量  
```java

```
