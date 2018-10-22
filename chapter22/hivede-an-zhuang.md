## 命令行界面
```
hive -h  //查看帮助文档
hive //直接进入hive客户端。
```
变量和属性  
set;  //查看所有属性

hive中的一次使用
hive -e "select * from mytest limit 3" >/temp/log
hive -S -e "select * from mytest limit 3" >/temp/log
hive -e "set" |grep warehouse

从文件中执行hive查询
hive -f /temp/hive.hql  
或者
hive > source /temp/hive.q

伪表：src

hiverc文件



