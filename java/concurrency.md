##显示锁(ReentrantLock)与内置锁(synchronized)的比较
两种加锁方式都能实现同样的内存语义，并且对共享数据提供独占式的访问而且同时支持重入。
###synchronized
####优点:
- 语法简单，只需要在方法或者代码块儿上添加synchronized关键字即可
- JVM自动完成锁的获取和释放
- JVM能自动实现锁的优化来提升性能，例如锁消除优化，锁粗化

####缺点：
- 锁获取过程无法被中断
- 无法设置锁获取时间的超时时间
- 无法以非阻塞方式获取锁
- 不支持锁的公平性选择
- 只能在单个方法内进行锁的获取与释放
- 一个锁对象只有一个等待队列，当有多个等待条件时会造成不必要的线程唤醒
- 性能比显示锁要稍差一些，但是在1.6以后区别不是很大

###ReentrantLock
####优点:
- 可以设置锁获取的超时时间，方便实现对操作时间有限制的需求
- 可以中断锁的获取，可以实现有取消功能的需求
- 可以用非阻塞方式来获取锁，实现在获取锁失败的情况下，需要做其它备选处理的需求
- 可以选择使用公平锁还是非公平锁（默认为非公平锁）
- 可以实现跨方法的锁获取与释放
- 一个锁对象可以拥有多个条件队列(Condition),方便实现精准的通知
- 性能更优异，并且可以使用分段加锁，以进一步降低锁的粒度获取更好的性能
####缺点：
- 语法繁琐，需要以try-finally的方式来手动确保锁释放，可能由于疏忽从而造成死锁

###如何判断是选择公平锁还是非公平锁？
如果锁的持有时间非常短暂，而且竞争比较激烈的情况下，使用非公平锁可以带来更多的性能提升，
因为在排队线程被唤醒期间，活跃线程对锁进行请求可以立即获取到锁,从而可以抵消线程的上下文切换带来的开销。
只有在锁的持有时间比较长时才应该考虑使用公平锁来防止线程饥饿问题的发生。
而且大多数情况下，非公平锁的性能是优于公平锁的，这也是为什么Java默认使用非公平锁。

###读写锁(ReadWriteLock)
读和写线程分别使用不同的锁来对共享数据进行加锁，允许多个读线程同时获取读锁来访问共享数据，而只能允许一个写线程获取写锁对数据进行修改。
比较适合在读多写少的情况下代替ReentrantLock来提升性能，如果是写比较多的情况下，性能反倒因为复杂度的提高还不如排他锁。

###为什么轮询的tryLock会造成公平锁的插队问题？
因为tryLock会先直接尝试获取锁，如果当时有锁可用，就可以直接获取，如果在锁持有时间很短的情况下，既能满足当前线程对锁的使用，也不影响后续被唤醒的线程对锁的使用，因为线程被唤醒到被调度也是需要时间的。

###如何避免死锁？
- 通过使用相同顺序来获取锁从而避免死锁的发生
- 使用显示锁的轮询和定时功能来避免死锁的发生


###如何实现有阻塞需求的业务
- 可以配合使用轮询和休眠来简单实现
- 可以使用条件队列来实现高效的阻塞
###如何正确的使用条件队列
1.获取锁(tryLock)
2.在循环中检查条件，不满足则调用wait继续等待条件
3.对锁保护的状态进行操作
4.调用通知
5.在finally块中释放锁
###notify方法使用的前提条件
只有在条件队列上等待的所有线程都在等待相同的条件，并且每次通知只能唤醒一个线程时才能使用notify方法
###对象内置条件队列和Condition对象的比较
####内置队列
优点：每个对象自带条件队列
缺点：一个锁对象只有一个条件等待队列，因此大部分情况下需要调用notifyAll来进行通知，容易造成性能问题，虽然可以使用条件通知来进行缓解，如果使用notify通知容易导致信号劫持问题，不支持公平等待队列
###condition条件队列
优点：一个锁对象可以创建多个条件等待队列用于不同的等待条件，因此代码逻辑会更容易分析，而且因为对不同的条件使用不同的队列可以使用signal唤醒单独的某个线程避免不必要的线程上下文切换的开销。可以选择公平队列或非公平队列。
缺点：
###两者如何进行选择
一般取决于锁的选择，因为选择锁时就会根是否需要中断，超时，非阻塞返回等条件来判断选择何种锁，一旦锁定下来了，条件队列也就相应的定下来了。
###AQS(AbstractQueuedSynchronizer)框架的实现原理
支持独占的获取操作需要实现tryAcquire,tryRelease和isHeldExclusively等
支持共享的获取操作需要实现tryAcquireShared,tryReleaseShared等
AQS的acquire,acquireShared,release和releaseShared就会调用相应的有try前缀的方法
###使用AQS框架实现的常见同步器类
- ReentrantLock
- ReadWriteReentrantLock
- Semaphore
- CountdownLatch
- SynchronousQueue
###原子变量的实现原理
利用硬件的CAS指令来实现变量的原子更新操作以及实现与volatile相同的内存可见性
###原子变量与锁之间的区别
原子变量相当于是一种乐观锁(optimistic locking)的实现，因此在使用时需要在循环中来查看更新是否生效，如果失败需要重新尝试。
原子变量不会引起进程调度，因此不会有进程上下文切换的开销，因此在并发情况不是很激烈的情况下，原子变量的性能要优于锁。
而锁是一种悲观锁(pessimistic locking)的实现，在使用时需要先锁定目标然后进行独占式的访问。

###volatile与原子变量的比较
volatile和原子变量相对于锁来说是更轻量级的同步机制，不会造成上下文的切换，在并发不是很激烈的情况下性能会更好
####volatile
优点：使用简单，支持所有的数据类型，使用内存屏障(store-load Barrier)来确保可见性
缺点：不支持复合操作,不支持数组元素的原子更新操作
####原子变量
优点：支持复合操作，支持数组元素的原子更新操作，支持store-store Barrier内存屏障类型，可以提供比volatile更高的性能
缺点：需要使用单独的原子变量类，只支持int,long,reference以及对应的数组数据类型
###原子变量支持的类型有哪些
- int，long，reference以及这三种类型对应的数组类型，
- long和double的Adder和Accumulator类,这两个类使用动态分段技术(dynamic striping)在多线程的环境下提供更好的性能
###如何解决ABA问题
可以使用AtomicStampedReference给数据加上一个版本号来解决
###JAVA内存模型的happens before关系有哪些
1. Program order rule.
  Each action in a thread happens before every action in that thread that comes later in the program order.
2. Monitor lock rule.
  An unlock on a monitor lock happens before every subsequent lock on that same monitor lock.
3. Volatile variable rule.
  A write to a volatile field happens before every subsequent read of that same field.
4. Thread start rule.
  A call to Thread.start on a thread happens before every action in the started thread.
5. Thread termination rule.
  Any action in a thread happens before any other thread detects that thread has been
  terminated,either by successfully return from Thread.join or by Thread.isAlive returning false.
6. Thread Interruption rule. 
  A thread calling interrupt on another thread happens before the interrupted thread detects the
  interrupt(either by having InterruptedException thrown,or invoking isInterrupted or interrupted).
7. Finalize rule. 
  The end of a constructor for an object happens before the start of the finalizer for that object.
8. Transitivity. 
  If A happens before B,and B happens before C,then A happens before C.
###如何安全的发布对象
1. 在静态初始化函数(static initializer)中初始化一个对象应用(因为类在被首次加载时JVM会进行加锁防止并发)
2. 将对象的引用保存到volatile类型的域中，或者AtomicReference对象中
3. 将对象的引用保存到某个正确构造对象的final类型的域中(初始化安全性只能保证通过final域可达的值从构造完成时开始的可见性)
4. 将对象的引用保存到一个由锁保护的域中
5. 不可变对象天然就是线程安全的

###锁的使用注意事项
- 一定不要在复杂计算或可能无法快速完成的操作（列如IO操作，网络调用，可阻塞操作等）时持有锁。
- 尽量缩小锁的使用范围
###同步（加锁）的作用
- 确保操作的原子性
- 确保内存的可见性

###如何设计线程安全的类
- 找出构成对象状态的所有变量
- 找出约束状态变量的不变性条件
- 建立对象状态的并发访问管理策略

私有构造函数捕获模式(private constructor capture idiom)

###同步容器
Vector
Hashtable
Collections.synchronizedXxxx
###并发容器
ConcurrentHashMap
ConcurrentSkipListMap
ConcurrentSkipListSet
CopyOnWriteArrayList
CopyOnWriteArraySet

###工作队列(producer-consumer)
- ArrayBlockingQueue
- LinkedBlockingQueue
- PriorityBlockingQueue
- LinkedTransferQueue
- SynchronousQueue
- DelayQueue

###双端队列(work-stealing)
- LinkedBlockingDeque


###中断处理
- 传递InterruptedException
  不捕获该InterruptedException,或先捕获InterruptedException，进行简单的清理工作然后再抛出InterruptedException
- 恢复中断
  比如在Runnable的实现中就无法抛出异常
  先捕获InterruptedException 然后调用Thread.currentThread().interrupt()方法来恢复中断状态

###同步工具类(Semaphore,Barrier,Latch)
- 闭锁(Latch)用于确保某些活动直到其他活动都完成后才能继续执行.具体实现CountDownLatch，FutureTask
- 信号量(Semaphore)用于控制同时访问某个特定资源的操作数量.具体实现Semaphore
- 栅栏(Barrier)用于确保一组线程都到达栅栏位置才能继续运行。具体实现CyclicBarrier，Exchanger


##活跃性问题

###饥饿
当线程一直无法获取到它所需要的资源时就会发生饥饿。例如线程优先级设置不当导致线程无法获取到cpu资源，或者是持有锁时执行一些无法结束的操作

预防措施：
- 不要使用线程优先级，避免平台依赖性。
- 不在可能长时间无法完成的操作中持有锁

###信号丢失
线程在等待一个已经发生过的信号，导致线程一直等待下去无法继续执行。最常见的例子就是在锁的条件队列上进行等待

###活锁
线程重复执行相同的操作，并且总是失败，导致线程无法向前执行。
最典型的例子就是毒药消息(poison message)，当消息处理失败后又被放入消息队列，然后导致一直被重复处理。
还有一个例子就是多个线程根据自身和对方的状态来进行调整时导致线程无法执行下去,可以通过随机延迟(random delay)来解决这个问题。

###死锁
####类型
- 静态锁顺序死锁
- 动态锁顺序死锁(例如通过方法传入的两个参数来进行加锁)
- 协作对象间的死锁(在持有锁期间调用外部方法一定要格外小心这个问题)
- 资源死锁(可以通过随机延迟或定时锁来解决这类死锁问题)
####解决办法
- 以相同的锁顺序来获取锁
- 通过开放调用(open call,即在调用外部方法时不持有锁)来避免相互协作对象间产生死锁

####如何分析死锁
- 通过导出threaddump(jstack thread_id or kill -3 thread_id)，也可以通过调用Management Bean API通过代码来触发threaddump导出，然后使用JProfiler或在线的Jstack工具来分析.

###性能优化
- 避免不成熟的优化，首先是确保程序正确运行，当有明确的需求时再进行优化。
- 阻塞操作会导致线程被挂起，在这个过程中会导致额外的两次上下文切换，以及所有必要的操作系统操作和缓存操作。
- 除高开销对象(比如数据库连接)以外尽量避免使用对象池(Object Pool)，因为Java分配对象的操作现在已经非常快了，
  而且对象池的大小也不好确定，太小了没啥作用，太大了会占用其它对象的内存空间从而导致垃圾回收器的频繁调度影响性能。

###如何降低锁竞争程度
- 减少锁的持有时间(缩小同步代码块的范围就是一种有效的手段)
- 降低锁的请求频率(锁分解和锁分段技术)
- 使用非阻塞锁，这些机制允许更高的并发性。(列如读写锁，原子变量)

###如何使用perfmon(vmstat)查看CPU使用情况
###如何使用perfmon(iostat)查看IO使用情况
###如何测量一个锁是否竞争激烈
可以使用Management Bean 或者shell脚本来定时的抓取thread dump，如果发现同一个锁在多次thread dump中都存在的话就表明这个锁的竞争比较激烈

###内存同步
内存同步会增加内存总线上的通信量，总线的带宽是有限的，所有的处理器都会共享这条总线。
因此非阻塞算法在竞争比较激烈的竞争下会导致同步通信量的增加，从而降低性能。
就好比过十字路口，如果交通不是太拥堵的情况，不看红绿灯而是由司机自己判断是否可以通行，
但是当交通比较拥堵时最好还是依据红绿灯来控制是否通行能最大限度的提高通行量

###线程池相关接口
Executors(工具类，方便创建常用的线程池对象)
Executor(线程执行器接口，定义了execute方法，实现了任务提交与执行的隔离) 
ExecutorService(提供线程池的生命周期管理，以及定义了可返回结果的submit接口)
ScheduledExecutorService(提供定时或周期性执行任务的能力)
CompletionService(将任务的提交和结果的获取相隔离开，特别适合提交一批任务后，在任意一个任务完成时就返回，然后取消其他未完成的任务)
###线程池相关实现类
ThreadPoolExecutor(主要的线程池实现类，主要参数有:corePoolSize,maximumPoolSize,keepAliveTime,workQueue,threadFactory,RejectedExecutionHandler)
ScheduledThreadPoolExecutor(继承ThreadPoolExecutor，提供定时调度的功能)
ExecutorCompletionService(CompletionService的实现类)
###difference between Runnable and Callable
Runnable: cannot return value, cannot throw exception
Callable: can return value, can throw exception,implemented by FutureTask

###why callable can return value and throw exception
in essence, A Callable object is converted to FutureTask object which implement the future and runnable interface,
it will responsible for return the value and exception

Future
RunnableFuture
FutureTask


###add exception handler to capture unhandled exception
we can add a UncaughtExceptionHandler when create a thread, it's very handy to logging any uncaptured exceptions for postmortem analysis.

###how to add some hooks will be executed when jvm shutdown
we can use Runtime.addShutdownHook to register some cleanup hooks


###如何处理不可中断阻塞
1. java.io包中的同步Socket I/O
   关闭socket可以使阻塞的read/write方法抛出SocketException，从而被终止
2. java.io包中的同步I/O
   中断InterruptibleChannel上等待的线程时，会抛出ClosedByInterruptException
3. Selector异步IO
   当一个线程在调用Selector.select方法时阻塞，那么调用selector的close或wakeup方法时会抛出ClosedSelectorException
4. 获取锁
   可以使用Lock API的lockInterruptibly来防止无法取消阻塞

###线程池的使用
###线程池大小设置
- corePoolSize 核心线程数，默认是在提交任务时创建线程，可以通过调用prestartAllCoreThreads,prestartCoreThread方法来提前启动
- maximumPoolSize 最大线程数，只有在工作队列满了并且当前核心线程数小于最大线程数时，才会创建线程，并且会根据keepAlive指定的时间来回收空闲线程
- keepAliveTime 指定线程空闲多久后会被回收，默认情况下只有非核心线程才会被回收，但是可以设置allowCoreThreadTimeOut来回收核心线程
###工作队列的选取
有界队列(ArrayBlockingQueue) 可能会导致任务被拒绝，CPU等资源没被充分利用
无界队列(LinkedBlockingQueue) 可能会导致大量的任务堆积
同步队列(SynchronousQueue) 可能会导致大量线程的创建
同步队列(PriorityBlockingQueue) 可能会导致大量低优先级线程的堆积
###线程工厂(ThreadFactory)
- 线程命名，指定线程组，指定线程优先级，指定后台线程等等
###饱和策略的选取(RejectedExecutionHandler)
- abortPolicy 抛出RejectedExecutionException直接抛弃当前任务
- callerRunsPolicy 在调用线程中执行当前任务
- discardPolicy 丢弃队列中最后面的一个任务，然后重试当前任务
- discardOldestPolicy 丢弃队列中最前面的一个任务，然后重试当前任务

###扩展的回调钩子,可以用于线程池统计信息的收集，日志打印，ThreadLocal初始化等任务
- beforeExecute
- afterExecute
- terminated
