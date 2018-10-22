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





