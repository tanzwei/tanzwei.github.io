## 一、概述
#### 1、什么是进程？
进程是指一个内存中运行的应用程序，每一个进程都有一个独立的内存空间。
#### 2、什么是线程？
线程是指进程中的一个执行流程，一个进程中可以运行多个线程。比如java.exe进程中可以运行很多线程，线程属于某个进程，线程没有自己的虚拟地址空间，与进程内的其它线程一起共享分配给该进程的所有资源。
对Java程序来说，当Dos命令窗口中输入：java HelloWorld  回车之后，会先启动JVM，而JVM就是一个进程。JVM再启动一个主线程main方法，同时再启动一个垃圾回收线程负责看护，回收垃圾。最起码，现在的Java程序中至少有两个线程并发：一个是垃圾回收线程，一个是执行main方法的主线程。
线程不能独立执行，必须依存在应用程序中，由应用程序提供多个线程执行控制。
#### 3、线程和进程是什么关系？
进程可以看作是现实生活中的公司，线程可以看作是公司当中的某个员工。
注意：进程A和进程B的内存独立不共享。线程A和线程B之间，堆内存和方法区之间内存共享；但是栈内存独立，一个线程一个栈。
![一个线程一个栈.jpg](../../image/img/Java%E4%B8%AD%E7%9A%84%E7%BA%BF%E7%A8%8B/1666166844131-e4bd0be1-9048-4d78-b983-5c41d4192ccd.jpeg)

#### 4、简单说下多线程并发
假设启动10个线程，会有10个栈空间，每个栈和每个栈之间互不干扰，各自执行各自的，这就是多线程并发。
例子：火车站可以看作是一个进程。火车站中的每一个售票窗口可以看作是一个线程。我在窗口1购票，你在窗口2购票，你不需要等我，我也不需要等你，所有多线程并发可以提高效率。
Java中之所以有多线程机制，目的就是为了提高程序的处理效率。
#### 5、一个线程包含以下内容：

   - 一个指向当前被执行指令的指令指针;
   - 一个栈;
   - 一个寄存器值的集合，定义了一部分描述正在执行线程的处理器状态的值;
   - 一个私有的数据区。
#### 6、关于线程的生命周期

   1. 新建状态
   2. 就绪状态
   3. 运行状态
   4. 阻塞状态
   5. 死亡状态

![线程的生命周期.jpg](../../image/img/Java%E4%B8%AD%E7%9A%84%E7%BA%BF%E7%A8%8B/1666185795180-1f6cc1c1-6413-4b9f-a528-ea65c02acefc.jpeg)
## 二、线程的创建
#### 1、编写一个类，继承java.lang.Thread，重写run方法
```java
public class ThreadTest01 {
    public static void main(String[] args) {
        //这里是main方法，这里的代码属于主线程，在主栈中运行。
        //新建一个分支线程对象。
        MyThread myThread = new MyThread();
        //启动多线程
        //start()方法的作用是：启动一个分支线程，在JVM中开辟一个新的栈空间，这段代码任务完成后，瞬间就结束了。
        //这段代码的任务只是为了开启一个新的栈空间，只要新的栈空间开辟出来了，start()方法就结束了。线程就启动成功了。
        //启动成功的线程会自动调用run方法，并且run方法在分支栈的栈底部（压栈）。
        //run方法在分支栈的栈底部，main方法在主栈的栈底部。run和main是平级的。
        myThread.start();
        //这里的代码还是在主线程中。
        for(int i = 0; i < 100; i++){
            System.out.println("主线程--->" + i);
        }
    }
}
class MyThread extends Thread{
    @Override
    public void run() {
        //编写程序，这段程序运行在分支线程中（分支栈）。
        for(int i = 0; i < 100; i++){
            System.out.println("分支线程--->" + i);
        }
    }
}
```
#### 2、编写一个类，实现java.lang.Runnable接口
```java
public class ThreadTest02 {
    public static void main(String[] args) {
        //创建一个可运行的对象
        MyRunnable r = new MyRunnable();
        //将可运行的对象封装成一个线程对象
        Thread t = new Thread(r);
        //Thread t = new Thread(new MyRunnable()); 合并代码
        //启动线程
        t.start();
        for(int i = 0; i < 100; i++){
            System.out.println("主线程--->" + i);
        }
    }
}

//这并不是一个线程类，是一个可运行的类。它还不是一个线程。
class MyRunnable implements Runnable{
    @Override
    public void run() {
        for(int i = 0; i < 100; i++){
            System.out.println("分支线程--->" + i);
        }
    }
}
```
#### 2.1、使用匿名内部类编写

```java
public class ThreadTest03 {
    public static void main(String[] args) {
        //采用匿名内部类编写
        Thread t = new Thread(new Runnable() {
            @Override
            public void run() {
                for(int i = 0; i < 100; i++){
                    System.out.println("分支线程--->" + i);
                }
            }
        });
        //启动线程
        t.start();
        for(int i = 0; i < 100; i++){
            System.out.println("主线程--->" + i);
        }
    }
}
```
#### 3、使用Callable接口创建线程
```java
/*
线程执行的第三种方式：
    实现Callable接口
    这种方式的优点：可以获取到线程的执行结果
    这种方式的缺点：效率较低，在获取t线程执行结果的时候，当前线程受阻塞，效率较低。
 */
public class ThreadTest08 {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        //第一步：创建一个“未来任务类”对象。
        //参数非常重要，需要给一个Callable接口实现类对象。
        FutureTask task = new FutureTask(new Callable() {
            @Override
            //call()方法就相当于run()方法。只不过call()方法有返回值。
            //线程执行一个任务，执行之后可能会有一个执行结果
            public Object call() throws Exception {
                System.out.println("FutureTask begin!");
                Thread.sleep(1000 * 5);
                System.out.println("FutureTask end!");
                int a = 100;
                int b = 200;
                return a + b;  //自动装箱，结果变成Integer
            }
        });

        //创建线程对象
        Thread t = new Thread(task);
        t.start();

        //获取线程t的返回结果
        //get()方法的执行会导致“当前线程阻塞”
        Object obj = task.get();

        //main方法在这里的程序想要执行必须等待get()方法结束
        //而get()方法可能需要很久，因为get()方法是为了拿到另一个线程
        //的执行结果，而另一个线程执行是需要时间的。
        System.out.println("Hello World");
    }
}
```
## 三、线程的常用方法

| **常用方法** | **作用** |
| --- | --- |
| setName(String str) | 设置线程名称 |
| setPriority(int i) | 设置线程优先级（1~10），数字越大优先级越高 |
| getName() | 获取线程名，主线程名默认main，自定义线程名默认Thread-N |
| getPriority() | 获取线程优先级 |
| getState() | 获取线程状态 |
| **start()** | 启动线程 |
| **run()** | 线程启动后执行的方法 |
| **Thread.currentThread()** | 获取当前运行的线程对象 |
| Thread.sleep(long m) | 设置当前线程休眠m毫秒 |
| Thread.yield() | 线程让步，让其它线程执行 |
| setDaemon(boolean f) | 是否将该线程设置为守护线程 |
| isDaemon() | 判断该线程是否属于守护线程 |

#### 1、关于线程的sleep方法
```java
/*
关于线程的sleep方法：
    static void sleep(long millis)
    1、静态方法：Thread.sleep(1000);
    2、参数是毫秒
    3、作用：让当前线程进入休眠，进入“阻塞状态”，放弃占有CPU时间片，让给其它线程使用。
          这行代码出现在A线程中，A线程就会进入休眠。
          这行代码出现在B线程中，B线程就会进入休眠。
    4、Thread.sleep()方法，可以做到这种效果：
           间隔特定的时间，去执行一段特定的代码，每隔多久执行一次。

    5、InterruptedException：中断异常
 */
public class ThreadTest05 {
    public static void main(String[] args) {
        /*for(int i = 0; i < 10; i++) {
            System.out.println(Thread.currentThread().getName() + "--->" + i);
            try {
                //间隔一秒输出
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }*/

        Thread t = new Thread(new MyThread4());
        t.setName("t");
        t.start();

        //希望5秒之后，t线程醒来（5秒后主线程手里的活儿干完了）
        try {
            Thread.sleep(1000*5);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        //终止t线程的睡眠（这种睡眠的方式依靠了java的异常处理机制。）
        t.interrupt();
    }
}
class MyThread4 implements Runnable{
    @Override
    public void run() {
        //重点；run()当中的异常不能throws，只能try catch
        //因为run()方法在父类中没有抛出任何异常，子类不能比父类抛出更多或更广泛的异常。
        System.out.println(Thread.currentThread().getName() + "--->begin");
        try {
            //休眠1分钟
            Thread.sleep(1000*60);
        } catch (InterruptedException e) {
            //e.printStackTrace();  //如果不想显示异常信息可以注释掉
        }
        //1分钟后才能执行到这里
        System.out.println(Thread.currentThread().getName() + "--->end");
    }
}
```
#### 2、关于Thread.sleep()方法的一个面试题：
```java
public class ThreadTest06 {
    public static void main(String[] args) {
        Thread t = new MyThread3();
        t.setName("MyThread");
        t.start();

        //调用sleep()方法
        try {
            //延迟5秒后执行
            //问题：这行代码会让t线程进入休眠状态吗？
            t.sleep(1000 * 5);  //在执行的时候还是会转换成：Thread.sleep(1000*5);
                                  //这行代码的作用是：让当前线程进入休眠状态，也就是说main线程进入休眠。
                                  //这样的代码出现在main方法中，main线程睡眠。
            //sleep的作用是让当前线程进入睡眠状态，即出现在哪个线程里则让哪个线程进入睡眠状态，和对象调用无关。
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        //5秒后这里才会执行
        System.out.println("Hello World");
    }
}
class MyThread3 extends Thread{
    @Override
    public void run() {
        for(int i = 0; i < 100; i++){
            System.out.println(Thread.currentThread().getName() + "--->" + i);
        }
    }
}
```

#### 3、使用指定器指定任务

```java
public class TimerTest {
    public static void main(String[] args) throws ParseException {
        //创建定时器对象
        Timer timer = new Timer();
        //Timer timer = new Timer(true);  守护线程

        //指定定时任务
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        Date firstTime = sdf.parse("2022-4-9 11:48:00");
//        timer.schedule(定时任务，第一次执行时间，间隔多久执行一次)；
        timer.schedule(new LogTimerTask(),firstTime,1000 * 5); //也可以使用匿名内部类的方式编写
    }
}
//因为定时任务是一个抽象类，不能new
//编写一个定时任务类
//假设这是一个记录日志的定时任务
class LogTimerTask extends TimerTask{
    @Override
    public void run() {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String strTime = sdf.format(new Date());
        System.out.println(strTime + "完成了一次备份");
    }
}
```
## 四、关于线程安全问题

#### 1、什么时候数据在多线程并发的环境下会存在问题？

   1. 多线程并发
   2. 有共享数据
   3. 共享数据有修改行为

满足以上三个条件之后，就会存在线程安全问题
#### 2、怎么解决线程安全问题？
线程排队执行（不能并发）；
用排队执行解决线程安全问题，这种机制被称为：线程同步机制。（线程同步就是线程排队了，线程排队会牺牲一部分效率）
#### 3、两个专业术语
异步编程模型：
线程t1和线程t2，各自执行各自的，t1不管t2，t2不管t1，谁也不需要等谁，这种编程模型叫做：异步编程模型。（其实就是：多线程并发 --> 效率高）
同步编程模型：
线程t1和线程t2，在线程t1执行的时候，必须等待t2线程执行结束，或者说在t2线程执行的时候，必须等待t1线程执行结束，两个线程之间发生了等待关系，这就是同步编程模型。（效率较低，线程排队执行 --> 同步就是排队）
#### 4、Java中有三大变量
**实例变量**：在堆中；
**静态变量**：在方法区；
**局部变量**：在栈中。
**4.1、**以上三大变量中，局部变量永远都不会存在线程安全问题，因为局部变量不会共享（一个线程一个栈），局部变量在栈中，所以局部变量永远不会共享。
**4.2、**实例变量在堆中，堆只有一个；静态变量在方法区中，方法区只有一个。堆和方法区都是多线程共享的，所以可能存在线程安全问题。
#### 5、线程安全实现代码案例
```java
public class Account {
    //账号
    private String account;
    //余额
    private double balance;

    public Account(){

    }
    public Account(String account, double balance) {
        this.account = account;
        this.balance = balance;
    }

    public String getAccount() {
        return account;
    }

    public void setAccount(String account) {
        this.account = account;
    }

    public double getBalance() {
        return balance;
    }

    public void setBalance(double balance) {
        this.balance = balance;
    }
    //取款的方法
    public void withdraw(double money){
        //以下这几行代码必须是线程排队的，不能并发。
        //一个线程把这里的代码全部执行结束后，另一个线程才能进来。

        /*
        线程同步机制的语法是：
            synchronized(){
            //线程同步代码块。
            }
        synchronized后面小括号中传的这个“数据”是相当关键的。
        这个数据必须是多线程共享的数据，才能达到多线程排队。

        ()中写什么？
            那要看你想让哪些线程同步。
            假设t1、t2、t3、t4、t5，有5个线程。
            你只希望t1、t2、t3排队，t4、t5不需要排队，怎么办？
            你一定要在()中写一个t1、t2、t3共享的对象。而这个
            对象对于t4、t5来说不是共享的。

            里面可以填写this，也可以填写实例变量，也可以填写字符串。

            注意：不可以填写局部变量，因为局部变量别的引用调用的时候，会重新new对象(一个线程一个栈)，而实例变量只有一个。
                 写字符串的时候也行，因为你所写的字符串是保存在字符串常量池的，也是唯一的，但是你写字符串
                 就相当于所有线程都要排队，都是共享的。
         */
        //这里的共享对象是：账户对象
        //不一定是this，这里只要是多线程共享的那个对象就行。
        /*
        在Java语言中，任何一个对象都有“一把锁”，其实这把锁就是标记。（只是把它叫做锁）
        100个对象，100把锁。1个对象1把锁。
         */

        /*
        以下代码执行原理？
            synchronized就相当于一把锁，谁先执行到synchronized，这就先打开锁，等将synchronized内的代码执行完毕后，
            才会开锁，其它的线程此时才可以继续执行，然后重复上个过程，直到线程执行完毕。
            这样就达到了线程排队执行。
         */
        synchronized (this){
            /*synchronized ("abc") {
            }*/
            //取款之前的余额
            double before = this.getBalance();
            //取款之后的余额
            double after = before - money;
            //更新余额
            this.setBalance(after);
        }
    }
}
```
```java
public class AccountThread extends Thread{
    //两个线程必须共享同一个账户对象。
    private Account act;

    //通过构造方法传递过来账户对象
    public AccountThread(Account act){
        this.act = act;
    }

    public void run(){
        //run()方法表示取款的操作
        //假设取款5000
        double money = 5000;
        //取款
        act.withdraw(money);
        System.out.println(Thread.currentThread().getName() + "对帐户" + act.getAccount() + "取款成功，余额" + act.getBalance());
    }
}
```
```java
public class Demo {
    public static void main(String[] args){
        //创建账户对象
        Account act = new Account("act-001",10000);
        //创建两个线程
        Thread t1 = new AccountThread(act);
        Thread t2 = new AccountThread(act);
        //Thread t3 = new AccountThread(a);  --->这个t3与t1、t2不共享，所以只有t1、t2排队执行。
        //设置name
        t1.setName("t1");
        t2.setName("t2");
        //启动线程取款
        t1.start();
        t2.start();
    }
}
```

**5.1、关于synchronized**
	synchronized 可以出现在实例方法上（public synchronized void withdraw(double money){}），一定锁的是this。所以这种方式不灵活。
另外还有一个缺点：synchronized出现在实例方法上，表示整个方法体都需要同步，可能会无故扩大同步的范围，导致程序的执行效率降低，所以这种方式不常用。
synchronized使用在实例方法上有什么优点？
		代码写的少了，节俭了。
	如果共享的对象是this，并且需要同步的代码块就是整个方法体，建议使用这种方式。
**5.2、如果使用局部变量的话，建议使用 StringBuilder，StringBuffer效率较低。**
```
ArrayList是非线程安全的。
Vector是线程安全的。
HashMap HashSet是非线程安全的。
Hashtable是线程安全的。
```
**5.3、总结**
```
 第一种：同步代码块
    灵活
    synchronized(线程共享对象){
    同步代码块；
    }
  
 第二种：在实例方法上使用synchronized
 	表示共享对象一定是this
	并且同步代码块是整个方法体。

 第三种：在静态方法上使用synchronized
 	表示找类锁。
	类锁永远只有1把。
	就算创建了100个对象，那类锁也只有一把。

对象锁：1个对象1把锁，100个对象100把锁。
类锁:100个对象，也可能只是1把类锁。
```
**5.4、以后开发中怎么解决线程安全问题？**
不建议一上来就使用synchronized，因为synchronized会让程序的执行效率降低，用户体验不好。
系统的用户吞吐量降低，用户体验差。在不得已的情况下再选择线程同步机制。

   1. 第一种方案：尽量使用局部变量代替“实例变量和静态变量”。
   2. 第二种方案：如果必须是实例变量，那么可以考虑创建多个对象，这样实例变量的内存就不会共享了（一个线程对应一个对象，100个线程对应100个对象，对象不共享，就没有数据安全问题了。）
   3. 第三种方案：如果不能使用局部变量，对象也不能创建多个，这个时候就只能选择synchronized。线程同步机制。
#### 6、守护线程
**6.1、**Java语言中线程分为两大类：

      1. 一类是：用户线程
      2. 一类是：守护线程（后台线程）

其中具有代表性的就是：垃圾回收机制（守护线程）
**6.2、**守护线程的特点：
一般守护线程是一个死循环，所有的用户线程只要结束，守护线程自动结束。
**6.3、**注意

      1. 主线程main是一个用户线程；
      2. setDaemon(true) 必须再 start() 之前设置，否则就会抛出lllegalThreadStateException异常，该线程仍默认为用户线程，继续执行；
      3. 守护线程创建的线程也是守护线程；
      4. 守护线程不应该访问、写入持久化资源，如文件、数据库，因为它会在任何时间被停止，导致资源未被释放、数据写入中断等问题。

**6.4、**守护线程用在什么地方呢？
可以用在数据备份中：每天00：00的时候系统数据自动备份，这个时候需要使用到定时器，并且我们可以将定时器设置为守护线程，一直在那里看着，每到00：00的时候就备份一次。所有的用户线程如果结束了，守护线程自动退出，没有必要进行数据备份了。
```java
public class Test {
    public static void main(String[] args) {

      	//定时器
				//Timer timer = new Timer();

        Thread t = new BakDataThread();
        t.setName("备份数据的线程");

        //启动线程之前，将线程设置为守护线程
        t.setDaemon(true);

        t.start();

        //主线程：主线程是用户线程
        for(int i = 0; i < 10; i++){
            System.out.println(Thread.currentThread().getName() + "--->" + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
class BakDataThread extends Thread{
    public void run(){
        int i = 0;
        //即使是死循环，但由于该线程是守护者，当用户线程结束，守护线程自动终止。
        while(true){
            System.out.println(Thread.currentThread().getName() + "--->" + (++i));
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```
#### 7、关于Object类中的wait和notify方法（方法和消费者模式）

   - wait 和 notify 方法不是线程对象的方法，是Java中任何一个Java对象都有的方法，因为两个方法是Object 类中自带的。
   - wait () 方法的作用？
```java
Object o = new Object();
o.wait();

/*
	表示让正在对象o上活动的线程进入等待状态，无限期等待，直到被唤醒为止；
	o.wait() 方法的调用，会让“当前线程”进入等待状态
*/
```

   - notify () 方法的作用？
```java
Object o = new Object();
o.notify();

/*
	表示唤醒正在对象o上等待的线程；
	还有一个notifyAll() 方法，这个方法是唤醒对象o上处于等待状态的所有线程。
*/
```
#### 8、关于线程死锁的例子
```java
/*
线程死锁
    死锁很难调试，永远不会结束。
 */
public class DeadLock {
    public static void main(String[] args){
        Object o1 = new Object();
        Object o2 = new Object();

        //t1和t2两个线程共享o1,o2
        Thread t1 = new MyThread1(o1,o2);
        Thread t2 = new MyThread2(o1,o2);

        t1.setName("t1");
        t2.setName("t2");

        t1.start();
        t2.start();
    }
}
//如果没有睡眠，可能t1直接把o1和o2执行结束，就不会发生死锁，但是如果让t1、t2睡眠，就一定会发生死锁。
//所以synchronized在开发中最好不要嵌套使用。
class MyThread1 extends Thread{
    Object o1;
    Object o2;
    public MyThread1(Object o1 , Object o2){
        this.o1 = o1;
        this.o2 = o2;
    }
    public void run(){
        synchronized (o1){
            try {
                //睡眠必然会造成线程死锁
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (o2){

            }
        }
    }
}

class MyThread2 extends Thread{
    Object o1;
    Object o2;
    public MyThread2(Object o1 , Object o2){
        this.o1 = o1;
        this.o2 = o2;
    }
    public void run(){
        synchronized (o2){
            try {
                //睡眠必然会造成线程死锁
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (o1){

            }
        }
    }
}
```
