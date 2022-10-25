---
title: OOP-Java-12
category: Java
date: 2021-10-19 15:34:09
tags:
---
### 泛型与容器类
#### 泛型generic
0. 介绍
   1. 泛型技术可以通过一种类型或方法操纵各种不同类型的对象，同时又提供了编译时的类型安全保证。
   2. 集合（容器）是以**类库形式**提供的多种数据类型，用户编程时可直接使用。
   3. 泛型通常（但不限于）与容器一起使用。
   4. 泛型其**实质**就是**将数据的类型参数化**，通过为类、接口及方法设置类型参数来定义泛型。
   5. 泛型使一个类或一个方法可在多种不同类型的对象上进行操作。
   6. 运用泛型**意味着编写的代码可以被多种类型不同的对象所重用，从而减少数据类型转换的潜在错误**。
   7. 使用泛型的**主要优点**：**能够在编译时而不是在运行时检测出错误。**
   8. **自动包装和自动解包**
      > 1. 当编译器发现程序在应该使用`包装类对象`的地方却使用`基本数据类型的数据`时，编译器将自动把`该数据`包装为`该基本类型对应的包装类的对象`，这个过程称为自动包装。
      > 2. 当编译器发现在应该使用`基本类型数据`的地方却使用了`包装类的对象`，则会把`该包装类对象`解包，从中取出`所包含的基本类型数据`，这个过程称为自动解包。
1. 泛型类的概念
   1. **泛型类**的定义是在类名后面加上<T>，
   2. **泛型接口**的定义是在接口名后面加上<T>，
   3. **泛型方法**的定义是在方法的返回值前面加上<T>，
   4. 其头部定义分别如下：
      1. *泛型类*的定义：`[修饰符] class 类名<T>`
      2. *泛型接口*的定义：`[public] interface 接口名<T>`
      3. *泛型方法*的定义：`[public] [static] <T> 返回值类型 方法名(T 参数)`
   5. T可以看作泛型定义中的“**类型形式参数**”，在应用具有泛型特性的类或接口时，需要使用“**类型实际参数**”，实际参数必须是**类类型**，利用泛型类创建的对象称为**泛型对象**，这个过程也成为**泛型实例化**。
2. 泛型类及应用
   1. 在*使用泛型定义的类创建对象*时，即在*泛型实例化*时，可以根据不同的需求给出类型参数T的具体类型。
   2. 可以把T看作一种特殊的变量，该变量的值在创建泛型对象时指定，它可以是除了基本类型之外的任意类型，包括类、接口、类型变量。
   3. >见【例12.1】泛型类的应用
      ```java
      package JavaBook.chap12;
      
      //泛型类的应用
      //filename:App12_1.java          泛型类的应用
      public class App12_1<T>         //定义泛型类，T是类型参数
      {
         private T obj;            //定义泛型类的成员变量

         public T getObj()         //定义泛型类的方法getObj()
         {
            return obj;
         }

         public void setObj(T obj)   //定义泛型类的方法setObj()
         {
            this.obj = obj;
         }

         public static void main(String[] args) {

            //泛型实例化
            App12_1<String> name = new App12_1<String>();  //创建App12_1<String>型对象
            App12_1<Integer> age = new App12_1<Integer>();  //创建App12_1<Integer>型对象

            //泛型类的实例化对象name 调用 泛型方法setObj()
            name.setObj("Zhang San");

            //newName是String的实例化对象，把泛型对象调用getObj()的值给newName
            String newName = name.getObj();
            System.out.println("newName: " + newName);
            age.setObj(25);                //Java自动将25包装为new Integer(25)
            int newAge = age.getObj();       //Java将Integer类型自动解包成int类型
            System.out.println("newAge: " + newAge);
         }
      }
      ```
   4. 注：**当一个泛型有多个类型参数时，每个类型参数在该泛型中都应该是唯一的**，如不能定义 Map<K,K>形式的泛型，但可以定义Map<K,V>形式的泛型。
3. 泛型方法
   1. *一个方法是否是泛型方法与其所在的类是否是泛型类没有关系*。
   2. 要定义泛型方法，只需将泛型的类型参数置于返回值类型前即可。
   3. *在Java中任何方法包括静态方法和构造方法都可声明为泛型方法。*
   4. 泛型方法除了定义不同，调用时与普通方法一样。
   5. *推荐使用返回值类型和参数类型一致的泛型方法。*
   6. *如果static方法需要使用泛型能力，必须使其成为泛型方法。*
   7. 类型推断只对赋值操作有效。
   8. >见【例12.2】和【例12.3】 泛型方法的应用
      ```java
      package JavaBook.chap12;

      //泛型方法的应用
      //filename App12_2.java
      public class App12_2             //定义一般类，即非泛型类
      {

      //    public static <E> void display(E[] list)  //定义泛型方法，E为类型参数
      //    {
      //        for (int i = 0; i < list.length; i++)
      //            System.out.print(list[i] + "  ");
      //        System.out.println();
      //    }
      //该方法的参数接收的是E类型的数组，而方法体则是输出参数list接收的数组的每个参数
         public static <E> void display(E[] list)  //定义泛型方法，E为类型参数
         {
            for (E e : list) {
                  System.out.print(e + "  ");
            }
            System.out.println();
         }

         public static void main(String[] args) {
            Integer[] num = {1, 2, 3, 4, 5};                     //定义数组
            String[] str = {"red", "Orange", "Yellow", "Green", "Cyanogen", "Blue", "Purple"};
            App12_2.<Integer>display(num);    //调用泛型方法
            App12_2.<String>display(str);
         }


      }
      ```
      ```java
      package JavaBook.chap12;

      //在泛型类中定义泛型方法，分别输出泛型类的类型参数和泛型方法的类型参数所属的类。
      //说明类的类型参数与泛型方法的类型参数是不同的。

      //泛型类
      class GenMet<T> {
         //泛型变量
         private T t;

         //泛型类的方法
         public void setObj(T t) {
            this.t = t;
         }
         //泛型类的方法

         public T getT() {
            return t;
         }

         //泛型方法
         public <U> void display(U u) {
            //打印类的类型参数T的类型
            System.out.println("Generic class T: " + t.getClass().getName());
            //打印泛型方法的参数U的类型
            System.out.println("Generic method U: " + u.getClass().getName());
            System.out.println("t: " + t);
            System.out.println("u: " + u);
         }
      }

      public class App12_3 {
         public static void main(String[] args) {
            //实例化一个Integer的T的对象
            GenMet<Integer> gen = new GenMet<>();
            //把T赋值为5
            gen.setObj(5);
            //获得T值
            System.out.println("gen.getT()" + gen.getT());

      //---
            System.out.println("first output: ");
            //调用泛型方法，接收字符串型的量
            //没有显式的传入实参的类型，java编译器会类型参数推断。
            gen.display("I'm the text");
      //        System.out.println("second output: ");
      //        //调用泛型方法，接收Double型的量
      //        gen.display(8.0);


            //Java三元表达式有字符强转的功能，返回值类型为两个返回值中类型精度更高的那个类型。
            int x = 2;
            double y = (x < 1) ? 2.2 : 2;
            System.out.println("value is " + y);
         }
      }
      ```
4. 限制泛型的可用类型
   1. 在定义泛型类时，默认可以使用任何类型来实例化一个泛型类对象，但Java语言也可以在用泛型类创建对象时对数据类型做出限制。其语法如下：`class ClassName<T extends anyClass>`,其中anyClass是指某个类或接口,T是anyClass的子类
   2. 这句话表示T是ClassName类的类型参数，且T有一个限制，即“T必须是anyClass类或者继承了anyClass类的子类或是实现了anyClass接口的类”，类型实际参数也是这个限制，且无论anyClass是类或者接口，在进行泛型限制时，都必须使用`extends`关键字。
   3. 在定义泛型类时，若没有使用extends关键字限制泛型的类型参数时，默认是Object类下的所有子类，即`<T>`和`<T extends Object>`是等价的。
   4. **泛型不是协变的**：若泛型的实际参数的类之间有父子关系时，参数化后得到的泛型类之间并不会具有同样的父子类关系，即子类泛型“并不是一种”父类泛型。
   5. >见【例12.4】 //有限制的泛型类
      ```java
      package JavaBook.chap12;

      //有限制的泛型类
      class GeneralType1<T extends Number> {
         T obj;

         //构造方法
         public GeneralType1(T obj) {
            this.obj = obj;
         }

         public T getObj() {
            return obj;
         }
      }

      public class App12_4 {
         public static void main(String[] args) {
            //实例化Integer的T的对象，走无参构造方法，obj=5
            GeneralType1<Integer> num = new GeneralType1<>(666);
            System.out.println("given params: " + num.getObj());
      //        not support
      //        GeneralType<String> s =new GeneralType<String>("Hello");
      //        System.out.println("given params: " + num.getObj());
         }
      }

      ```

5. 泛型的类型通配符和泛型数组的应用
   1. 使用通配符“?”创建泛型类对象，
      1. **通配符的主要作用**
         1. 创建可重新赋值但不可修改其内容的泛型对象
         2. 用在方法的参数中，限制传入不想要的类型实参。
   2. 声明泛型类对象o:
      1. 条件：只知道通配符“?”表示时`某个类`又或是`继承该类的子类`又或是`实现某个接口的类`，但具体是什么类型不知道。
      2. `泛型类名<? exends T> o=null;`
   3. >例子：通配符`?`的使用
        ```java
        App12_1<? exends List> x=null;
        x=new App12_1<LinkedList>();//正确  
        x=new App12_1<HashMap>();//错误
        ```
   4. 通配符“?”用于方法的参数中，防止传入不允许接收的类型实参。
      1. **非受限通配**：在创建泛型类对象时，如果只使用了“?”通配符，则默认是“? exends Object”，所以“?”也被称为非受限通配。
      2. **直接用通配符<?>创建泛型对象的特点**
         1. 具有通用性，即该泛型类的其他对象可以赋值给用通配符`?`创建的泛型对象，因为`?`等价于`? exends Object`，反之不可。
         2. 用通配符`?`创建的泛型对象，只能获取或删除其中的信息，但不可为其添加新的信息。
         3. 上限通配：`? exends Object`中，T被认为是类型参数`?`的上限。
         4. 下限通配：`? super Object`中，T被认为是类型参数`?`的下限，（T或T的一个未知父类型）。
         5. 引入通配符的主要目的：**支持泛型中的子类，实现多态**。
         6. *通配符与类型参数的区别：*
            1. 泛型方法中**类型参数**的优势：可以表达多个参数之间或参数与返回值之间的类型依赖关系。
            2. 如果方法中并不存在类型之间的依赖关系，则可以不使用泛型方法，而选用**通配符**。
            3. **通配符**更清晰、简明，在程序开发过程中建议尽量采用通配符。
         7. 由于JVM只是在编译时对泛型进行安全检查，所以特别强调以下几点：
            1. 不能使用泛型的类型参数T创建对象。
            2. 在泛型中可以用类型参数T声明一个数组，但不能使用类型参数T创建数组对象。
            3. 不能在静态环境中使用泛型类的类型参数T。
            4. 异常类不能是泛型的，即泛型类不能继承java.lang.Throwable类。
      3. >见【例12.5】类型通配符“?”的使用方法
         ```java
         package JavaBook.chap12;

         //类型通配符“？”的使用方法
         class GeneralType<T> {
            T obj;

            public void setObj(T obj) {
               this.obj = obj;
            }

            public T getObj() {
               return obj;
            }

            //下面的方法接收的泛型类对象参数中的类型参数只能是GeneralType实例出来的String或String的子类
            public static void showObj(GeneralType<? extends String> o) {
               System.out.println("given value is = " + o.getObj());
            }
         }

         public class App12_5 {
            public static void main(String[] args) {

               //实例化String的T的对象
               GeneralType<String> n = new GeneralType<>();
               //赋值obj
               n.setObj("fox");
               //n is String, so n can activate showObj()
               GeneralType.showObj(n);

               //and n can also getObj
               System.out.println("value type = " + n.getObj());

               //实例化Double的T的对象
               GeneralType<Double> num = new GeneralType<>();
               num.setObj(25.0);
               //num is not String, so num can not activate showObj()
               System.out.println("value type = " + num.getObj());

            }
         }
         ```
   5. 定义泛型类时也可以声明数组
      1. >【例12.6】 
         ```java
         package JavaBook.chap12;

         //定义一个泛型类，并在该类中利用类型参数声明数组
         public class App12_6<T> {

            //用类型参数T声明数组，即定义泛型数组
            private T[] array;

            //方法的参数接收的数组 是 类型参数T的类型
            public void setT(T[] array) {
               this.array = array;
            }

            public T[] getT() {
               return array;
            }

            public static void main(String[] args) {

               App12_6<String> a = new App12_6<String>();
               String[] array = {"Red", "Yellow", "Green"};
               a.setT(array);
               for (int i = 0; i < a.getT().length; i++) {
                     System.out.println(a.getT()[i] + " ");
               }

            }
         }

         ```
6. 继承泛型类与实现泛型接口
   1. 被定义为泛型的类或接口可被`继承`与`实现`。
   2. >例如：继承泛型类与实现泛型接口
        ```java
         package JavaBook.chap12;

         //定义一个泛型类，并在该类中利用类型参数声明数组
         public class App12_6<T> {

            //用类型参数T声明数组，即定义泛型数组
            private T[] array;

            //方法的参数接收的数组 是 类型参数T的类型
            public void setT(T[] array) {
               this.array = array;
            }

            public T[] getT() {
               return array;
            }

            public void showArray(T[] array) {
               for (T t : array) {
                     System.out.println(t + " ");
               }
            }

            public static void main(String[] args) {

               App12_6<String> a = new App12_6<String>();
               String[] array = {"Red", "Yellow", "Green"};
               a.setT(array);
               a.showArray(array);
         //        for (int i = 0; i < a.getT().length; i++) {
         //            System.out.println(a.getT()[i] + " ");
         //        }

            }
         }

        ```
---
#### 容器类
0. 介绍
   1. 容器类是Java以类库形式供用户开发程序时可直接使用的各种数据结构。数据结构不仅可以存储数据，还支持访问和处理数据的操作。这些数据结构存放在以**Collection**及**Map**接口为**根**的层次结构中，称为**Java容器(集合)框架**。Collection译为容器，Set译为集合。
   2. 从JDK5开始，容器框架**全部采用泛型实现**，且都存放在java.utli包中。
   3. ![容器框架中的接口及实现这些接口的类继承关系](https://pic.imgdb.cn/item/6174bb072ab3f51d91c20c61.jpg)
   4. 逻辑上：逻辑结构、线性结构、树结构、图结构
   5. 存储上：内存上：顺序存储（内存）、链式存储结构、哈希存储结构（硬盘）
   6. 框架中的接口声明了对各种集合类型执行的一般操作；
   7. 包括Collection、Set、List、Queue、Dueue、SortedSet、Map、SortedMap等，举例：
      1. `Set`的对象用于`存储一组不重复的元素集合`
      2. `List`的对象用于`存储一个由元素构成的线性表`
      3. `Map`保持了`键到值的映射`，可以通过键来实现对值的快速访问
1. 容器接口Collection
   1. Collection<E>接口声明了一组操作成批对象的抽象方法：查询方法、修改方法。添加元素、删除元素、管理数据。
   2. **Set和List接口都继承了Collection接口**
<!-- todo:Collection<E>接口的常用方法 -->
   1. *表12.1给出了Collection<E>接口的常用方法*
1. 列表接口List及其子类
   1. 扩展了Collection，是**包含有序元素的线性表**;
   2. **元素必须按顺序，可重复，可空值null；**
   3. 每个元素都有一个index值（从0开始）标明元素在列表中的位置。**List接口使用下标来访问元素。**
<!-- todo:List<E>接口的主要方法 -->
   4. *表12.2给出了List<E>接口的主要方法。*
2. 实现它的四个主要类是：LinkedList、ArrayList、VectorStack
3. `链表类LinkedList`：
   1. 采用链表结构保存对象，循环双链实现List
   2. 向链表中任意位置**插入、删除元素时不需要移动其他元素**，
   3. 链表的大小可以动态增大或减小
   4. 不具备随机存取特性
   5. 适合大量删除、存取操作，非连续
4. `数组列表类ArrayList`：
   1. 使用一维数组实现List，
   2. 可变数组，允许所有元素（包括null）
   3. 具有随机存取特性的特性
   4. **插入、删除时需要移动其他元素**，
   5. 当元素很多时插入、删除操作的速度较慢
   6. 添加元素时会自动增大，但是不会自动缩小(可以用trimToSize()缩小)
5. TODO:**如何选用这两种线性表***LinkedList、ArrayList的区别！*
   1. 若要通过下标随机访问元素，但除了在末尾处之外，不在其他位置插入或删除元素，应该选择ArrayList类
   2. 若要在线性表的任意位置上进行插入或删除元素，则应选择LinkedList类
   
   3. Vector；
   4. Stack。
<!-- todo:LinkedList<E>类和ArrayList<E>类的 构造方法、常用方法 -->
   5. 表12.3和表12.4分别给出了LinkedList<E>类和ArrayList<E>类的构造方法。
   6. 表12.5和表12.6分别给出了LinkedList<E>类与ArrayList<E>类的常用方法。
   7. >应用见【例12.7】利用LinkedList<E>类构造一个先进后出的堆栈
      ```java
      package JavaBook.chap12;
      //利用LinkedList<E>类构造一个先进后出的堆栈

      import java.util.LinkedList;
      import java.util.Scanner;

      class StringStack {
         private LinkedList<String> ld = new LinkedList<>();

         //将输入的数组入栈
         public void push(String name) {
            ld.addFirst(name);
         }

         //获取并删除栈顶数据
         public String pop() {
            return ld.removeFirst();
         }

         //重写了isEmpty()方法用于判断线性表ld是否为空
         public boolean isEmpty() {
            return ld.isEmpty();
         }
      }

      public class App12_7 {
         public static void main(String[] args) {
            Scanner sc = new Scanner(System.in);
            StringStack stack = new StringStack();
            System.out.println("plz input data (end with quit) : ");

            //将键盘输入的数据入栈，知道输入quit结束入栈操作
            while (true) {
                  String input = sc.next();
                  if (input.equals("quit")) {
                     break;
                  }
                  stack.push(input);
            }
            System.out.println("first come late out: ");

            //利用循环将栈中的数据以先进后出的顺序输出
            while (!stack.isEmpty()) {
                  System.out.println(stack.pop() + " ");
            }
         }
      }

      ```
    
7. 补充：**向量(Vector<E>)**
   1. 实现了Collection接口的具体类；
   2. 能够存储任意对象，但通常情况下，这些不同类型的对象都**具有相同的父类或接口**；
   3. 如果存储基本类型（primitive）的数据，系统会将这些数据**自动装箱**；
   4. 能够根据空间需要**容量自动扩充**；
   5. 增加元素方法的效率较高，除非空间已满，在这种情况下，在增加之前需要先扩充容量。
8. *区别***Vector<E>与ArrayList<E>的区别与联系**
   1. Vector与ArrayList一样，都是通过数组实现的，都有一个初始的容量大小，并可以设置初始的空间大小，当存储的空间不够时，需要增加存储空间，Vector默认增长原来的一倍，而ArrayList是原来的的0.5倍。
   2. **Vector支持线程的同步**，即某一时刻只有一个线程能够写Vector，避免多线程同时写而引起的不一致性
   3. **ArrayList是异步的**，不是线程安全的，但是因为同步影响执行效率，所以ArrayList比Vector性能好。
<!-- todo:Vector构造方法、常用方法 -->
9.  Vector<E>类的构造方法
     ```java
     Vector myVector = new Vector();  //初始容量为10 
     Vector myVector = new Vector(int cap); 
     Vector myVector = new Vector(Collection <? extends E> col);
     //以参数col中的元素进行初始化
     //也可用数组元素生成，但需先将数组转换成List对象，如
     String[]  num = {"one", "two", "three", "four", "five"}; 
     Vector<String>   aVector = new Vector<String>(java.util.Arrays.asList(num));
     ```
10. Vector类的常用方法（同ArrayList)：
    1.  void add(E e) :添加一个对象，如
         ```java
         Vector<String> teamList = new Vector<String>();  
         teamList.add("Zhang Wei");  
         teamList.add("Li Hong"); 
         ```
    2. int size():返回元素的个数。 
    3. boolean isEmpty() :如果不含元素，则返回true。
    4. boolean addAll(Collection <? extends E> col):添加整个集合，如果接收者对象的结果有变化，则返回true，如
         ```java
         Vector<String> teamList = new Vector<String>();  
         teamList.add("Zhang Wei");  
         teamList.add("Li Hong"); 
         Vector<String> yourList = new Vector<String>(); 
         yourList.addAll(teamList); 
         ```
    5. E get(int pos):返回指定位置的元素，如
         ```java
         Vector<String> teamList = new Vector<String>();  
         teamList.add("Zhang Wei");  
         teamList.add("Li Hong"); 
         teamList.add("Yu Hongshu");  
         String list1=teamList.get(1); // 返回 "Li Hong" 
         String list2=teamList.get(3); // 产生例外ArrayIndexOutOfBoundsException
         ```
    6. void set(int pos, E obj) :用参数对象替换指定位置的对象，如
         ```java
         Vector<String> teamList = new Vector<String>();  
         teamList.add("Zhang Wei");  
         teamList.add("Li Hong"); 
         teamList.add("Yu Hongshu");  
         teamList.set(2, "Liu Na");        
         System.out.println(teamList); //显示[Zhang Wei, Li Hong, Liu Na]
         teamList.set(3,"Ma Li");  // 产生例外ArrayIndexOutOfBoundsException
         ```
    7. boolean remove(Object obj) :去除给定对象的第一次出现，如果找到了对象，则返回true。去除一个对象后，其后面的所有对象依次向前移动。如
         ```java
         Vector<String> teamList = new Vector<String>();  
         teamList.add("Zhang Wei");  
         teamList.add("Li Hong"); 
         teamList.add("Yu Hongshu");  
         teamList.remove("Li Hong");
         teamList.remove("Wang Hong");//不做任何事，也不出现错误
         System.out.println(teamList);   // 显示[Zhang Wei,Yu Hongshu]
         ```
    8. E remove(int pos) :去除给定位置的元素，并返回被去除的对象。如
         ```java
         Vector<String> teamList = new Vector<String>();  
         teamList.add("Zhang Wei");  
         teamList.add("Li Hong"); 
         teamList.add("Yu Hongshu");
         teamList.remove(0);            //去除Zhang Wei
         teamList.remove(0);            //去除 Li Hong
         System.out.println(teamList);  // 显示[Yu Hongshu]
         teamList.remove(1);   //产生例外 ArrayIndexOutOfBoundsException
         ```
    9. boolean removeAll(Collection<?> col) :从接收者对象中去除所有在参数对象中出现的元素，如果接收者对象的结果有变化，则返回true。如
         ```java
         Vector<String> teamList = new Vector<String>();  
         teamList.add("Zhang Wei");  
         teamList.add("Li Hong"); 
         teamList.add("Yu Hongshu");
         Vector<String> yourList = new Vector<String>();  
         yourList.add("Yu Hongshu");  
         yourList.add("He Li"); 
         yourList.add("Zhang Wei"); 
         teamList.removeAll(yourList); 
         System.out.println(teamList);    // 显示[Li Hong]
         ```
    10. void clear() :去除所有的元素
    11. boolean contains(Object obj) :返回是否包含指定的对象，如果包含则返回true；否则，返回false
    12. boolean containsAll(Collection<?> col) :返回是否包含参数col中的所有对象
    13. int indexOf(Object obj) :返回给定对象在Vector /ArrayList中第一次出现的位置，如不存在，则返回-1。如
         ```java
         Vector teamList = new Vector();  
         teamList.add("Zhang Wei");  
         teamList.add("Li Hong"); 
         teamList.indexOf("Li Hong");      // 返回1
         teamList.indexOf("Zhang Li");     // 返回-1
         ```
    14. Enumeration<E> elements() :返回包含Vector中所有元素的Enumeration类对象。该方法只能应用于Vector对象，不能应用于ArrayList对象。如
         ```java
         Vector<String> teamList = new Vector<String>();  
         teamList.add("Zhang Wei");  
         teamList.add("Li Hong"); 
         teamList.add("Yu Hongshu");
         teamList.elements();  // 返回Enumeration类对象
         ```
    15. **Iterator<E> iterator() : 返回包含Vector/ArrayList中所有元素的Iterator类对象**
    16. **存取容器对象的方法:**
         1、使用foreach语句，绝大多数容器都支持该方式遍历元素；
         2、用容器中的toArray()方法把容器对象转换为数组，用循环语句访问数组中的元素；
         3、利用size()和get()方法
         4、利用迭代功能













11. **遍历（迭代）**
   0. 介绍
      1. **对容器中元素进行访问，经常需要按照某种次序对容器中的每个元素访问且仅访问一次，这就是遍历，也称为迭代。**
      2. **遍历是指从容器中获得当前元素的后续元素。**
   1. 对容器的遍历方式：（存取容器对象的方法）
      1. `foreach`循环语句
      2. 使用`Collection`接口中定义的`toArray()`方法将容器对象转换为数组，然后再利用循环语句对数组中的每个元素进行访问。
      3. 利用`size()`和`get()`方法进行遍历，先获取容器内的总个数，然后依次取出每个位置上的元素并访问，如下面的代码段。
      4. 使用java提供的迭代功能。
      5. >TODO:案例：把Customer对象存入Vector中，再使用get()方法取出。
         ```java
         //把Customer对象存入Vector中，再使用get()方法取出。代码如下：
         String[]  names = {"Zhang", "Li", "Wang", "Zhao"}; 
         Vector<Customer> v = new Vector<Customer>(); 

         for (int i=0; i<names.length; i++) { 
             Customer c = new Customer(); 
             c.setName(names[i]); 
             v.add(c); 
         }

         for (int i=0; i<v.size();i++) { 
              Customer c =v.get(i); 
             System.out.println(c.getName()); 
         }

         //Vector存储基本类型（primitive）的数据时，系统会自动进行装箱(与所有的集合类一样)。
         Vector<Double> rateVector = new Vector<Double>(); 
         double[]  rates = {36.25, 25.4, 18.34, 35.7,23.78}; 
         for (int i=0; i<rates.length; i++) 
             rateVector.add(rates[i]);

         //当从Vector中取出时，得到相应的包裹类型会自动拆箱还原为原始类型。代码如下：
         double sum = 0.0; 
         for (int i=0; i<rateVector.size();i++) 
            sum + = rateVector.get(i); 
         return sum;
         ```
12. `Iterator`、`ListIterator`接口
   1. `Iterator`能够从容器类对象中提取每一个元素，并提供了用于遍历元素的方法，但只支持从前向后的遍历；
      1. 三个实例方法：
         1. hasNext()  :判断是否还有元素；
         2. next()  :取得下一个元素；
         3. remove() :去除一个元素。注意是从集合中去除最后调用next()返回的元素，而不是从Iterator类中去除。（指向原来的Iterator）
      2. 在遍历的过程中，Iterator类对象能够与其对应的集合对象保持一致;
      3. Iterator只支持对List对象从前向后的遍历。
   2. `ListIterator`支持对容器类对象的双向遍历；
      <!-- todo:ListIterator常用方法 -->
      1. 常用方法表12.8、应用见【例12.8】
      2. >TODO:创建一个数组列表对象并向其添加元素，然后对列表的元素进行修改并遍历
         ```java
         package JavaBook.chap12;
         //filename：App12_8.java

         import java.util.ArrayList;
         import java.util.List;
         import java.util.ListIterator;

         public class App12_8 {
            public static void main(String[] args) {
               //创建数组列表对象al
               List<Integer> al = new ArrayList<Integer>();
               //输出
               for (int i = 1; i < 5; i++) {
                     //向数组列表al中添加元素
                     al.add(i);
               }

               System.out.println("ArrayList origin data: " + al);

               //创建数组列表al的迭代器listIter
               ListIterator<Integer> listIter = al.listIterator();
               //在序号为0的元素前添加一个元素
               listIter.add(0);
               System.out.println("data after add: " + al);

               if (listIter.hasNext()) {
                     System.out.println("listIter.hasNext()): " + listIter.hasNext());
         //            System.out.println("listIter.previousIndex()): " + listIter.previousIndex());
                     //指针会从第0个指向下一个
                     System.out.println("listIter.next()): " + listIter.next());
                     //指针会从第1个指向下一个
                     System.out.println("listIter.next()): " + listIter.next());
                     //指针会从第2个指向下一个，也就是listIter[3],是第四个数,值为3
                     int i = listIter.nextIndex();    //执行该语句时i的值是1
                     System.out.println("value of i is: " + i);
                     listIter.next();             //返回序号为1的元素
                     listIter.set(9);  //修改数组列表al中序号为1的元素
                     System.out.println("data after edit: " + al);
               }

               listIter = al.listIterator(al.size());   //重新创建从al最后位置开始的迭代器listIter
               System.out.print("reverse: ");    //反向遍历数组列表

               while (listIter.hasPrevious()) {
                     System.out.print(listIter.previous() + "  ");    //反向遍历数组列表
               }

            }
         }
         ```

13. `Arrays`类
  1. Arrays提供了一套专门用于操作数组的实用方法，它们作为静态方法存在该类中；
  2. 还包括将数组视为列表(List)的静态工厂。
<!-- todo:Arrays类常用方法 -->
  3. Arrays类常用方法：
  4. >例:数组的填充和复制。
  5. >例:数组的比较。
14. 集合接口`Set`及其子类
    1. `Set<E>接口`
       1.  扩展了Collection；
       2.  **无序**，集合中元素的顺序与元素加入集合的顺序无关；
       3.  **禁止重复的元素**，是**数学中“集合”的抽象**。
    2. `SortedSet<E>接口`
       1.  一种特殊的Set；
       2.  其中的元素是**升序排列**的，还增加了与次序相关的操作；
       3.  通常用于存放词汇表这样的内容。
    3. `哈希集合类HashSet<E>`
       1. 根据哈希码存取集合中的元素（名词：哈希码、哈希函数、哈希表、散列表、上座率、装填因子）
       2. 实现了Set接口，对equals()和hashCode()有了更强的约定，
       3. **如何比较两个HashSet中的元素是否相同**：
          1. 先比较hashCode()返回值是否相同，
          2. 若相同再使用equals()比较，
          3. 都相同则视为相同的元素。
       4. >例：将每个字符串添加到哈希集合中，集合中已有的元素不能添加，并将重复的元素输出。最后在对集合进行遍历，输出其所有元素。12_9
            ```java
            package JavaBook.chap12;//filename：App12_9.java

            //将每个字符串添加到哈希集合中，集合中已有的元素不能添加，并将重复的元素输出。
            //最后在对集合进行遍历，输出其所有元素。
            //HashSet特点：不重复、无顺序

            import java.util.HashSet;

            public class App12_9 {
               public static void main(String[] args) {

                  String[] input_thing = new String[]{
                           "1", "2", "3", "4", "5", "6", "7", "8", "9", "10",
                           "11", "12", "13", "14", "15", "16", "17", "18", "19", "20",
                           "11", "12", "13", "14", "15"
                  };

                  HashSet<String> hs = new HashSet<String>(); //创建哈希集合对象hs，初始容量为16
                  //LinkedHashSet<String> hs=new LinkedHashSet<String>();

                  for (String a : input_thing)
                        //如果hs没有添加成功a
                        if (!hs.add(a))          //向哈希集合hs添加元素，但重复的元素不添加
                        {
                           System.out.println("element: " + a + " is duplicate");        //输出重复的元素
                        }
                  System.out.println("Content of HashSet is: " + hs.size() + ", whose element is ");
                  //创建哈希集合hs的迭代器it
                  //判断集合中是否还有后续元素
                  for (String h : hs) {
                        System.out.print(h + "  ");   //输出哈希集合中的元素
                  }

               }
            }
            ```
    4. `树集合类TreeSet`
       1. **有序**
       2. **如果排序很重要，就选择TreeSet**，否则应该选用HashSet。
       3. >例：先创建一个哈希集合对象hs，并向其添加元素，然后再用hs创建树集合对象ts，之后利用树集合的相应方法输出某些元素。12_10
            ```java
            package JavaBook.chap12;//filename：App12_10.java
            // 先创建一个哈希集合对象hs，并向其添加元素，
            // 然后再用hs创建树集合对象ts，
            // 之后利用树集合的相应方法输出某些元素。12_10

            import java.util.HashSet;
            import java.util.Set;
            import java.util.TreeSet;

            public class App12_10 {
               public static void main(String[] args) {
                  Set<String> hs = new HashSet<>();   //创建哈希集合对象hs
                  hs.add("唐  僧1");        //向哈希集合的对象hs添加元素
                  hs.add("孙悟空2");
                  hs.add("猪八戒3");
                  hs.add("沙和尚4");
                  hs.add("白龙马5");
                  System.out.println("哈希集合：" + hs);
                  //要你自己定义排序规则，TreeSet后面写个{}，重写orderBy
                  TreeSet<String> ts = new TreeSet<>(hs);  //利用hs创建树集合对象ts
                  System.out.println("树集合：" + ts);          //输出树集合
                  System.out.println("树集合的第一个元素：" + ts.first());
                  System.out.println("树集合最后一个元素：" + ts.last());
                  System.out.println("headSet(孙悟空)的元素，孙悟空之前的：" + ts.headSet("孙悟空"));
                  System.out.println("tailSet(孙悟空)的元素：孙悟空以及之后的" + ts.tailSet("孙悟空"));
                  System.out.println("ceiling (沙)的元素：" + ts.ceiling("沙"));
                  //floor(E e) 方法返回在这个集合中小于或者等于给定元素的最大元素，如果不存在这样的元素,返回null.
                  //ceiling(E e) 方法返回在这个集合中大于或者等于给定元素的最小元素，如果不存在这样的元素,返回null.
               }
            }

            ```
    5. *区别***HashSet与TreeSet的抉择**
       1. 如果排序很重要，就选择TreeSet，否则应该选用HashSet。
       2. HashSet与LinkedHashSet的抉择：如果一定要让元素有序输出，就要使用LinkedHashSet！
    6. *区别***哈希表存储对象的方式与前面所讲的数组、Vector及ArrayList不同**：
       1. 数组、Vector及ArrayList中对象的存储位置是随机的，即对象本身与其存储位置之间没有必然的联系。因此查找一个对象时，只能以某种顺序（如顺序查找，二分查找）与各个元素进行比较，如果数组或向量中的元素数量很庞大时，查找的效率必然降低；
       2. 哈希表中，对象的存储位置和对象的关键属性k之间有一个特定的对应关系f，我们称之为哈希(Hash)函数。它使每个对象与一个唯一的存储位置相对应。因而在查找时，只要根据待查对象的关键属性k，计算f(k)的值即可知其存储位置。
    7. HashSet常用方法见教材表12.9、12.10，例题见【例12.9】；
    8. 树集合类TreeSet<E>实现了SortedSet接口，常用方法见教材表12.11、12.12，例题见【例12.10】。

15. 映射接口`Map`及其子类
    1. `Map<K,V>接口`
       1. Map中的元素都是成对出现的，它提供了键(Key)到值(Value)的映射，当需要通过关键字实现对值的快速存取时使用；
       2. 值是指要存入Map的元素（对象），键判定了元素在Map只的存储位置；允许键、值为空；
       3. Map中的键是唯一的，且每一个键最多只能映射到一个值。
       4. 常用方法见教材表12.13
    2. `SortedMap<K,V>接口`
       1. 一种特殊的Map，其中的关键字是**升序排列**的；
       2. 与SortedSet对等的Map，通常用于词典和电话目录等。
    3. `哈希映射HashMap<K,V>`、`HashTable<K,V>`
       1. 实现了Map接口；
       2. HashMap类与HashTable类很相似，但是
          1. **HashMap类允许有空的关键字**，
          2. **而HashTable类不允许空关键字，且线程安全**。
       3. HashMap<K,V>的构造方法见表12.14
       4. HashTable<K,V>的构造方法
       5. HashTable的常用方法
    4. `树映射TreeMap<K,V>`
       1. 实现了SortedMap接口；
       2. TreeMap类中**关键字不允许为空**且**升序排列**。
       3. 常用方法见教材表12.15、12.16
       4. >见【例12.11】。
            ```java
            package JavaBook.chap12;

            import java.util.*;

            public class App12_11 {
               public static void main(String[] args) {
                  Map<String, String> hm = new HashMap<>();   //创建HashMap对象hm
                  hm.put("006", "唐  僧");    //将元素添加到映射hm中
                  hm.put("008", "孙悟空");
                  hm.put("009", "猪八戒");
                  hm.put("007", "沙和尚");
                  hm.put("010", "白龙马");
                  hm.put("011", "白龙马");
                  hm.put("01255", "白龙马");
                  hm.put("01344", "白龙马");
                  hm.put("01433", "白龙马");
                  hm.put("01522", "白龙马");
                  System.out.println("哈希映射中的内容如下：\n" + hm);   //输出hm中的元素


                  String str = hm.remove("010");   //在hm中删除键值为“010”的元素

                  //从Map转Set
                  Set<String> keys = hm.keySet();     //获取哈希映射hm的键对象集合
                  System.out.println("键对象集合keys: " + keys);

                  //从Set转Iterator
                  Iterator<String> it = keys.iterator();   //获取键对象集合keys的迭代器
                  System.out.println("keys的迭代器iterator: " + it);

                  System.out.println("==================");
                  //HashMap类实现的Map映射，无序
                  System.out.println("HashMap类实现的Map映射，无序：");
                  while (it.hasNext())        //判断是否还有后续元素
                  {
                        String xh = it.next();        //返回键
                        String name = hm.get(xh);   //返回键所对应的值
                        System.out.println(xh + "  " + name);
                  }

                  //创建TreeMap对象tm
                  TreeMap<String, String> tm = new TreeMap<>(hm);                  //向树映射对象tm添加元素
                  Iterator<String> iter = tm.keySet().iterator();  //获取迭代器
                  System.out.println("TreeMap类实现的Map映射，键值升序：");
                  while (iter.hasNext())                //判断是否还有后续元素
                  {
                        String xh = iter.next();       //返回键
                        String name = hm.get(xh);    //返回键所对应的值
                        System.out.println(xh + "  " + name);
                  }
               }
            }

            ```





