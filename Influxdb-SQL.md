# Influxdb sql语句
### Left join in influx DB
```
Left join in influx DB
https://stackoverflow.com/questions/26376807/left-join-in-influx-db
influx-db不能像关系型数据库使用join连接
select * from statistics as s inner join browsers as b where s.browser_type_id  = b.id
但influx-db可以使用相同的时间序列进行join连接
You cannot join series in InfluxDB using arbitrary columns. InfluxDB only supports joining time series based on the time column. This is a special type of join unlike the one you're used to in relational databases. Time join in InfluxDB tries to correlate points from different time series that happened at approximately the same time. You can read more about joins in InfluxDB in the docs
https://influxdb.com/docs/v0.8/api/query_language.html#joining-series

```
### Influxdb sql语句
1. [玩转时序数据库InfluxDB](http://www.ywnds.com/?p=10763)-推荐byArvin

```
# 表名都可以正则;
select * from /.*/ limit 1
 
# 输出Json格式;
$ influx -database 'test' -execute 'select * from disk' -format 'json' -pretty
 
# 查询数据大于200的;
select * from disk where free > 80
 
# 查询数据里面含有下面字符串的;
select * from user_events where url_base = ‘friends#show’
 
# 约等于;
select line from log_lines where line =~ /paul@influx.com/
 
# 按照30m分钟进行聚合，时间范围是大于昨天的主机名是server1的;
select mean(value) from cpu_idle group by time(30m) where time > now() – 1d and hostName = 'server1'
select column_one  from foo  where time > now() – 1h limit 1000;
select reqtime, url from web9999.httpd where reqtime > 2.5;
select reqtime, url from web9999.httpd where time > now() – 1h limit 1000;
 
# url搜索里面含有login的字眼，还以login开头;
select reqtime, url from web9999.httpd where url =~ /^\/login\//;
 
# 数据的merge;
select reqtime, url from web9999.httpd merge web0001.httpd;

下面再说下数据的汇聚，聚合啥的。

# count();
SELECT COUNT(column_name) FROM series_name group by time(10m) …

# min();
SELECT MIN(column_name) FROM series_name group by time(10m) …

# MAX();
SELECT MAX(column_name) FROM series_name group by time(10m) …

# mean();
SELECT MEAN(column_name) FROM series_name group by time(10m) …

# count();
SELECT COUNT(column_name) FROM series_name group by time(10m) …
 
# min();
SELECT MIN(column_name) FROM series_name group by time(10m) …
 
# MAX();
SELECT MAX(column_name) FROM series_name group by time(10m) …
 
# mean();
SELECT MEAN(column_name) FROM series_name group by time(10m) …
```
1. [influxdb基本SQL操作](https://blog.csdn.net/gongpulin/article/details/81103515)-推荐byArvin

```
influxdb基本SQL操作
https://blog.csdn.net/gongpulin/article/details/81103515
```