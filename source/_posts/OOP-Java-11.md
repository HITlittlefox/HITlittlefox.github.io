---
title: OOP-Java-11
category: Java
date: 2021-10-15 18:02:25
tags:
---
## 第11章 多线程

1. 线程的概念
   1. 程序、进程、多任务与线程
      1. 程序:**由指令和数据构成的完成某种功能的文件**；
      2. 进程:**一个独立程序的每一次运行**；
      3. 多任务:**在一个系统中可以同时运行多个进程**；
      4. 线程:**一个进程中可以同时执行的子任务；**
   2. 线程的状态与生命周期
      1. 要实现多线程，必须在**主线程**中创建**新的线程对象**，Java语言使用**Thread类及其子类的对象**来表示线程，新建线程在它的生命周期内通常要经历五种状态。
         1. **新建状态-->就绪状态-->运行状态-->阻塞状态（Blocked）-->消亡状态**
         2. start()--run()--wait()--notify()--Synchronized()--run()--yield()--run()--sleep()--run()--run()
         3. 通过线程的**控制**与**调度**可使线程在这几种状态间转化。
      2. **线程生命周期：线程从产生到消亡的过程。**
      3. ![线程生命周期](https://pic.imgdb.cn/item/616ace6a2ab3f51d91cd9290.jpg)
   3. 线程的优先级
      1. 每个Java线程都有一个**优先级**，其范围都在1和10之间，数字越大优先级越高。默认情况下，每个线程的优先级都设置为5；
      2. 在线程A运行过程中创建的新的线程对象B，初始状态具有和线程A相同的优先级；
      3. 可在线程创建之后的任何时候，通过`setPriority(int priority)`方法改变其原来的优先级。
      4. **调度：指在各个线程之间分配CPU资源。**
         1. 线程调度有两种模型：
            1. 分时模型
            2. 抢占模型
            3. Java语言支持**抢占式调度模型**
      5. 基于线程优先级的线程调度：
         1. 具有较高优先级的线程比优先级较低的线程优先执行；
         2. **对具有相同优先级的线程，Java的处理是随机的**；
         3. 底层操作系统支持的优先级可能要少于10个，这样会造成一些混乱。因此，只能将优先级作为一种很粗略的工具使用。
2. 线程的创建
   > 在Java中创建多线程有**继承java.lang包中的Thread类**和**实现Runnable接口**两种方法。
   1. 利用Thread类的子类来创建线程
      1. Thread类的**构造方法**见教材表11.1所示
      2. Thread类的其**常用方法**如表11.2所示。
      3. TODO:*由Thread类创建多线程的方法:*
         1. 从Thread类派生一个子类，并创建这个子类的对象，就可以产生一个新的线程；
         2. 这个子类应该重写Thread类的`run()`方法，在run方法中写入需要在新线程中执行的语句段；
         3. 这个子类的对象需要调用`start()`方法来启动，新线程将自动进入run方法。原线程将同时继续往下执行。
         4. > 案例1：例11.1由Thread类创建多线程的方法:
            ```java
            package JavaBook.chap11;

            //由Thread类创建多线程的方法:
            //从Thread类派生一个子类，并创建这个子类的对象，就可以产生一个新的线程；
            //这个子类应该重写Thread类的run()方法，在run方法中写入需要在新线程中执行的语句段；
            //这个子类的对象需要调用start()方法来启动，新线程将自动进入run方法。原线程将同时继续往下执行。

            //使用Thread类的子类来创建线程
            class MyThread extends Thread {
               private final String who;

               public MyThread(String str) {
                  who = str;
               }

               public void run() {
                  for (int i = 0; i < 5; i++) {
                        try {
                           int num = (int) (1000 * Math.random());
                           System.out.println(num);
                           sleep(num);
                        } catch (InterruptedException e) {
                           e.printStackTrace();
                        }
                        System.out.println(who + "is running!");
                  }
               }
            }

            public class App11_1 {
               public static void main(String[] args) {

                  MyThread you = new MyThread("you");
                  MyThread she = new MyThread("she");
                  you.start();
                  she.start();
                  System.out.println("main() ran over!");
               }
            }

            ```
         5. > 案例2：例:创建两个具有不同优先级的线程，都从1递增到200000，每增加50000显示一次。
            ```java
            package JavaBook.chap10;

            //例:创建两个具有不同优先级的线程，都从1递增到200000，每增加50000显示一次。
            class TestThread extends Thread {
               private int tick = 1;
               private int num;

               public TestThread(int i) {
                  this.num = i;
               }

               public void run() {
                  while (tick < 200000) {
                        tick++;
                        //每隔5000进行显示
                        if ((tick % 50000) == 0) {
                           System.out.println("Thread #" + num + ", tick = " + tick);
                           //放弃执行权
                           Thread.yield();
                           try {
                              sleep(1);
                           } catch (InterruptedException e) {
                              e.printStackTrace();
                           }
                        }
                  }
               }

            }


            public class ex7_5 {
               public static void main(String[] args) {
                  TestThread[] runners = new TestThread[2];
                  for (int i = 0; i < 2; i++) {
                        //创造多线程
                        runners[i] = new TestThread(i);
                  }
                  //设置第一个线程优先级为2
                  runners[0].setPriority(2);
                  //设置第二个线程优先级为3
                  runners[1].setPriority(2);
                  for (int i = 0; i < 2; i++) {
                        //start多线程
                        runners[i].start();
                  }
               }
            }

            ```
   2. 利用Runnable接口创建线程
      1. TODO:*由Runnable接口创建多线程的方法:*
         1. Runnable接口只有一个方法`run()`，用户可以声明一个类实现Runnable接口，并实现`run()`方法，将线程代码写入其中；
         2. **通过创建该类的对象创建线程**；
         3. 通过该对象创建一个Thread类,调用`start()`方法启动此线程就会在此线程上运行`run()`方法。
         4. > 案例1：例11.2由Runnable接口创建多线程
            ```java
            package JavaBook.chap11;

            //由Runnable接口创建多线程
            class MyThread implements Runnable {
               private String who;

               public MyThread(String str) {
                  who = str;
               }

               public void run() {
                  for (int i = 0; i < 5; i++) {
                        try {
                           int num = (int) (1000 * Math.random());
                           System.out.println(num);
                           //MyThread类是由Runnable实现的，所以sleep()需要加前缀Thread
                           Thread.sleep(num);
                        } catch (InterruptedException e) {
                           e.printStackTrace();
                        }
                        System.out.println(who + "is running!");
                  }
               }
            }

            public class App11_2 {
               public static void main(String[] args) {
                  MyThread you = new MyThread("you");
                  MyThread she = new MyThread("she");
                  Thread t1 = new Thread(you);
                  Thread t2 = new Thread(you);
                  t1.start();
                  t2.start();


               }
            }
            ```
         5. > TODO:案例2：例11.3多线程中join()方法
            ```java
            package JavaBook.chap11;

            //多线程中join()方法

            class MyThread1 extends Thread {
               private final String who;

               public MyThread1(String str) {
                  who = str;
               }

               public void run() {
                  for (int i = 0; i < 5; i++) {
                        try {
                           int num = (int) (1000 * Math.random());
                           System.out.println(num);
                           sleep(num);
                        } catch (InterruptedException e) {
                           e.printStackTrace();
                        }
                        System.out.println(who + "is running!");
                  }
               }
            }

            public class App11_3 {
               public static void main(String[] args) {

                  MyThread1 you = new MyThread1("you");
                  MyThread1 she = new MyThread1("she");
                  you.start();
                  try {
                        //当某一线程调用join()方法时，则其他线程会等到该线程结束后才开始执行。
                        you.join();
                  } catch (InterruptedException e) {
                        e.printStackTrace();
                  }

                  she.start();
                  try {
                        she.join();
                  } catch (InterruptedException e) {
                        e.printStackTrace();
                  }

                  System.out.println("main() ran over!");
               }
            }

            ```
   3. **区别：***两种创建线程对象的方式的特点*：
      >1. 直接继承Thread类的特点是：
      >   1. 编写简单，可以直接操纵线程；
      >   2. 但缺点是若继承Thread类，就不能再继承其他类。
      >2. 使用Runnable接口的特点是：
      >   1. 可以将Thread类与所要处理的任务的类分开，形成清晰的模型；
      >   2. 还可以从其他类继承，从而实现多重继承的功能
      >   3. 相比于Thread类，Runnable更适合于多个线程处理同一资源。
      >   4. 几乎所有多线程应用都可以用实现Runnable接口的方式来实现
      >   5. 主要区别就在于对**数据的共享**上。使用Runnable接口可以轻松实现**多个线程共享相同数据**，只要用同一个实现了Runnable接口的类的对象作为参数创建多个线程就可以了
   4. 线程间的数据共享
      1. 建立Thread子类和实现Runnable接口都可以创建多线程，但**它们的主要区别:就在于对数据的共享上。**
         1. 使用Runnable接口可以轻松实现**多个线程共享相同数据**，只要用同一个实现了Runnable接口的类的对象作为参数创建多个线程就可以了。
         2. > 案例1：见例11.4、11.5
            ```java
            //11.5
            package JavaBook.chap11;

            //模拟航班售票系统，实现3个售票窗口发售某次航班的10张机票，一个售票窗口用一个线程来表示。
            //用Runnable接口程序，模拟航班售票窗口

            //每个线程都在独立地处理各自的资源
            //解决这个问题
            //3窗口共同卖10张票

            class ThreadSale extends Thread {
               //私有变量tickets代表及票数，是共享数据
               private int tickets = 10;


               public void run() {
                  while (true) {
                        //如果有票可售
                        if (tickets > 0) {
                           System.out.println(this.getName() + " sale number " + tickets-- + ".");
                        } else {
                           System.exit(0);
                        }
                  }
               }
            }

            //创建类，main中创建并启动3个线程对象
            public class App11_5 {
               public static void main(String[] args) {
                  ThreadSale t = new ThreadSale();
                  Thread t1 = new Thread(t, "first sale window");
                  Thread t2 = new Thread(t, "second sale window");
                  Thread t3 = new Thread(t, "third sale window");
                  t1.start();
                  t2.start();
                  t3.start();
               }

            }
            ```
3. 线程间的同步控制
   1. **区分***（异步与同步的区分）*
      >1. 异步执行：包含了运行时所需要的数据或方法的线程，不必关心其他线程的状态或行为，称这样的线程为**独立的、不同步的、异步执行的**。
      >2. 线程的同步：当一个线程对共享的数据进行操作时，应使之成为一个“原子操作”，即在没有完成相关操作之前，**不允许其他线程打断它**，否则就会破坏数据的完整性，必然会得到错误的处理结果，这就是**线程的同步**。（处理数据的线程，不能处理其他线程当前还没有处理结束的数据，但是可以处理其他的数据）
   2. **区分***同步与共享数据*
      1. 共享：线程之间对内存数据的共享
      2. 同步是在共享的基础上，针对多个线程共享会导致数据不一致而提出来的。
      3. 线程之间彼此不独立、需要进行同步控制
      4. 同时运行的几个线程需要共享一些数据
   3. 有时线程之间彼此不独立、需要进行同步控制。
   4. 线程间的互斥
      1. 同时运行的几个线程需要共享一个（些）数据；
      2. 一个线程对共享的数据进行操作时，不允许其他线程打断它，否则会破坏数据的完整性。即**被多个线程共享的数据，在某一时刻只允许一个线程对其进行操作**,这就需要线程同步。
      3. > 案例1：见例11.6 见例11.7 TODO:多线程模拟用户从银行取款
         >设计一个模拟用户从银行取款的应用程序。设某银行账户存款额的初值是2000元，用线程模拟两个用户分别从银行取款的情况。两个用户分4次分别从一囊的同一账户取款，每次取100元。
         >最后应该剩下2000-400-400=1200，但是**结果随机**。所以**有问题**！
         >**出现错误结果的原因**：两个并发线程共享同一内存变量所引起的；因为在线程执行过程中，在执行有关的若干个动作时，没有能够保证**独占**相关资源，而是在对该资源进行处理时又被其他线程的操作打断或干扰而引起的。
         >**解决方法**：保证线程在一个完整的操作所有动作的执行过程中，都占有相关资源而不被打断，这就是**线程同步**的概念。
   5. **“生产者/消费者” 问题**
      1. 生产者产生数据，消费者消费数据，具体来说，假设有一个Java应用程序，其中有一个线程负责往数据区写数==，另一个线程从同一数据区中读数据，两个线程可以并行执行(类似于流水线上的两道工序)；
      2. 如果数据区已满，生产者要等消费者取走一些数据后才能再放；而当数据区没有数据时，消费者要等生产者放入一些数据后再取。
   
   
   6. **这里我们先学一些概念！！!**（在并发程序设计中）
      1. **临界资源**（同步资源）：对多线程共享的资源或数据（在一个时刻只能被一个线程访问的资源）
      2. **临界代码**（临界区）：每个线程中访问临界资源的那一段代码（访问临界资源的那段代码）
      3. 临界区必须互斥地使用，即一个线程执行临界区中的代码时，其他线程不准进入临界区，直至该线程退出为止。
      4. Java语言中每个对象都有一个“互斥锁”与之相连。
      5. 为了保证互斥，Java语言使用synchronized关键字来标识同步的资源，这里的资源可以是一种类型的数据，也就是对象，也可以是一个方法，还可以是一段代码，synchronized直译为同步，但实际指的是**互斥**。
      6. **synchronized的功能**是：
         1. 首先判断对象或方法的互斥锁是否存在，若在就获得互斥锁，然后就可以执行紧随其后的临界代码段或方法体；
         2. 如果对象或方法的互斥锁不存在（已被其他线程拿走），就进入等待状态，知道获得互斥锁。（当被synchronized限定的代码段执行完，就自动释放互斥锁。）

   7. > 例:用两个线程模拟存票、售票过程:
      1. 假定开始售票处并没有票，一个线程往里存票，另外一个线程则往出卖票；
      2. 我们新建一个票类对象，让存票和售票线程都访问它。本例采用两个线程共享同一个数据对象来实现对同一份数据的操作。
   8. 在并发程序设计中，对多线程共享的资源或数据称为**临界资源或同步资源**，临界资源同一时刻只能被一个线程访问，每个线程中访问临界资源的代码称为**临界代码或临界区**，Java技术通过**互斥锁**机制实现线程间的互斥操作。
      1. 每个对象都只有一个“**互斥锁**”与之相连，利用多线程对其的争夺可实现线程间的**互斥操作**；
      2. 当线程A获得了一个对象的**锁旗标**后，线程B必须等待线程A完成规定的操作、并释放出锁旗标后，才能获得该对象的锁旗标，并执行线程B中的操作。
   9.  Java使用synchronized 关键字来标识同步的资源，这里的资源是某种类型的数据，临界区是一段代码或一个方法；

      3. 同步代码段语法：
         `synchronized（对象）{代码段}`
      4. 同步方法语法：
         `public synchronized返回值类型 方法名(){方法体}`

      > synchronized的功能是：首先判断对象的互斥锁是否在，如果在就获得互斥锁，然后就可以执行紧随其后的代码段或方法；如果对象的锁旗标不在（已被其他线程拿走），就进入等待状态，直到获得互斥锁；当被synchronized限定的代码段执行完，就释放锁旗标。

      1. > 案例1：见例11.7
         ```java
         package JavaBook.chap11;

         /*
         程序说明：
         当Consumer线程售出票后，available值变为false，当Producer线程放入票后，available值变为true；
         只有available为true时，Consumer线程才能售票，否则就必须等待Producer线程放入新的票后的通知；
         只有available为false时，Producer线程才能放票，否则必须等待Consumer线程售出票后的通知。

         //实现的是存一票卖一票
         */

         //票类
         class Tickets {
            protected int size;
            int number = 0;
            boolean available = false;

            public Tickets(int size) {
               this.size = size;
            }

            public synchronized void put() {
               if (available)
                     try {
                        //进入等待池，并释放互斥锁(锁旗标)
                        wait();
                     } catch (Exception ignored) {
                     }
               System.out.println("存入第【" + (++number) + "】号票");
               available = true;
               //唤醒另一个进程
               notify();
            }

            public synchronized void sell() {
               if (!available)
                     try {
                        //进入等待池，并释放互斥锁(锁旗标)
                        wait();
                     } catch (Exception ignored) {
                     }
               System.out.println("售出第【" + (number) + "】号票");
               available = false;
               //唤醒另一个进程
               notify();
               if (number == size) number = size + 1;
               //number>size表示售票结束
            }
         }

         //生产者类，是一个线程
         class Producer extends Thread {
            Tickets t = null;

            public Producer(Tickets t) {
               this.t = t;
            }

            public void run() {
               //while循环
               while (t.number < t.size)
                     t.put();
            }
         }

         //消费者类，是一个线程
         class Consumer extends Thread {
            Tickets t = null;

            public Consumer(Tickets t) {
               this.t = t;
            }

            public void run() {
               while (t.number <= t.size)
                     t.sell();
            }
         }

         public class App11_8 {
            public static void main(String[] args) {
               Tickets t = new Tickets(10);
               //启动两个线程
               new Producer(t).start();
               new Consumer(t).start();
            }
         }
         ```
4. 线程间的通信
   1. java.1ang.Object类的`wait()`、`notify()`、`notifyAll()`等方法为线程间的通信提供了有效手段。
   2. `wait()`:如果当前状态不适合本线程执行，正在执行同步代码（synchronized）的某个线程A调用`wait()`方法（在对象x上），该线程暂停执行而进入对象x的等待池，并释放已获得的对象x的互斥锁(锁旗标)。线程A要一直等到其他线程在对象x上调用`notify()`或`notifyAll()`方法，才能够在重新获得对象x的互斥锁后继续执行（从`wait()`语句后继续执行）。
   3. `notify()`:唤醒等待池中的第一个线程，本线程继续执行，线程被唤醒以后获得互斥对象的互斥锁，并进入就绪状态等待调度。
   4. `notifyAll()`:唤醒等待池中的所有线程，优先级最高的线程最先被调度执行。
   5. > 案例1：见例11.8（完善存票售票）
      ```java
      /*
      程序说明：
      当Consumer线程售出票后，available值变为false，当Producer线程放入票后，available值变为true；
      只有available为true时，Consumer线程才能售票，否则就必须等待Producer线程放入新的票后的通知；
      只有available为false时，Producer线程才能放票，否则必须等待Consumer线程售出票后的通知。
      */
      public class App11_8 {
         public static void main(String[] args) {
             Tickets t = new Tickets(10);
             new Producer(t).start();
             new Consumer(t).start();
         }
      }

      class Tickets {
         protected int size;
         int number = 0;
         boolean available = false;

         public Tickets(int size) {
             this.size = size;
         }

         public synchronized void put() {
             if (available)
                 try {
                     wait();
                 } catch (Exception e) {
                 }
             System.out.println("存入第【" + (++number) + "】号票");
             available = true;
             notify();
         }

         public synchronized void sell() {
             if (!available)
                 try {
                     wait();
                 } catch (Exception e) {
                 }
             System.out.println("售出第【" + (number) + "】号票");
             available = false;
             notify();
             if (number == size) number = size + 1;
             //number>size表示售票结束
         }
      }

      class Producer extends Thread {
         Tickets t = null;

         public Producer(Tickets t) {
             this.t = t;
         }

         public void run() {
             while (t.number < t.size)
                 t.put();
         }
      }

      class Consumer extends Thread {
         Tickets t = null;

         public Consumer(Tickets t) {
             this.t = t;
         }

         public void run() {
             while (t.number <= t.size)
                 t.sell();
         }
      }

      ```
   6. > TODO:multiThreadingBankRefined
      ```java

      package JavaBook.chap11;

      import java.util.Random;

      //银行账户类
      class Account {
         String name;
         double balance;

         //构造方法
         public Account(String name) {
            this.name = name;
            this.balance = 0;
         }

      }

      //多线程
      class SaveThread extends Thread {
         private Account account;
         private double value;

         //传入一个account类、一个double值
         public SaveThread(Account account) {
            this.account = account;
         }

         public void run() {

            for (int i = 0; i < 5; i++) {
                  synchronized (account) {

                     //产生5个500~1000的随机整数
                     Random random = new Random();
                     this.value = random.nextInt(1000) + 500;
                     System.out.println("valueInPut:" + this.value);

                     //存款
                     if (value > 0) {
                        account.balance += value;
                     }
                     System.out.println("您的存款金额为" + value + " ; " + "存款成功,您的余额为" + account.balance);

                  }
                  try {
                     Thread.sleep(1);
                  } catch (InterruptedException ignored) {
                  }

            }
         }

      }

      //主线程
      class FetchThread extends Thread {

         private Account account;

         //传入一个account类、一个double值
         public FetchThread(Account account) {
            this.account = account;
         }

         public void run() {

            for (int i = 0; i < 5; i++) {
                  synchronized (account) {

                     //产生5个500~1000的随机整数
                     Random random = new Random();
                     double value = random.nextInt(1000) + 500;
                     System.out.println("valueOutPut:" + value);

                     //取款
                     //如果取钱金额<=存款金额,取出来，并把存款金额减去取钱金额
                     if (account.balance > 0) {
                        //如果要取负数,取不到钱
                        if (value <= 0) {

                              System.out.println("您的取款金额是负数，无法取款负数的金额！" + "您的余额为" + account.balance);

                        } else if (value <= account.balance) {

                              account.balance -= value;
                              System.out.println("您的取款金额为" + value + " ; " + "取款成功,您的余额为" + account.balance);

                        } else {

                              //如果取钱金额>存款金额,就把剩余的钱全都取出来，并把存款清零
                              value = account.balance;
                              account.balance = 0;
                              System.out.println("您的取款金额是" + value + "<=存款金额，所以会把存款金额全部取出来 ; " + "取款成功,您的余额为" + account.balance);

                        }
                     } else {

                        System.out.println("您的余额是0，无法取款~");

                     }

                  }
                  try {
                     Thread.sleep(1);
                  } catch (InterruptedException ignored) {
                  }

            }
         }
      }


      public class multiThreadingBankRefined {
         public static void main(String[] args) {
            Account Tony = new Account("Tony");
            (new FetchThread(Tony)).start();

            //两个线程，一个是存款线程（存款5次）、一个是取款线程（取款5次）
            (new SaveThread(Tony)).start();


         }
      }
      ```
5. 后台线程
   1. 也叫守护线程，通常是为了辅助其它线程而运行的线程；
   2. 它不妨碍程序终止；
   3. 一个进程中只要还有一个前台线程在运行，这个进程就不会结束；如果一个进程中的所有前台线程都已经结束，那么无论是否还有未结束的后台线程，这个进程都会结束；
   4. “垃圾回收”便是一个后台线程；
   5. 如果对某个线程对象在启动（调用start方法）之前调用了`setDaemon(true)`方法，这个线程就变成了后台线程。
6. 死锁
   1. 线程在运行过程中，其中某个步骤往往需要满足一些条件才能继续进行下去，如果这个条件不能满足，线程将在这个步骤上出现阻塞；
   2. 线程A可能会陷于对线程B的等待，而线程B同样陷于对线程C的等待，依次类推，整个等待链最后又可能回到线程A。如此一来便陷入一个彼此等待的轮回中，任何线程都动弹不得，此即所谓死锁（deadlock）；
   3. 对于死锁问题，关键不在于出现问题后调试，而是在于预防。
   4. > 案例1：拿球游戏（todo:及其优化）
      ```java

      ```
7. 控制线程的生命
   1. 结束线程的生命
      1. 用stop方法可以结束线程的生命，但如果一个线程正在操作共享数据段，操作过程没有完成就用stop结束的话，将会导致数据的不完整，因此并不提倡使用此方法；
      2. 通常，可通过控制run方法中循环条件的方式来结束一个线程。
   2. > 例:线程不断显示递增整数，按下回车键则停止执行。
      >

      ```java
      import java.io.*;

      public class App11_11 {
         public static void main(String[] args) throws IOException {
             TestThread t = new TestThread();
             t.start();
             new BufferedReader(new InputStreamReader(System.in)).readLine();
             t.stopme();   //调用stopme方法结束t线程
         }
      }

      class TestThread extends Thread {
         private boolean flag = true;

         public void stopme() { //在此方法中控制循环条件
             flag = false;
         }

         public void run() {
             int i = 0;
             while (flag) {
                 System.out.println(i++);//如果flag为真则一直显示递增整数
             }
         }
      }

      ```
