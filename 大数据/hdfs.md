## 应用场景
适合存储体积较大的数据，而不适合用来存储大量小文件，一个数据被分为多个块并存储多个副本，块大小2.x版本以前是64M，2.x以后为128M

## namenode
存储元数据，包括数据包含哪些数据块，各个数据块存储位置等

## secondary namenode
namenode数据保存在内存中，为了保证可靠，需要做持久化，方案是fsimage + editlog，fsimage是数据快照，editlog为启动后对namenode的写操作。hdfs启动时会将editlog合并到fsimage得到最新的数据，namenode很少重启，这时editlog将会越来越大，secondary namenode就是用来在运行时合并editlog的。

## datanode
真正存储数据的节点

## 常见问题
### 块副本存储策略
一般是存三份，当前机架两份，不同机架一份