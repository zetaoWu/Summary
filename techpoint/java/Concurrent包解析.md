## Concurrent包 解析

  **Executor:**

   Executor接口是所有线程执行类的父接口，这个接口可以建立线程池，然后执行线程

   **ExecutorService:**

   ExecutorService可以帮助我们建立线程池。

   **BlockingQueue:**

  阻塞队列跟信号量差不多，比如生产者消费者问题中，如果不用阻塞队列，采用非阻塞队列存放产品的话，需要用synchronized来对produce()和consume()操作进行同步，而采用阻塞队列就不需要这样了，它自身就带同步功能，当空时自然不能取，满时自然不能继续生产，这就是BlockingQueue的作用。

  阻塞队列使用最经典的场景就是socket客户端数据的读取和解析，读取数据的线程不断将数据放入队列，然后解析线程不断从队列取数据解析。还有其他类似的场景，只要符合生产者-消费者模型的都可以使用阻塞队列。

  **Semphore:**

  信号量Semaphore是一个计数信号量，用来保护一个或多个共享资源的访问，是Java Concurrent包下提供的另一种同步方式，*就像synchronized一样的呢，它就是替代synchronized的*。 Semaphore可以控制某个资源可被同时访问的个数，通过 acquire() 获取一个许可，如果没有就等待，而 release() 释放一个许可。

  **CountDownLatch:**

  利用它可以实现类似计数器的功能。比如有一个任务A，它要等待其他4个任务执行完毕之后才能执行，此时就可以利用CountDownLatch来实现这种功能了。

  *操作方法*

  * 构造函数CountDownLatch(int count)，count表示要等待的操作数的数目。
  * await()方法，阻塞等待，需要其他线程完成期待的操作，直到count为0。
  * countDown()方法，当某一个操作完成后，调用此方法，count数减一。

  CountDownLatch一般用于某个线程A等待若干个其他线程执行完任务之后，它才执行；
  CyclicBarrier一般用于一组线程互相等待至某个状态，然后这一组线程再同时执行；
  CountDownLatch是不能够重用的，而CyclicBarrier是可以重用的。

  **ReentrantLock:**

  ReentrantLock是java.util.concurrent包下提供的一套互斥锁，相比Synchronized，ReentrantLock类提供了一些高级功能，主要有以下3项：
   1.*等待可中断*，持有锁的线程长期不释放的时候，正在等待的线程可以选择放弃等待，这相当于Synchronized来说可以避免出现死锁的情况。
   2.*公平锁*，多个线程等待同一个锁时，必须按照申请锁的时间顺序获得锁，Synchronized锁非公平锁，ReentrantLock默认的构造函数是创建的非公平锁，可以通过参数true设为公平锁，但公平锁表现的性能不是很好
   3.*锁绑定多个条件*


  **ThreadLocal**

  线程私有变量，最常见的ThreadLocal使用场景为 用来解决 数据库连接、Session管理等。 ThreadLocal为变量在每个线程中都创建了一个副本，那么每个线程可以访问自己内部的副本变量。

  **Condition:**
