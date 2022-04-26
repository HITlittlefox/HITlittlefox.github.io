---
title: OOP-Java-10
category: Java
date: 2021-10-15 18:02:18
tags:
---
### java语言的输入输出和文件处理
#### Java语言的输入输出
0. 介绍
   1. 输入输出是指**程序**与外部设备或其他计算机进行交互的操作。
   2. Java语言把这些输入与输出操作用**流**来实现，用统一的**接口**来表示。 
   3. Java语言的输入输出功能必须借助于**输入输出类库`java.io`包**来实现。
   4. 通常程序需要从外部获取/输出信息
      1. 这个“外部”范围很广，包括诸如键盘、显示器、文件、磁盘、网络、另外一个程序等;
      2. “信息”也可以是任何类型的，例如一个对象、串字符、图像、声音等。
1. 流的概念 
   1. 流(Stream)是指计算机各部件之间的数据流动。
   2. 一个流就是一个从源流向目的地的数据序列；
   3. 在Java中将信息的输入与输出过程抽象为I/O流：
      1. **输入是指数据流入程序**
      2. **输出是指数据从程序流出**
      3. 举例：
         1. **信息，从程序，流出去，到达文件----叫做输出**
         2. **信息，从文件，读出来，到达程序接收----叫做输入**
   4. I/O流类一旦被创建就会自动打开；
   5. 通过调用close方法，可以显式关闭任何一个流，如果流对象不再被引用，Java的垃圾回收机制也会隐式地关闭它。
   6. 输入流
      1. 为了从信息源获取信息，程序打开一个输入流，程序可从输入流读取信息。
      2. ![输入流](https://pic.imgdb.cn/item/616d65ad2ab3f51d91e0ac0d.jpg)
   7. 输出流
      1. 当程序需要向目标位置写信息时，便需要打开一个输出流，程序通过输出流向这个目标位置写信息。
      2. ![输出流](https://pic.imgdb.cn/item/616d65d42ab3f51d91e0cbb2.jpg)
   8. 不论数据从哪来，到哪去，也不论数据本身是何类型，读写数据的方法大体上都是一样的：
      1. 读--打开一个流--读信息--关闭流
      2. 写--打开一个流--写信息--关闭流
   9. 输入/输出流可以从以下几个方面进行分类：
      1. 从流的方向划分
         1. 输入流
         2. 输出流
      2. 从流的分工划分
         1. 节点流
         2. 处理流
      3. 从流的内容划分
         1. 面向字符的流（字符流）
         2. 面向字节的流（字节流）
2. 输入输出流类库
   1. java.io包中有四个基本类：InputStream、OutputStream及Reader、Writer类，它们分别处理字节流和字符流。 
   2. InputStream、OutputStream、Reader与Writer是抽象类，用于数据流的输入输出；
   3. File是文件类，用于对磁盘文件与文件夹的管理；
   4. RandomAccessFile是随机访问文件类，用于实现对磁盘文件的随机读写操作。 
   5. >见P175图10.2输入输出流的类层次结构图
   6. 字符流
      1. **字符流：针对字符数据的特点进行过优化，提供一些面向字符的有用特性**；
      2. 源或目标通常是文本文件；
      3. 实现内部格式和文本文件中的外部格式之间转换。
   7. 它们的子类又可分为两大类：
      1. 节点流：从数据源读入数据或往目的地写出数据；
      2. 处理流：对数据执行某种处理。
   8. 面向字符的抽象基类：Reader和Writer，多数程序使用这两个抽象类的子类来读/写文本信息，例如FileReader/FileWriter用来读/写文本文件。
   9. 字符流类结构
      1.  ![Reader](https://pic.imgdb.cn/item/616d67c62ab3f51d91e281cc.jpg)
      2.  ![Writer](https://pic.imgdb.cn/item/616d67e72ab3f51d91e29e39.jpg)
   10.字节流
      1. **字节流：数据源或目标中含有非字符数据，必须用字节流来输入/输出**；
      2. 通常被用来读写诸如图片、声音之类的二进制数据；
      3. 绝大多数数据被存储为二进制文件。世界上的文本文件大约只能占到2％，通常二进制文件要比含有相同数据量的文本文件小得多。
   11. InputStream和OutputStream是用来处理8位字节流的抽象基类，程序使用这两个类的子类来读写8位的字节信息，分为两部分：
       1.  节点流
       2.  处理流
   12. 字节流类结构
       1.  ![InputStream](https://pic.imgdb.cn/item/616d69072ab3f51d91e395f6.jpg)
       2.  ![OutputStream](https://pic.imgdb.cn/item/616d69132ab3f51d91e3a185.jpg)
3. 标准输入输出对象 
   1. System类的静态成员变量，包括
      1. System.in：InputStream类型的，代表标准输入流，这个流是已经打开了的，默认状态对应于键盘输入；
      2. System.out：PrintStream类型的，代表标准输出流，默认状态对应于屏幕输出；
      3. System.err：PrintStream类型的，代表标准错误信息输出流，默认状态对应于屏幕输出。
      4. >例:从键盘读入信息并在显示器上显示。
         ```java
         package JavaBook.chap10;

         import java.io.BufferedReader;
         import java.io.IOException;
         import java.io.InputStreamReader;

         //输出输入的内容
         public class Ex10_1 {
            public static void main(String[] args) throws IOException {
               BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
               String s;
               while ((s = in.readLine()).length() != 0)
                     System.err.println(s);
               in.close();

            }

         }
         ```
      5. System.in：程序启动时由Java系统自动创建的流对象，它是原始的字节流，不能直接从中读取字符，需要对其进行进一步的处理；
      6. InputStreamReader(System.in)：以System.in为参数创建一个InputStreamReader流对象，相当于字节流和字符流之间的一座桥梁，读取字节并将其转换为字符；
      7. BufferedReader：对InputStreamReader处理后的信息进行缓冲，以提高效率。
      8. 标准I/O重新导向：
         1. `setIn(InputStream)`： 设置标准输入流；
         2. `setOut(PrintStream)`：设置标准输出流；
         3. `setErr(PrintStream)`：设置标准错误输出流。
         4. >例：重导向标准输入System.in和标准输出System.out。
4. 处理流 
   1. **处理流：不直接与数据源或目标相连，而是基于另一个流来构造，从流读写数据的同时对数据进行处理**；
   2. InputStreamReader和BufferedReader都属于**处理流**：
      1. **InputStreamReader读取字节并转换为字符(字节流转换为字符流)**；
      2. BufferedReader对另一个流产生的数据进行缓冲。
   3. 缓冲流
      1. 为一个流配有一个缓冲区(Buffer)，一个缓冲区就是专门用于传送数据的一块内存 。当向一个缓冲流写入数据时，系统将数据发送到缓冲区，而不是直接发送到外部设备。缓冲区自动记录数据，当缓冲区满时，系统将数据全部发送到相应的外部设备。输入雷同。
      2. ![缓冲流](https://pic.imgdb.cn/item/616fcc662ab3f51d91a4370a.jpg)
      3. BufferedReader从键盘读入信息用一行表达式实现：
            ```java
            //从键盘读入信息
            BufferedReader stdin = new BufferedReader(new InputStreamReader(System.in));
            ```
5. I/O异常 
   1. 多数IO方法在遇到错误时会抛出异常，因此调用这些方法时必须：
      1. 在方法头声明抛出IOException异常；
      2. 或者在try块中执行IO，然后捕获IOException。

#### 文本文件的读写
0. 介绍
   1. 使用Reader和Writer类的子类来创建对象，再利用对象来处理文本文件的读写操作。
   2. **使用FileReader类读取文本文件**。
   3. **使用FileWriter类写文本文件**，FileWriter类继承自OutputStreamWriter类，而OutputStreamWriter类又继承自Writer类。
1. 写文本文件 
   1. FileWriter类 
      1. 创建一个磁盘文件 
      2. write() 方法
      3. 关闭一个磁盘文件
      4. 捕获I/O异常 
      5. 代码：
         ```java
         package JavaBook.chap10;

         import java.io.FileWriter;
         import java.io.IOException;

         //使用FileWriter类写入文件
         public class App10_5 {
            public static void main(String[] args) throws IOException {
               FileWriter fw = new FileWriter("C:\\Users\\96361\\Desktop\\programming-language-learning2\\Java--HITymr\\src\\JavaBook\\chap10\\love2.txt");
               char[] c = {'H', 'H', 'H', 'H', 'H', 'H'};
               String str = "Welcome to using java";
               fw.write(c);
               fw.write(str);
               fw.close();

            }
         }
         ```
   2. **BufferedWriter类**
      1. BufferedWriter写入，用一行表达式实现：
         ```java
         //BufferedWriter写入
         BufferedWriter out = new BufferedWriter(new FileWriter(fileName));
         ```
      2. 代码：
         ```java
         package JavaBook.chap10;

         import java.io.*;

         //使用BufferedWriter复制文本文件
         public class App10_8 {
            public static void main(String[] args) throws IOException {
               String str;

               try (

                        BufferedReader in = new BufferedReader(new FileReader("C:\\Users\\96361\\Desktop\\programming-language-learning2\\Java--HITymr\\src\\JavaBook\\chap10\\love.txt"));
                        BufferedWriter out = new BufferedWriter(new FileWriter("C:\\Users\\96361\\Desktop\\programming-language-learning2\\Java--HITymr\\src\\JavaBook\\chap10\\love2.txt"));


               ) {
                     while ((str = in.readLine()) != null) {
                        System.out.println(str);
                        out.write(str);
                        out.newLine();
                     }
                     out.flush();
               } catch (IOException ioe) {
                     System.out.println("error! " + ioe);
               }
            }
         }
         ```
   3. >例:在E盘根目录创建文本文件Hello.txt，并往里写入若干行文本。
      ```java
      package JavaBook.chap10;

      import java.io.FileWriter;
      import java.io.IOException;

      //使用FileWriter把信息写入文件
      class Ex10_3 {

         public static void main(String[] args) throws IOException {
            //main方法中声明抛出IO异常
            String fileName = "C:\\Users\\96361\\Desktop\\programming-language-learning\\Java--HITymr\\src\\JavaBook\\chap10\\Hello1.txt";
            //String fileName = "E:\\Hello1.txt";

            FileWriter writer = new FileWriter(fileName, true);
            writer.write("Hello\n");
            writer.write("This !is my first text file,\n");
            writer.write("You can see how this is done.\n");
            writer.write("输入一行中文也可以\n");
            writer.write("呐呐呐\n");
            writer.close();
         }
      ```
   4. Writer类的流可实现内部格式到外部磁盘文件格式的转换：
      1. “Hello.txt”是一个普通的ASCII码文本文件，每个英文字符占一个字节，中文字符占两个字节；
      2. Java程序中的字符串则是每个字符占两个字节的，采用Unicode编码。
2. 读文本文件 
   1. FileReader类
      1. 从文本文件中读取字符
      2. 继承自Reader抽象类的子类InputStreamReader
      3. 代码：
         ```java
         package JavaBook.chap10;

         import java.io.FileReader;
         import java.io.IOException;

         //使用FileReader类读取文件
         public class App10_4 {
            public static void main(String[] args) throws IOException {
               char[] c = new char[500];
               try (FileReader fr = new FileReader("C:\\Users\\96361\\Desktop\\programming-language-learning2\\Java--HITymr\\src\\JavaBook\\chap10\\love.txt");
               ) {
                     int num = fr.read(c);
                     String str = new String(c, 0, num);
                     System.out.println("read chars number is: " + num + ", and their content is: ");
                     System.out.println(str);
               }
            }
         }
         ```
         TODO:here!
   2. **BufferedReader**
      1. 读文本文件的缓冲器类
      2. 具有readLine()方法，可以对换行符进行鉴别，一行一行地读取输入流中的内容
      3. 继承自Reader
      4. 代码：
         ```java
         package JavaBook.chap10;

         import java.io.BufferedReader;
         import java.io.FileReader;
         import java.io.IOException;

         //使用BufferedReader读取文本文件
         public class App10_7 {
            public static void main(String[] args) throws IOException {
               String thisLine;
               int count = 0;
               try (FileReader fr = new FileReader("C:\\Users\\96361\\Desktop\\programming-language-learning2\\Java--HITymr\\src\\JavaBook\\chap10\\love.txt");
                     BufferedReader bfr = new BufferedReader(fr)) {
                     while ((thisLine = bfr.readLine()) != null) {
                        count++;
                        System.out.println(thisLine);
                     }
                     System.out.println("total read " + count + " line.");
               } catch (IOException ioe) {
                     System.out.println("error!" + ioe);
               }
            }
         }
         ```
   3. BufferedReader从文件读取，一行表达式实现：
        ```java
        //BufferedReader读取方法：
        BufferedReader bfr = new BufferedReader(new FileReader(fileName)); 
        ```
       1. ![文件输入方法](https://pic.imgdb.cn/item/616d74cd2ab3f51d91ee1431.jpg)
       2. >例:从Hello.txt中读取文本并显示在屏幕上。
3. 文本文件的复制            
   1. >教材P191例10.8 
   2. >例:指定源文件和目标文件名，将源文件的内容拷贝至目标文件。
   <!-- TODO:文本文件的复制-->
   3. ![概览](https://pic.imgdb.cn/item/6170d80b2ab3f51d916590b6.jpg)
      ```java
      package JavaBook.chap10;

      import java.io.*;

      class CopyMaker {
         String sourceName, destName;
         BufferedReader source;
         BufferedWriter dest;
         String line;

         //打开文件
         private boolean openFiles() {
            try {
                  //打开源文件
                  source = new BufferedReader(new FileReader(sourceName));
            } catch (IOException iox) {
                  System.out.println("Problem opening source file:" + sourceName);
                  return false;
            }
            try {
                  //打开目标文件
                  dest = new BufferedWriter(new FileWriter(destName));
            } catch (IOException iox) {
                  System.out.println("Problem opening destination file:" + destName);
                  return false;
            }

            return true;
         }

         //复制内容
         private boolean copyFiles() {
            try {
                  //读
                  line = source.readLine();
                  //写
                  while (line != null) {
                     dest.write(line);
                     dest.newLine();
                     //读
                     line = source.readLine();
                  }
            } catch (IOException iox) {
                  System.out.println("Problem reading or writing");
                  return false;
            }

            return true;
         }

         //关闭文件
         private boolean closeFiles() {
            boolean retVal = true;

            try {
                  //关闭源文件
                  source.close();
            } catch (IOException iox) {
                  System.out.println("Problem closing source file:" + sourceName);
                  retVal = false;
            }

            try {
                  //关闭目标文件
                  dest.close();
            } catch (IOException iox) {
                  System.out.println("Problem closing destination file:" + destName);
                  retVal = false;
            }

            return retVal;
         }

         //复制器的复制方法，有两个参数，一个是source原文件，一个是destination目标文件
         public boolean copy(String src, String dst) {
            sourceName = src;
            destName = dst;
            return openFiles() && copyFiles() && closeFiles();
         }
      }


      public class Ex10_6 {
         public static void main(String[] args) {
            if (args.length == 2) {
                  CopyMaker cm = new CopyMaker();
                  cm.copy(args[0], args[1]);
            } else
                  System.out.println("Please Enter File names");
         }
      }         

      ```
   4. 共包括两个类：
      1. CopyMaker
         1. private boolean openFiles()
         2. private boolean copyFiles()
         3. private boolean closeFiles()
         4. public boolean copy(String src, String dst ) 
      2. Ex10_6
         1. main()   
#### 二进制文件的读写
0. 介绍
   1. 二进制文件
      1. 原则上讲，所有文件都是由8位的字节组成的；
      2. 如果文件字节中的内容应被解释为字符，则文件被称为文本文件；如果被解释为其它含义，则文件被称为二进制文件；
      3. 例如文字处理程序，例如字处理软件Word产生的doc文件中，数据要被解释为字体、格式、图形和其他非字符信息。因此，这样的文件是二进制文件，不能用Reader流正确读取。
   2. 为什么需要二进制文件
      1. 输入输出更快；
      2. 比文本文件小很多；
      3. 有些数据不容易被表示为字符。
1. 写二进制文件
   1. 抽象类OutputStream
   2. 派生类FileOutputStream
      1. 用于一般目的输出（非字符输出）；
      2. 用于成组字节输出。
   3. 派生类DataOutputStream
      1. 具有写各种基本数据类型的方法；
      2. 将数据写到另一个输出流；
      3. 它在所有的计算机平台上使用同样的数据格式；
      4. 其中size方法可作为计数器，统计写入的字节数。
      5. >教材例10.1、10.2二进制文件读写
      6. >例:将三个int型数字255、0、－1写入数据文件data1.dat。
   4. BufferedOutputStream类
      1. 写二进制文件的缓冲流类；
      2. 类似于文本文件中的BufferedWriter；
      3. 对于大量数据的写入，可提高效率；
      4. BufferedOutputStream类用法示例：
            ```java
            DataOutputStream out = new DataOutputStream(new BufferedOutputStream(new FileOutputStream( fileName ) ) ); 
            ```
      5. >例:向文件中写入各种数据类型的数，并统计写入的字节数。
2. 读二进制文件 
   1. FileInputStream
   2. DataInputStream
   3. BufferedInputSteam 
      1. 读写整数 
      2. 读写单字节 
   4. >例:读取上例创建的数据文件中的3个int型数字，显示相加结果
3. 二进制文件复制 
   1. >例:从命令行输入源文件名和目标文件名，将源文件复制为目标文件。
4. 其他I/O流 
   1. 顺序输入流(SequenceInputStream)：它是InputStream的直接子类，其功能是将多个输入流顺序连接在一起，形成单一的输入数据流，没有对应的输出数据流存在。
   2. 管道输入输出流：它提供了利用管道方式进行数据输入输出管理的类。管道流用来将一个程序或线程的输出连接到另外一个程序或线程作为输入，使得相连线程能够通过PipedInputStream和PipedOutputStream类进行数据交换，从而可以实现程序内部线程间的通信或不同程序间的通信。
   3. 过滤输入流类FilterInputStream和过滤输出流类FilterOutputStream，分别实现了在数据的读、写操作的同时进行数据处理。
#### File类
1. 专门用来管理磁盘文件和文件夹；
2. 定义了一些与平台无关的方法来操纵文件：
   1. 创建、删除文件；
   2. 重命名文件；
   3. 判断文件的读写权限及是否存在；
   4. 设置和查询文件的最近修改时间等。
3. 构造文件流可以使用File类的对象作为参数。
4. File类构造方法及常用方法参见教材P192表10.19、10.20、10.21   例10.9

#### 文件压缩与解压缩
0. 压缩流类
   1. java.util.zip包中提供了一些类，使我们可以以压缩格式对流进行读写；
   2. 它们都继承自字节流类OutputStream和InputStream；
   3. 其中GZIPOutputStream和ZipOutputStream可分别把数据压缩成GZIP格式和Zip格式；
   4. GZIPInputStream和ZipInputStream可以分别把压缩成GZIP格式或Zip的数据解压缩恢复原状。
1. 简单的GZIP压缩格式
   1. GZIPOutputStream
      1. 父类是DeflaterOutputStream；
      2. 可以把数据压缩成GZIP格式。
   2. GZIPInputStream
      1. 父类是 InflaterInputStream； 
      2. 可以把压缩成GZIP格式的数据解压缩。
2. 运用ZIP压缩多个文件
   1. Zip文件
      1. 可能含有多个文件，所以有多个入口(Entry);
      2. 每个入口用一个ZipEntity对象表示，该对象的getName()方法返回文件的最初名称。
   2. ZipOutputStream
      1. 父类是DeflaterOutputStream；
      2. 可以把数据压缩成ZIP格式。
   3. ZipInputStream
      1. 父类是InflaterInputStream；
      2. 可以把压缩成ZIP格式的数据解压缩。

#### 对象序列化
TODO:here
0. 通俗化解释
   1. 对象在内存里和在硬盘上不能用同一种表示，对象在内存里存储的时候会使用引用或者指针，引用或者指针没法被保存到硬盘上，所以只能把对象“序列化”成一种东西（取决于具体的实现，既可以选择二进制，也可以选择ASCII或者其他文本）
1. **保存对象的信息，在需要的时候，再读取这个对象叫对象序列化；**
2. 内存中的对象在程序结束时就会被垃圾回收机制清除；
3. 用于对象信息存储和读取的输入输出流类：
   1. `ObjectInputStream`  把对象读入程序；
   2. `ObjectOutputStream`  对象写入磁盘文件；
   3. 对象要想实现序列化，其所属的类必须实现Serializable接口；
   4. 不保存对象的transient和static类型的变量。
4. Seriealizable接口
   1. 空接口，使类的对象可实现序列化；
   2. Serializable 接口的定义：
        ```java
        package java.io;
        public interface Serializable {
            // there's nothing in here!
        }
        ```
5. 实现Serializable接口的语句
    ```java
    public class MyClass implements Serializable {
        ...
    }
    ```
6. 使用关键字transient可以阻止对象的某些成员被自动写入文件。
7. >例:创建一个书籍对象，并把它输出到一个文件book.dat中，然后再把该对象读出来，在屏幕上显示对象信息。
   ```java
   package JavaBook.chap10;

   //例:创建一个书籍对象，并把它输出到一个文件book.dat中，然后再把该对象读出来，在屏幕上显示对象信息。

   import java.io.*;

   //对象要想实现序列化，其所属的类必须实现Serializable接口；
   class Book implements Serializable {
      int id;
      String name, author;
      float price;

      public Book(int id, String name, String author, float price) {
         this.id = id;
         this.name = name;
         this.author = author;
         this.price = price;
      }
   }

   public class Ex10_16 {
      public static void main(String[] args) throws IOException, ClassNotFoundException {
         Book book = new Book(100032,
                  "Java Programming Skills",
                  "Wang Sir",
                  30);
         //建立一个输出流(信息从程序流向文件)
         ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("book.dat"));
         //写入输出流
         oos.writeObject(book);
         //输出流关闭
         oos.close();

         book = null;
         //建立一个输入流(信息从文件流向程序)
         ObjectInputStream ois = new ObjectInputStream(new FileInputStream("book.dat"));
         //写入输入流
         book = (Book) ois.readObject();
         //输入流关闭
         ois.close();
         System.out.println("ID is:" + book.id);
         System.out.println("name is:" + book.name);
         System.out.println("author is:" + book.author);
         System.out.println("price is:" + book.price);
      }
   }
   ```

#### 随机文件读写
1. RandomAccessFile类
   1. 可跳转到文件的任意位置读/写数据；
   2. 可在随机文件中插入数据，而不破坏该文件的其他数据；
   3. 在等长记录格式文件的随机读取时有很大的优势，但仅限于操作文件，不能访问其它IO设备，如网络、内存映像等；
   4. 有个位置指示器，指向当前读写处的位置。刚打开文件时，文件指示器指向文件的开头处。对文件指针显式操作的方法有：
        ```java
        int skipBytes(int n)：//把文件指针向前移动指定的n个字节；
        void seek(long)：//移动文件指针到指定的位置；
        long getFilePointer()：//得到当前的文件指针。
        //RandomAccessFile常见方法参见教材P195表10.22-10.24
        ```
   5. >例:创建一个雇员类，包括姓名、年龄。姓名不超过8个字符，年龄是int类型。每条记录固定为20个字节。使用RandomAccessFile向文件添加、修改、读取雇员信息。
      ```java
      package JavaBook.chap10;

      //创建一个雇员类，包括姓名、年龄。姓名不超过8个字符，年龄是int类型。每条记录固定为20个字节。使用RandomAccessFile向文件添加、修改、读取雇员信息

      import java.io.RandomAccessFile;
      import java.util.Arrays;

      //创建一个雇员类，包括姓名、年龄。
      class Employee {
         char[] name = {'\u0000', '\u0000', '\u0000', '\u0000', '\u0000', '\u0000', '\u0000', '\u0000'};
         int age;

         public Employee(String name, int age) throws Exception {
            if (name.toCharArray().length > 8) {
                  System.arraycopy(name.toCharArray(), 0, this.name, 0, 8);
            } else
                  System.arraycopy(name.toCharArray(), 0, this.name,
                        0, name.toCharArray().length);
            this.age = age;
         }
      }

      public class Ex10_17 {
         String Filename;


         public Ex10_17(String Filename) {
            this.Filename = Filename;
         }

         //使用RandomAccessFile向文件添加雇员信息
         public void writeEmployee(Employee e, int n) throws Exception {
            RandomAccessFile ra = new RandomAccessFile(Filename, "rw");
            ra.seek(n * 20L); //将位置指示器移到指定位置上

            //限制长度
            for (int I = 0; I < 8; I++)
                  ra.writeChar(e.name[I]);

            ra.writeInt(e.age);
            ra.close();
         }

         //使用RandomAccessFile向文件读取雇员信息
         public void readEmployee(int n) throws Exception {
            char[] buf = new char[8];
            RandomAccessFile ra = new RandomAccessFile(Filename, "r");
            ra.seek(n * 20L);

            //限制长度
            for (int I = 0; I < 8; I++)
                  buf[I] = ra.readChar();

            System.out.print("name:" + Arrays.toString(buf));
            System.out.println("age:" + ra.readInt());
            ra.close();
         }

         public static void main(String[] args) throws Exception {
            Ex10_17 t = new Ex10_17("employee.txt");

            //建三个雇员对象
            Employee e1 = new Employee("ZhangSantt", 23);
            Employee e2 = new Employee("littlefox", 33);
            Employee e3 = new Employee("wang hua", 19);

            //随机写入
            t.writeEmployee(e1, 0);
            t.writeEmployee(e3, 2);
            t.writeEmployee(e2, 1);

            //随机读取
            System.out.println("first employee");
            t.readEmployee(0);

            System.out.println("third employee");
            t.readEmployee(2);


            System.out.println("second employee");
            t.readEmployee(1);
         }
      }
      ```