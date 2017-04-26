














# java的多线程机制
## 1.什么是线程，线程与进程的关系
- 线程是依附于进程的，**进程是分配资源的最小单位，一个进程可以生成多个线程，这些线程拥有共享的进程资源**。就每个线程而言，只有很少的独有资源，如控制线程运行的线程控制块，保留局部变量和少数参数的栈空间等。线程有就绪、阻塞和运行三种状态，并可以在这之间切换。也正因为多个线程会共享进程资源，所以当它们对同一个共享变量/对象进行操作的时候，线程的冲突和不一致性就产生了
- 线程与进程的区别
    - 　进程：每个进程都有独立的代码和数据空间（进程上下文），进程间的切换会有较大的开销    ，一个进程包含1--n个线程。
     
    - 线程：同一类线程共享代码和数据空间，每个线程有独立的运行栈和程序计数器(PC)，线程切    换开销小

## 2.java线程实现的接口与继承的类
- 使用多线程需要实现Runnable接口、继承Thread类、使用ExecutorService、Callable、Future实现有返回结果的多线程
## 3.创建线程的方式
- Java提供了线程类Thread来创建多线程的程序。其实，创建线程与创建普通的类的对象的操作是一样的，而线程就是Thread类或其子类的实例对象。每个Thread对象描述了一个单独的线程。要产生一个线程，有两种方法：
 
    - 需要从Java.lang.Thread类派生一个新的线程类，重载它的run()方法； 

    - 实现Runnalbe接口，重载Runnalbe接口中的run()方法。
    - 总之就是需要重载继承或实现类内的run()方法;
    
    - 方法也可以实现需要的要求，为什么要用到多线程这个概念
        -
        - 在某些情况下，我们希望程序可以在执行某项任务的同时执行另外一些无需或很少人工干预的任务，这个时候我们就会在程序中采用多线程的方式执行该任务，以最大限度的利用CPU资源，从而在更短时间内完成程序。
    - 使用Thread类来创建线程的代码：

```
public class MutliThreadDemo {

    public static void main(String [] args){
    
        //实例化对象
        MutliThread m1=new MutliThread("Window 1");

        MutliThread m2=new MutliThread("Window 2");

        MutliThread m3=new MutliThread("Window 3");
        
        //让三个进程同时运行
        m1.start();

        m2.start();

        m3.start();

        }
    
    }
    //内部类继承了Thread类覆写了父类内的方法
    class MutliThread extends Thread{

    private int ticket=100;//每个线程都拥有100个数字

    public MutliThread(String name){

        super(name);//调用父类带参数的构造方法

    }

    public void run(){

        while(ticket>0){

            System.out.println(ticket--+" is saled by "+Thread.currentThread().getName());

        }

    }

    }
```
- 实现Runnable接口来创建多线程
    - 
    - 代码：
```
    

public class MutliThreadDemo2 {

    public static void main(String [] args){

        MutliThread m1=new MutliThread("Window 1");

        MutliThread m2=new MutliThread("Window 2");

        MutliThread m3=new MutliThread("Window 3");

        Thread t1=new Thread(m1);

        Thread t2=new Thread(m2);

        Thread t3=new Thread(m3);

        t1.start();

        t2.start();

        t3.start();

    }

}

class MutliThread implements Runnable{

    private int ticket=100;//每个线程都拥有100个数字

    private String name;

    MutliThread(String name){

        this.name=name;

    }

    public void run(){

        while(ticket>0){

            System.out.println(ticket--+" is saled by "+name);

        }

    }

} 
```

    

## 4.线程如何使用
- 线程使用的方法
    -
    - run()：
        如果该线程是使用独立的 Runnable 运行对象构造的，则调用该 Runnable 对象的 run 方法；否则，该方法不执行任何操作并返回
    - start()： 
          使该线程开始执行；Java 虚拟机调用该线程的 run 方法。 
    - join()：
          等待该线程终止。
    - isAlive()：
          测试线程是否处于活动状态
    - sleep(long millis)：
          在指定的毫秒数内让当前正在执行的线程休眠（暂停执行），此操作受到系统计时器和调度程序精度和准确性的影响 
## 5.线程的生命周期
- a.什么叫线程的生命周期
    - 线程是一个动态执行的过程，他也有一个从产生到死亡的过程
- b.线程生命周期的五种状态
    - 新建（new Thread）
    当创建Thread类的一个实例（对象）时，此线程进入新建状态（未被启动）。
    例如：Thread  t1=new Thread();
    
    就绪（runnable）
    线程已经被启动，正在等待被分配给CPU时间片，也就是说此时线程正在就绪队列中排队等候得到CPU资源。例如：t1.start();
    
    运行（running）
    线程获得CPU资源正在执行任务（run()方法），此时除非此线程自动放弃CPU资源或者有优先级更高的线程进入，线程将一直运行到结束。
    
    死亡（dead）
    当线程执行完毕或被其它线程杀死，线程就进入死亡状态，这时线程不可能再进入就绪状态等待执行。
    
    自然终止：正常运行run()方法后终止
    
    异常终止：调用stop()方法让一个线程终止运行
    
    堵塞（blocked）
    由于某种原因导致正在运行的线程让出CPU并暂停自己的执行，即进入堵塞状态。
    
    正在睡眠：用sleep(long t) 方法可使线程进入睡眠方式。一个睡眠着的线程在指定的时间过去可进入就绪状态。
    
    正在等待：调用wait()方法。（调用motify()方法回到就绪状态）
    
    被另一个线程所阻塞：调用suspend()方法。（调用resume()方法恢复）
## 6.线程同步
- 我们可以在计算机上运行各种计算机软件程序。每一个运行的程序可能包括多个独立运行的线程（Thread）。 
线程（Thread）是一份独立运行的程序，有自己专用的运行栈。线程有可能和其他线程共享一些资源，比如，内存，文件，数据库等。 
当多个线程同时读写同一份共享资源的时候，可能会引起冲突。这时候，我们需要引入线程“同步”机制，即各位线程之间要有个先来后到，不能一窝蜂挤上去抢作一团。 
同步这个词是从英文synchronize（使同时发生）翻译过来的。我也不明白为什么要用这个很容易引起误解的词。既然大家都这么用，咱们也就只好这么将就。 
线程同步的真实意思和字面意思恰好相反。线程同步的真实意思，其实是“排队”：几个线程之间要排队，一个一个对共享资源进行操作，而不是同时进行操作。

因此，关于线程同步，需要牢牢记住的第一点是：线程同步就是线程排队。同步就是排队。线程同步的目的就是避免线程“同步”执行。这可真是个无聊的绕口令。 
关于线程同步，需要牢牢记住的第二点是 “共享”这两个字。只有共享资源的读写访问才需要同步。如果不是共享资源，那么就根本没有同步的必要。 
关于线程同步，需要牢牢记住的第三点是，只有“变量”才需要同步访问。如果共享的资源是固定不变的，那么就相当于“常量”，线程同时读取常量也不需要同步。至少一个线程修改共享资源，这样的情况下，线程之间就需要同步。 
关于线程同步，需要牢牢记住的第四点是：多个线程访问共享资源的代码有可能是同一份代码，也有可能是不同的代码；无论是否执行同一份代码，只要这些线程的代码访问同一份可变的共享资源，这些线程之间就需要同步。

为了加深理解，下面举几个例子。 
有两个采购员，他们的工作内容是相同的，都是遵循如下的步骤： 
（1）到市场上去，寻找并购买有潜力的样品。 
（2）回到公司，写报告。 
这两个人的工作内容虽然一样，他们都需要购买样品，他们可能买到同样种类的样品，但是他们绝对不会购买到同一件样品，他们之间没有任何共享资源。所以，他们可以各自进行自己的工作，互不干扰。 
这两个采购员就相当于两个线程；两个采购员遵循相同的工作步骤，相当于这两个线程执行同一段代码。

下面给这两个采购员增加一个工作步骤。采购员需要根据公司的“布告栏”上面公布的信息，安排自己的工作计划。 
这两个采购员有可能同时走到布告栏的前面，同时观看布告栏上的信息。这一点问题都没有。因为布告栏是只读的，这两个采购员谁都不会去修改布告栏上写的信息。

下面增加一个角色。一个办公室行政人员这个时候，也走到了布告栏前面，准备修改布告栏上的信息。 
如果行政人员先到达布告栏，并且正在修改布告栏的内容。两个采购员这个时候，恰好也到了。这两个采购员就必须等待行政人员完成修改之后，才能观看修改后的信息。 
如果行政人员到达的时候，两个采购员已经在观看布告栏了。那么行政人员需要等待两个采购员把当前信息记录下来之后，才能够写上新的信息。 
上述这两种情况，行政人员和采购员对布告栏的访问就需要进行同步。因为其中一个线程（行政人员）修改了共享资源（布告栏）。而且我们可以看到，行政人员的工作流程和采购员的工作流程（执行代码）完全不同，但是由于他们访问了同一份可变共享资源（布告栏），所以他们之间需要同步。
## 7.生产者与消费者
- 生产者-消费者模型：当队列满时，生产者需要等待队列有空间才能继续往里面放入商品，而在等待的期间内，

        生产者必须释放对临界资源（即队列）的占用权。因为生产者如果不释放对临界资源的占用权，

        那么消费者就无法消费队列中的商品，就不会让队列有空间，那么生产者就会一直无限等待下去。

        因此，一般情况下，当队列满时，会让生产者交出对临界资源的占用权，并进入挂起状态。
        然后等待消费者消费了商品，然后消费者通知生产者队列有空间了。

        同样地，当队列空时，消费者也必须等待，等待生产者通知它队列中有商品了。这种互相通信的过程就是线程间的协作。
- 代码
- 
```
public class CusAndPro {

 

    private int queueSize = 10 ;

    private PriorityQueue<Integer> queue = new PriorityQueue<Integer>(queueSize);

     

    public static void main(String[] args) {

        CusAndPro cap = new CusAndPro();

        Consumer cus = cap.new Consumer();

        Producer pro = cap.new Producer();

        Thread cusT = new Thread(cus);

        Thread proT = new Thread(pro);

         

        proT.start();

        cusT.start();

    }

    /**

     * 消费者

     * com.subject01.CusAndPro.java

     * @author 孙涛

     * 2016年5月10日

     */

    class Consumer implements Runnable{

 

        @Override

        public void run() {

            cousume();

        }

 

        private void cousume() {

            while(true){

                synchronized (queue) {

                    while(queue.size() ==0){

                        try {

                            System.out.println("队列空，等待数据。。。");

                            queue.wait();

                        } catch (InterruptedException e) {

                            e.printStackTrace();

                            queue.notify();

                        }

                    }

                     

                    queue.poll() ;

                    queue.notify();

                    System.out.println("从队列中取走一个元素，队列中剩余"+queue.size()+"个");

                }

            }

        }

         

    }

    /**

     * 生产者

     * com.subject01.CusAndPro.java

     * @author 孙涛

     * 2016年5月10日

     */

    class Producer implements Runnable{

 

        @Override

        public void run() {

            produce();

        }

 

        private void produce() {

            while(true){

                synchronized(queue){

                    while(queue.size() == queueSize){

                        try {

                            System.out.println("队列已满，等待空余的空间");

                            queue.wait();

                        } catch (InterruptedException e) {

                            e.printStackTrace();

                            queue.notify();

                        }

                    }

                     

                    queue.offer(1);   // 每次插入一个元素

                    queue.notify();

                    System.out.println("向队列取中插入一个元素，队列剩余空间："+(queueSize-queue.size()));

                }

            }

        }

         

    }

}
```
## 8.线程池
- 多线程技术主要解决处理器单元内多个线程执行的问题，它可以显著减少处理器单元的闲置时间，增加处理器单元的吞吐能力。
    
    假设一个服务器完成一项任务所需时间为：T1 创建线程时间，T2 在线程中执行任务的时间，T3 销毁线程时间。
    
    如果：T1 + T3 远大于 T2，则可以采用线程池，以提高服务器性能。
                一个线程池包括以下四个基本组成部分：
                1、线程池管理器（ThreadPool）：用于创建并管理线程池，包括 创建线程池，销毁线程池，添加新任务；
                2、工作线程（PoolWorker）：线程池中线程，在没有任务时处于等待状态，可以循环的执行任务；
                3、任务接口（Task）：每个任务必须实现的接口，以供工作线程调度任务的执行，它主要规定了任务的入口，任务执行完后的收尾工作，任务的执行状态等；
                4、任务队列（taskQueue）：用于存放没有处理的任务。提供一种缓冲机制。
                
    线程池技术正是关注如何缩短或调整T1,T3时间的技术，从而提高服务器程序性能的。它把T1，T3分别安排在服务器程序的启动和结束的时间段或者一些空闲的时间段，这样在服务器程序处理客户请求时，不会有T1，T3的开销了。
    线程池不仅调整T1,T3产生的时间段，而且它还显著减少了创建线程的数目，看一个例子：
    假设一个服务器一天要处理50000个请求，并且每个请求需要一个单独的线程完成。在线程池中，线程数一般是固定的，所以产生线程总数不会超过线程池中线程的数目，而如果服务器不利用线程池来处理这些请求则线程总数为50000。一般线程池大小是远小于50000。所以利用线程池的服务器程序不会为了创建50000而在处理请求时浪费时间，从而提高效率。
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    

