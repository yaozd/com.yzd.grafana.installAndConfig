### [Influxdb-中文教程](https://www.cnblogs.com/michellexiaoqi/category/1044214.html)
1. [influxDB概念](https://www.cnblogs.com/michellexiaoqi/p/7259121.html)
2. [influxDB 变换类函数](https://www.cnblogs.com/michellexiaoqi/p/7249766.html)
3. [influxDB聚合类函数](https://www.cnblogs.com/michellexiaoqi/p/7256005.html)
4. [influxDB选择类函数](https://www.cnblogs.com/michellexiaoqi/p/7256282.html)
5. [Using InfluxDB in Grafana,influxDB在grafana中使用](https://www.cnblogs.com/michellexiaoqi/p/7271880.html)
6. [influxDB---Data Exploration](https://www.cnblogs.com/michellexiaoqi/p/7297489.html)
7. [influxDB---数据库操作SQL](https://www.cnblogs.com/michellexiaoqi/p/7338913.html)

### Influxdb常用统计语句
```
来自：spring-boot-metrics-to-influxdb的dev-yzd分支
https://github.com/yaozd/spring-boot-metrics-to-influxdb.git
1.heap的统计：
SELECT mean("heap") FROM "microservice_status" WHERE ("serviceId" =~ /^$app$/) AND $timeFilter GROUP BY time($interval) fill(null)
2.heap.used的统计：
SELECT mean("heap.used") FROM "microservice_status" WHERE ("serviceId" =~ /^$app$/) AND $timeFilter GROUP BY time($interval) fill(null)
3.young.gc.count(30s)的统计（spring boot中只提供了GC收集的总次数）：
SELECT LAST("young.gc.count") -FIRST("young.gc.count") FROM "microservice_status" WHERE ("serviceId" =~ /^$app$/) and time > now() - 1h GROUP BY time(30s) fill(null)
4.young.gc.time(30s)的统计（spring boot中只提供了GC收集的总时间）：
SELECT LAST("young.gc.time") -FIRST("young.gc.time") FROM "microservice_status" WHERE ("serviceId" =~ /^$app$/) and time > now() - 1h GROUP BY time(30s) fill(null)

```

```
随笔分类 - influxDB
influxDB---数据库操作SQL
摘要: 查询 查询不能只查tag标签，一定要加上fields。 如：select val,"班组" FROM "测试表" WHERE dev = 'cs123' and time> now() - 20m 直接写:select "班组" FROM "测试表" WHERE dev = 'cs123' and 阅读全文
posted @ 2017-08-10 13:59 michellexiaoqi 阅读(69) | 评论 (0) 编辑
influxDB---Data Exploration
摘要: the group clause group by 返回的分组结果是根据用户指定的tag ,time interval。 1、group by tags 2、group by time intervals group by time()分组查询返回用户指定时间间隔结果 语法： Description阅读全文
posted @ 2017-08-07 09:06 michellexiaoqi 阅读(79) | 评论 (0) 编辑
Using InfluxDB in Grafana,influxDB在grafana中使用
摘要: grafana带有功能丰富的数据源插件influxDB。支持丰富的查询编辑器、注释和templating（模版）查询。 增加数据源（Adding the data source） Edit/ADD data source name :数据源名称。这就是在面板和查询中引用数据源的方式。 defalut阅读全文
posted @ 2017-08-02 08:26 michellexiaoqi 阅读(492) | 评论 (0) 编辑
influxDB概念
摘要: 一、基本概念 1）database--数据库，这个同传统数据库的数据库概念。 2）measurement--数据表，在InfluxDB中，measurement即为表的作用，同传统数据库中的table作用一致。 二、、与传统数据库中的名词做比较 三、InfluxDB特有概念 1）tag--标签，在I阅读全文
posted @ 2017-07-30 14:42 michellexiaoqi 阅读(98) | 评论 (0) 编辑
influxDB选择类函数
摘要: 1）TOP()函数 作用：返回一个字段中最大的N个值，字段类型必须是长整型或float64类型。 语法： N = 3 N = 1 2、BOTTOM()函数 作用：返回一个字段中最小的N个值。字段类型必须是长整型或float64类型。 语法： N = 1 3）FIRST()函数 作用：返回一个字段中最阅读全文
posted @ 2017-07-29 16:22 michellexiaoqi 阅读(440) | 评论 (0) 编辑
influxDB聚合类函数
摘要: 1）count()函数 返回一个（field）字段中的非空值的数量。 说明 water_level这个字段在 h2o_feet表中共有15258条数据。 注意：聚合函数中如果没有指定时间的话，会默认以 epoch 0 (1970-01-01T00:00:00Z) 作为时间。 可以在where 中加入阅读全文
posted @ 2017-07-29 15:14 michellexiaoqi 阅读(670) | 评论 (0) 编辑
influxDB 变换类函数
摘要: 1、DERIVATIVE()函数 作用：返回一个字段在一个series中的变化率。 InfluxDB会计算按照时间进行排序的字段值之间的差异，并将这些结果转化为单位变化率。其中，单位可以指定，默认为1s。 语法： 其中，unit取值可以为以下几种： DERIVATIVE()函数还可以在GROUP B阅读全文
posted @ 2017-07-28 13:43 michellexiaoqi 阅读(1403) | 评论 (0) 编辑
```

### 注意事项
```
1.
查询
查询不能只查tag标签，一定要加上fields。
如：select val,"班组" FROM "测试表" WHERE dev = 'cs123' and time> now() - 20m 
直接写:select "班组" FROM "测试表" WHERE dev = 'cs123' and time> now() - 20m ,数据库不会显示数据。
2.
group by 返回的分组结果是根据用户指定的tag ,time interval。
1、group by tags
2、group by time intervals
group by time()分组查询返回用户指定时间间隔结果
下面的例子使用下面的示例数据样本：
> SELECT "water_level","location" FROM "h2o_feet" WHERE time >= '2015-08-18T00:00:00Z' AND time <= '2015-08-18T00:30:00Z'
```