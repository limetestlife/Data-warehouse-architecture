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
show databases like 'liem_.*';

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

```
select a.d1,a.d2 from (select split(c1,'\t')[3] d1,count(*) d2 from lime_dayh where dt=20181114 group by split(c1,'\t')[3]) a order by a.d1;
=====
split(c1,'\t')[3]  把c1字段以tab分隔符拆分成数组，取第4个元素
group by 分组
order by 排序
其与msyql和Oracle的sql不同处在其拆分行为需要作为单独的过程。
```

```
select b.workid workid,regexp_replace(b.wordkey, '\\\^', ' ') id,b.index index,a1.extend extend from
(select keyadd.workid,keyword.keycode,keyword.wordkey,keyword.index as index from
(select * from consumpationuplist_keyword where dt='$date') keyword
left join
(select * from consumpationuplist_key_add where dt='$date') keyadd
on (keyword.keycode=keyadd.keycode)) b
left outer join
(select keycode,onkey,concat_ws(':',collect_set(ext)) extend from
(select keycode,onkey,CONCAT_WS(',',concat('mid=>',mid),concat('read=>',read)) as ext from
(select keycode,onkey,mid,read ,row_number() over (partition by keycode,onkey order by cast(read as int) desc) rank_code from
(select keycode,mid,read,wordkey from consumpationuplist_keyword_uid_mid where dt='$date' and (tran>0 || comm>0 || like>0 ||read>0)) a LATERAL VIEW explode(split(wordkey, ',')) aa as onkey) h where rank_code<=200) gb group by keycode,onkey) a1
on a1.keycode=b.keycode and a1.onkey=b.wordkey;
===
regexp_replace sql中转义 \^，hive -e sql.sql中多加一个即\\^ 在多调用一层脚本再多加\\\^ 。在hive -e "SQL"的执行方式中，"'正则表达式'"，正则表达式先被一个单引号括起来，再被一个双引号括起来的，所以正则表达式里面，\\^的第一个\用来解析第二个\，第二个\才真正起到了转义的作用
concat('mid=>',mid)   字符串拼接
CONCAT_WS(',',concat('mid=>',mid),concat('read=>',read))   设置连接符的拼接
concat_ws(':',collect_set(ext))   去重的拼接
row_number() over (partition by keycode,onkey order by cast(read as int) desc)  分组排序
a LATERAL VIEW explode(split(wordkey, ',')) aa as onkey  列才分成多行
```














