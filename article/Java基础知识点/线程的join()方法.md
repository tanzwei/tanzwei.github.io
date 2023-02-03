#### 概述：
等待相应线程运行结束。若线程A调用线程B的join方法，那么线程A将会暂停运行，直到线程B运行结束。(谁join进来就等谁先运行完)join实际上是通过wait来实现的。下面实例中t2线程需要等待线程t1执行完成后再执行使用场景，线程2依赖于线程1执行的返回结果。
在线程2中调用线程1的join方法，当线程调用了这个方法，线程1会强占CPU资源，知道线程执行结束为止。（谁调用join方法，谁就能强占cpu资源，直至执行结束）
这里说的是强占，而不是抢占，也就是说这个线程调用了join方法后，线程抢占到CPU资源，它就不会再释放，知道线程执行完毕。
```
    public static void main(String[] args) throws Exception{
      Thread t1 =  new Thread(()->{
          try {
              Thread.sleep(500);
              System.out.println("线程1醒了");
          } catch (InterruptedException e) {
              e.printStackTrace();
          }
            for(int i=0;i<100;i++){
                System.out.println("线程1 i:"+i);
 
            }
      });
      t1.setName("线程1");
 
      Thread t2 = new Thread(()->{
          try {
              t1.join();
          } catch (InterruptedException e) {
              e.printStackTrace();
          }
         for(int i=0;i<100;i++){
             System.out.println("线程2 i:"+i);
             try {
                 Thread.sleep(100);
             } catch (InterruptedException e) {
                 e.printStackTrace();
             }
         }
      });
      t2.setName("线程2");
 
        t2.start();
        t1.start();
 
    }
```
输出结果：
```
线程1醒了
线程1 i:0
线程1 i:1
线程1 i:2
线程1 i:3
线程1 i:4
线程1 i:5
……
线程1 i:99
线程2 i:0
线程2 i:1
线程2 i:2
线程2 i:3
线程2 i:4
……
线程2 i:99
```
