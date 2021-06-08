##显示锁(ReentrantLock)与内置锁(synchronized)的比较
两种加锁方式都能实现同样的内存语义，并且对共享数据提供独占式的访问而且同时支持重入。
###synchronized
####优点:
- 语法简单，不易出错，众人皆知，只需要在方法声明或者代码块儿上添加synchronized关键字即可
- 不需要手动的获取和释放锁，完全有JVM自动完成
- JVM能够进行一些锁的自动优化来提升性能，例如锁消除优化，

####缺点：
- 不支持锁获取过程的中断
- 无法设置锁的超时时间
- 无法进行轮询式的锁获取方式
- 不支持锁的公平性选择
- 性能比显示锁要稍差一些，但是在1.6以后区别不是很大
- 只能在一个方法内进行锁定



###ReentrantLock
####优点:
- 可以对获取锁的过程进行定时，方便实现对操作时间有限制的需求
- 可以中断锁的获取，可以实现有取消功能的需求
- 可以已轮询的方式来获取锁，可以实现对在获取锁失败的情况下，需要做其它备选处理的需求
- 可以选择使用公平锁还是非公平锁（默认为非公平锁）
- 可以实现跨方法的锁定
- 
- 性能更优异，并且可以使用连锁式加锁的方式来实现分段加锁，以进一步降低锁的粒度获取更好的性能
####缺点：
- 语法繁琐，一般以try-finally的方式来手动的获取和释放，可能由于疏忽从而造成死锁

###如何判断是选择公平锁还是非公平锁？
如果锁的持有时间非常短暂，而且竞争比较激烈的情况下，使用非公平锁可以带来更多的性能提升，因为在排队线程被唤醒期间，活跃线程对锁进行请求也可以立即获取到锁.
否则就改使用公平锁来防止线程饥饿问题的发生。而且大多数情况下，非公平锁的性能是优于公平锁的，这也是为什么Java默认使用非公平锁。

###读写锁(ReadWriteLock)
读和写线程分别使用不同的锁来对共享数据进行加锁，允许多个读线程同时获取读锁来访问共享数据，而只能允许一个写线程获取写锁对数据进行修改。
比较适合在读多写少的情况下使用来提升性能，如果是写比较多的情况下，性能反倒因为复杂度的提高还不如排他锁。

###Lock的Condition和Object自带条件队列的比较


###为什么轮询的tryLock会造成公平锁的插队问题？
###如何避免死锁？
- 通过使用相同顺序来获取锁从而避免死锁的发生
- 使用显示锁的轮询和定时功能来避免死锁的发生


###如何实现有阻塞需求的业务
可以配合使用轮询和休眠来简单实现
可以使用条件队列来实现高效的阻塞
###天天如何正确的使用条件队列
获取锁
在循环中检查条件，不满足则调用wait等待条件
对锁保护的状态进行操作
调用通知
在finally块中释放锁
###notify方法使用的前提条件
只有在条件队列上等待的所有线程都在等待相同的条件，以及每次通知只能唤醒一个线程时才能使用notify方法
###对象内置条件队列和Condition对象的比较
####内置队列
优点：每个对象自带条件队列，
缺点：一个锁对象只有一个条件等待队列，因此大部分情况下需要调用notifyAll来进行通知，可能会造成性能问题，虽然可以使用条件通知来进行缓解，如果使用notify通知容易导致信号劫持问题，不支持公平等待队列
###condition条件队列
优点：一个锁对象可以创建多个条件等待队列用于不同的等待条件，因此代码逻辑会更容易分析，而且因为对不同的条件使用不同的队列可以使用signal唤醒单独的某个线程避免不必要的线程上下文切换的开销。可以选择公平队列或非公平队列。
缺点：
###两者如何进行选择
一般取决于锁的选择，因为选择锁时就会根是否需要中断，超时，无条件返回等条件来判断选择何种锁，一旦锁定下来了，条件队列也就相应的定下来了。
###AQS框架的实现原理
支持独占的获取操作需要实现tryAquire,tryRelease和isHeldExclusively等
支持共享的获取操作需要实现tryAquireShared,tryReleaseShared等
而AQS的aquire,aquireShared,release和releaseShared就会调用相应的有try前缀的方法
###使用AQS框架实现的常见同步器类
- ReentrantLock
- ReadWriteReentrantLock
- Semaphore
- CountdownLatch
- SynchronousQueue
###原子变量的实现原理
利用硬件的CAS指令来实现变量的原子更新操作以及实现于volatile相同的内存可见性
###原子变量与锁之间的区别
原子变量相当于是一种乐观锁的实现，因此在使用时需要在循环中来查看更新是否生效，如果失败需要重新尝试，而锁是一种悲观锁的实现，
在使用时需要先锁定目标然后进行独占式的访问，而且原子变量不会引起进程调度，因此不会有进程上下文切换的开销，因此在并发情况不是很激烈的情况下，原子变量的性能要优于锁。
###volatile与原子变量的比较
volatile和原子变量与锁相比是更轻量级的同步机制，不会造成上下文的切换，性能更好
####volatile
优点：使用简单，支持所有的数据类型，使用store-load Barrier内存屏障来确保可见性
缺点：不支持复合操作,不支持数组元素的原子更新操作
####原子变量
优点：支持复合操作，支持数组元素的原子更新操作，支持store-store Barrier内存屏障类型，可以提供比volatile更高的性能
缺点：需要使用单独的原子变量类，只支持int,long,reference以及对应的数组数据类型
###原子变量支持的类型有哪些
int，long，reference以及这三种类型对应的数组类型，以及long和double的Adder和Accumulator类
###如何解决ABA问题
可以使用AtomicStampedReference给数据加上一个版本号来解决
###JAVA内存模型的happens before关系有哪些
- Program order rule.
  Each action in a thread happens before every action in that thread that comes later in the program order.
- Monitor lock rule.
  An unlock on a monitor lock happens before every subsequent lock on that same monitor lock.
- Volatile variable rule.
  A write to a volatile field happens before every subsequent read of that same field.
- Thread start rule.
  A call to Thread.start on a thread happens before every action in the started thread.
- Thread termination rule.
  Any action in a thread happens before any other thread detects that thread has
  terminated,either by successfully return from Thread.join or by Thread.isAlive returning false.
- Interruption rule. 
  A thread calling interrupt on another thread happens before the interrupted thread detects the
  interrupt(either by having InterruptedException thrown,or invoking isInterrupted or interrupted).
- Finalize rrule. 
  The end of a constructor for an object happens before the start of the finalizer for that object.
- Transitivity. 
  If A happens before B,and B happens before C,then A happens before C.
###如何安全的发布对象
- 在静态初始化函数中初始化一个对象应用
- 将对象的引用保存到volatile类型的域中，或者AtomicReference对象中
- 将对象的引用保存到某个正确构造对象的final类型的域中(初始化安全性只能保证通过final域可达的值从构造完成时开始的可见性)
- 将对象的引用保存到一个由锁保护的域中
- 不可变对象天然就是线程安全的

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

是有构造函数捕获模式(private constructor capture idiom)

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
  不捕获改InterruptedException,或先捕获InterruptedException，进行简单的清理工作然后再抛出InterruptedException
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

预防措施：不要使用线程优先级，避免平台依赖性。

###信号丢失
线程在等待一个已经发生过的信号，导致线程一直等待下去无法继续执行。最常见的例子就是在锁的条件队列上进行等待

###活锁
线程不断的重复执行相同的操作，而且总是失败，导致线程无法向前执行。
最典型的例子就是毒药消息，当消息处理失败后又被放入消息队列，然后导致一直被重复处理。
还有一个例子就是多个线程根据自身和对方的状态来进行调整时导致线程无法执行下去。可以通过随机延迟来解决这个问题

###死锁
####类型
- 静态锁顺序死锁
- 动态锁顺序死锁(例如通过方法传入的两个参数来进行加锁)
- 协作对象间的死锁(在持有锁期间调用外部方法一定要格外小心这个问题)
- 资源死锁(可以通过随机延迟或定时锁来解决这类死锁问题)
####解决办法
- 已相同的锁顺序来获取锁
- 通过开放调用(open call,即在调用外部方法是不持有锁)来避免相互协作对象间产生死锁

####如何分析死锁
- 通过导出threaddump(jstack thread_id or kill -3 thread_id)，也可以通过调用management API通过代码来触发threaddump导出，然后使用JProfiler或在线的Jstack工具来分析.

###性能优化
- 避免不成熟的优化，首先是程序正确允许，当有明确的需求时再进行优化。
- 阻塞操作会导致线程被挂起，在这个过程中会导致额外的两次上下文切换，以及所有必要的操作系统操作和缓存操作。
- 除高开销对象(比如数据库连接)以外尽量避免使用使用对象池，因为Java分配对象的操作现在已经非常快了，而且对象池的大小也不好确定，太小了没啥作用，太大了会占用其它对象的内存空间从而导致垃圾回收器的频繁调度影响性能。

###如何降低锁竞争程度
- 减少锁的持有时间(缩小同步代码块的范围就是一种有效的手段)
- 降低锁的请求频率(锁分解和锁分段技术)
- 使用非阻塞锁，这些机制允许更高的并发性。(列如读写锁，原子变量)

###如何使用perfmon(vmstat)查看CPU使用情况
###如何使用perfmon(iostat)查看IO使用情况
###如何使用测量锁竞争

###内存同步
内存同步会增加内存总线上的通信量，总线的带宽是有限的，所有的处理器都会共享这条总线。
因此非阻塞算法在竞争比较激烈的竞争下会导致同步通信量的增加
