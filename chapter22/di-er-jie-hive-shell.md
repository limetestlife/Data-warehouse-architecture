create external table lime_hbase(
c1 string,
c2 string)
partitioned by(dt string)
stored as rcfile;

alter table lime_hbase add partition (dt='20180415') location '/user/sinadata/tmp/liangmeng1/weibosporthdfs/';

select sum(case when substr(c1,1,2)='53' then 1 else 0 end)  from lime_hbase;

select count(*) from lime_hbase where substr(c1,1,2)='53';


nohup hive -e 'select substr(c1,1,2) as section_flag,count(*) as num from  lime_hbase GROUP BY substr(c1,1,2)' >sum.log &




# 数据定义

数据库
show databases;
show databases like 'h.*';

表




# 实例
```
nohup hive -S -e "select distinct a.uid from 
(select uid,mid from ods_xxxx_content where dt>=20181029 and dt<=20181112 and instr(concat(extend,content),'#理想生活季#')>0) a
join 
(select uid,object from ods_xxxxx where behavior='14000003' and dt>=20181029 and dt<=20181112 and instr(extend,'isTransmit')<1) b
on a.mid=b.object">resuid &

知识点：
nohup xxxxx &         shell后台执行
hive -S -e "hivesql"  静默执行sql语句
concat(str1,str2)     将两个字符串合并
instr(str1,str2)      str2在str1中的起始位置，若str1不包含str2则返回0，故可以用来判断字符串包含情况。  

```





