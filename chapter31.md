**1.hdfs上传文件的流程。**

答：这里描述的 是一个256M的文件上传过程

① 由客户端 向 NameNode节点节点 发出请求

②NameNode 向Client返回可以可以存数据的 DataNode 这里遵循机架感应原则

③客户端 首先 根据返回的信息 先将 文件分块（Hadoop2.X版本 每一个block为 128M 而之前的版本为 64M

④然后通过那么Node返回的DataNode信息 直接发送给DataNode 并且是 流式写入  同时 会复制到其他两台机器

⑤dataNode 向 Client通信 表示已经传完 数据块 同时向NameNode报告 ⑥依照上面（④到⑤）的原理将 所有的数据块都上传结束 向 NameNode 报告 表明 已经传完所有的数据块 。

**HDFS读写数据的过程**
 读：
1、跟namenode通信查询元数据，找到文件块所在的datanode服务器
2、挑选一台datanode（就近原则，然后随机）服务器，请求建立socket流
3、datanode开始发送数据（从磁盘里面读取数据放入流，以packet为单位来做校验）
4、客户端以packet为单位接收，现在本地缓存，然后写入目标文件写：
1、根namenode通信请求上传文件，namenode检查目标文件是否已存在，父目录是否存在
2、namenode返回是否可以上传
3、client请求第一个 block该传输到哪些datanode服务器上
4、namenode返回3个datanode服务器ABC
5、client请求3台dn中的一台A上传数据（本质上是一个RPC调用，建立pipeline），A收到请求会继续调用B，然后B调用C，将真个pipeline建立完成，逐级返回客户端
6、client开始往A上传第一个block（先从磁盘读取数据放到一个本地内存缓存），以packet为单位，A收到一个packet就会传给B，B传给C；A每传一个packet会放入一个应答队列等待应答
7、当一个block传输完成之后，client再次请求namenode上传第二个block的服务器。
