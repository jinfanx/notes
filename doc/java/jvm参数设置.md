## 为什么要设置jvm参数
jvm运行时需要设置一些参数，包括内存、gc等，如果不设置，jvm将会使用默认值，在生产环境中，这些值往往是不能满足需求的，可能导致应用运行效率低下甚至宕机

## 设置哪些参数
主要是内存和gc参数

|参数|说明|示例|默认值|
|:---|:--|:---|:----|
|-Xmx| 最大堆内存 | -Xmx:4096m |物理内存的1/4,`一般大小和初始内存保持一致，因为可以避免内存伸缩的开销`|
|-Xms| 初始堆内存 | -Xms:4096m |物理内存的1/64|
|-Xmn| 年轻代大小 | -Xmn:1024m ||
|-Xss| 栈大小 | -Xss256k | |
|-XX:PermSize| 非堆初始大小 | -XX:PermSize=80m |`和最大非堆内存保持一致，因为可以避免内存伸缩的开销`|
|-XX:MaxPermSize| 非堆最大内存 | -XX:MaxPermSize:80m ||
|-XX:SurvivorRatio| Eden:Survivor, 年轻代=Eden + survivor + sruvivor, 该值表示Eden和一个Survivor的比值，8表示Eden占年轻代的80%，两个survivor各占10%；1表示Eden和两个survivor各占1/3 | XX:SurvivorRatio=4 |8|

关于垃圾收集器设置见[ gc.md ](gc.md#垃圾收集器)


## jvm参数设置实例
```
-server
-Xms6000M
-Xmx6000M
-Xmn500M
-XX:PermSize=500M
-XX:MaxPermSize=500M
-XX:SurvivorRatio=65536
-XX:MaxTenuringThreshold=0
-Xnoclassgc
-XX:+DisableExplicitGC
-XX:+UseParNewGC
-XX:+UseConcMarkSweepGC
-XX:+UseCMSCompactAtFullCollection
-XX:CMSFullGCsBeforeCompaction=0
-XX:+CMSClassUnloadingEnabled
-XX:-CMSParallelRemarkEnabled
-XX:CMSInitiatingOccupancyFraction=90
-XX:SoftRefLRUPolicyMSPerMB=0
-XX:+PrintClassHistogram
-XX:+PrintGCDetails
-XX:+PrintGCTimeStamps
-XX:+PrintHeapAtGC
-Xloggc:log/gc.log
```

## 参考文章
[https://www.cnblogs.com/dayhand/p/3757273.html](https://www.cnblogs.com/dayhand/p/3757273.html)