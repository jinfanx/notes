## 工作原理
本质上是一个CS应用，通常所说的zookeeper是指Server，可以在zookeeper的节点上注册事件即Watcher，当事件发生时可以通知到订阅了该事件的客户端，观察者模式。当客户端连接到Server后，会定时发送心跳，当Server检测不到心跳时，就会删除对应的节点，从而感应到节点下线，触发相应事件，通知到相关的客户端。

## 应用
- 分布式协调服务
检测集群状态，知道集群中哪些机器存活哪些失效

- 发布订阅（配置中心）
用zk存储配置，相应的服务从zk取配置，并订阅配置变化，当配置发生变化时zk可以主动通知各个服务，使服务更新配置

- 目录服务

- 分布式锁

- 集群选举
集群内的多台机器同时创建某个节点，zk能保证只有一台机器能成功，此时成功的机器就时leader，其他失败的机器可以监听创建的节点，当节点失效时，zk会通知到其他机器，重新进行选举。典型应用有hdfs namenode和yarn resource manager的ha（高可用）

## 参考文章
[https://blog.csdn.net/qiangcuo6087/article/details/79042035](https://blog.csdn.net/qiangcuo6087/article/details/79042035)