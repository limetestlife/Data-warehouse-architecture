# ZooKeeper简介
ZooKeeper是一个分布式的，开放源码的分布式应用程序协调服务，是Google的Chubby一个开源的实现，它是集群的管理者，监视着集群中各个节点的状态根据节点提交的反馈进行下一步合理操作。最终，将简单易用的接口和性能高效、功能稳定的系统提供给用户  https://www.cnblogs.com/felixzh/p/5869212.html

3.Zookeeper文件系统

每个子目录项如NameService 都被称作为znode，和文件系统一样，我们能够自由的增加、删除znode，在一个znode下增加、删除子znode，唯一的不同在于znode是可以存储数据的。 

有四种类型的znode： 
1、PERSISTENT-持久化目录节点：客户端与zookeeper断开连接后，该节点依旧存在 
2、PERSISTENT_SEQUENTIAL-持久化顺序编号目录节点：客户端与zookeeper断开连接后，该节点依旧存在，只是Zookeeper给该节点名称进行顺序编号 
3、EPHEMERAL-临时目录节点：客户端与zookeeper断开连接后，该节点被删除 
4、EPHEMERAL_SEQUENTIAL-临时顺序编号目录节点：客户端与zookeeper断开连接后，该节点被删除，只是Zookeeper给该节点名称进行顺序编号 





5.Zookeeper做了什么？
1.命名服务   2.配置管理   3.集群管理   4.分布式锁  5.队列管理


zookeeper原理



