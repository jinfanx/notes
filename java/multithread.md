## 线程状态
五种，其中阻塞状态优分两种，等待阻塞和其他阻塞
- new
- runnable
- running
- blocked
   - wait block
   - other(join、sleep)
- dead
## concurrent包
### BlockingQueue
- ArrayBlockingQueue
- LinkedBlockingQueue
- DelayQueue
- LinkedTransferQueue
- PriorityBlockingQueue
优先级队列，放入队列的元素是排序的
- SynchronousQueue

### ConcurrentCollection
- CopyOnWriteArrayList
- CopyOnWriteArraySet
- ConcurrentHashMap
- ConcurrentLinkedQueue
- ConcurrentLinkedDeque
- ConcurrentSkipListSet
- ConcurrentSkipListMap

### locks

### atom

### tools
- Semaphore
- Exchanger
- Phaser
- CountDownLatch
- CyclicBarrier

## 线程池
- SingleThreadPool
- FixedThreadPool
- CachedThreadPool
- ScheduleThreadPool
- ThreadPoolExecutor

## Runnable、Callable、Future
- Runnable没有返回值，没有异常
- Callable有返回值，有异常
- Future支持泛型，是对返回值的包装，包含检测任务是否已结束的方法，需要轮询或超时来判断任务进度，从而获取返回值，假异步
- CompletionService
真异步，通过阻塞的take方法获取线程池中已完成的任务


## 锁
### 基本概念
- 共享锁
- 排它锁
- 轻量级锁
- 重量级锁
- 悲观锁
- 乐观锁
- 偏向锁
- 自旋锁 
- java锁升级
- CAS
> compare and swap
- AQS

## 常见问题
### 实现代码同步方法
synchronized和ReentrantLock

### 阻塞队列中add、offer、put区别
> add添加失败抛出异常，offer添加失败返回false，put会阻塞直到成功

### 阻塞队列中remove、poll、take区别
> remove出队失败抛异常，poll出队失败返回null，take会阻塞直到取到元素

### ThreadLocal应用场景
1. 线程间使用同一个对象的副本，可以避免创建大量对象同时避免线程安全问题。如数据库连接、复用SimpleDateFormat等（猜测是使用了原型模式，避免从头开始创建对象）

2. 避免在调用链上传参，相当于使用全局变量。如web系统中的session，可以在第一次处理时把用户信息放到session中，后续的方法就不用传递用户信息，只从session中获取，避免了参数传递。

### 线程池参数
指的是`java.util.concurrent.ThreadPoolExecutor`
```java
public ThreadPoolExecutor(int corePoolSize,
                              int maximumPoolSize,
                              long keepAliveTime,
                              TimeUnit unit,
                              BlockingQueue<Runnable> workQueue,
                              ThreadFactory threadFactory,
                              RejectedExecutionHandler handler) {
        if (corePoolSize < 0 ||
            maximumPoolSize <= 0 ||
            maximumPoolSize < corePoolSize ||
            keepAliveTime < 0)
            throw new IllegalArgumentException();
        if (workQueue == null || threadFactory == null || handler == null)
            throw new NullPointerException();
        this.corePoolSize = corePoolSize;
        this.maximumPoolSize = maximumPoolSize;
        this.workQueue = workQueue;
        this.keepAliveTime = unit.toNanos(keepAliveTime);
        this.threadFactory = threadFactory;
        this.handler = handler;
    }
```
- corePoolSize 核心线程数量，即一直存在的线程数量
- maximumPoolSize 最大线程数量
- keepAliveTime 非核心线程的最大空闲时间，超过这个时间，非核心线程将被关闭
- unit 时间单位，keepAliveTime的时间单位
- workQueue 等待队列，没有被及时处理的任务将会放在等待队列中
- ThreadFactory 线程工厂，用来创建线程
- RejectedExecutionHandler 拒绝策略，当等待队列已满时的处理策略，java实现了四种策略，都定义在`java.util.concurrent.ThreadPoolExecutor`类中


