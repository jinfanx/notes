## gc策略
年轻代与老年代特定不同，年轻代对象朝生夕死，一次gc一般有90%以上的对象可以被回收，一般采用复制算法；
老年代在full gc时被回收，gc之后一般仍会有大量对象存活，一般用标记整理算法。
## gc算法
引用计数法无法解决循环引用问题，容易引起内存泄漏

### 垃圾回收算法
- 标记清除
- 标记整理
- 复制算法

### gc root
- 虚拟机栈
- 本地方法栈
- 方法区
- jvm自身（如classloader等）

## 垃圾收集器

|垃圾回收器|分代|特点|使用方法|
|:--------|:---|:---|:------|
|Serial|young|串行收集器，单线程，client模式下默认的年轻代垃圾收集器|-XX:+UseSerialGC |
|Serial Old|old|串行收集器，单线程|MCS发生Concurrent Mode Failure时使用，以及时client模式下默认的老年代垃圾收集器|
|ParNew|young|多线程|-XX:+UseParNewGC或-XX:+UseConcMarkSweepGC，使用CMS时默认会使用ParNew，因为除serial外，只有ParNew可以搭配CMS使用|
|ParOld|old|多线程|XX:+UseParallelOldGC|
|Parallel Scavenge|young|停顿时间可控、高吞吐量、多线程|-XX:MaxGCPauseMillis 最大停顿时间<br/>-XX:GCTimeRatio 用户代码运行时间与gc时间比值，如99，则表示gc比例为1/(99+1),即1%|
|CMS|old|低停顿，高吞吐|-XX:+UseConcMarkSweepGC|
|G1|yong and old|不用搭配其他垃圾回收器，低停顿、高吞吐、多线程|-XX:+UseG1GC|
|ZGC||jdk11引入的垃圾收集器，TB级别的内存管理，GC停顿时间不会随着堆的增大而提高，最大GC停顿时间不超过10ms，吞吐量损耗不超过15%|--|


> 高吞吐：吞吐量=用户代码运行时间/总时间，高吞吐表示用户代码运行所占时间比例大

> 低停顿：GC时会STW(stop the world)，低停顿指gc时停顿时间短

## 查看jvm运行参数
```shell
java -XX:+PrintCommandLineFlags Main
```

## 参考文章
[https://blog.csdn.net/CrankZ/article/details/86009279](https://blog.csdn.net/CrankZ/article/details/86009279)