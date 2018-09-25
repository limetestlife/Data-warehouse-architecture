**kafka的message包括哪些信息**
一个Kafka的Message由一个固定长度的header和一个变长的消息体body组成
header部分由一个字节的magic(文件格式)和四个字节的CRC32(用于判断body消息体是否正常)构成。当magic的值为1的时候，会在magic和crc32之间多一个字节的数据：attributes(保存一些相关属性，比如是否压缩、压缩格式等等)；如果magic的值为0，那么不存在attributes属性body是由N个字节构成的一个消息体，包含了具体的key/value消息