spark集群运算的模式
Spark 有很多种模式，最简单就是单机本地模式，还有单机伪分布式模式，复杂的则运行在集群中，目前能很好的运行在 Yarn和 Mesos 中，当然 Spark 还有自带的 Standalone 模式，对于大多数情况 Standalone 模式就足够了，如果企业已经有 Yarn 或者 Mesos 环境，也是很方便部署的。
standalone(集群模式)：典型的Mater/slave模式，不过也能看出Master是有单点故障的；Spark支持ZooKeeper来实现 HA
on yarn(集群模式)： 运行在 yarn 资源管理器框架之上，由 yarn 负责资源管理，Spark 负责任务调度和计算
on mesos(集群模式)： 运行在 mesos 资源管理器框架之上，由 mesos 负责资源管理，Spark 负责任务调度和计算
on cloud(集群模式)：比如 AWS 的 EC2，使用这个模式能很方便的访问 Amazon的 S3;Spark 支持多种分布式存储系统：HDFS 和 S3