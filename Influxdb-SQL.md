# Influxdb sql���
### Left join in influx DB
```
Left join in influx DB
https://stackoverflow.com/questions/26376807/left-join-in-influx-db
influx-db�������ϵ�����ݿ�ʹ��join����
select * from statistics as s inner join browsers as b where s.browser_type_id  = b.id
��influx-db����ʹ����ͬ��ʱ�����н���join����
You cannot join series in InfluxDB using arbitrary columns. InfluxDB only supports joining time series based on the time column. This is a special type of join unlike the one you're used to in relational databases. Time join in InfluxDB tries to correlate points from different time series that happened at approximately the same time. You can read more about joins in InfluxDB in the docs
https://influxdb.com/docs/v0.8/api/query_language.html#joining-series

```
### Influxdb sql���
1. [��תʱ�����ݿ�InfluxDB](http://www.ywnds.com/?p=10763)-�Ƽ�byArvin

```
# ��������������;
select * from /.*/ limit 1
 
# ���Json��ʽ;
$ influx -database 'test' -execute 'select * from disk' -format 'json' -pretty
 
# ��ѯ���ݴ���200��;
select * from disk where free > 80
 
# ��ѯ�������溬�������ַ�����;
select * from user_events where url_base = ��friends#show��
 
# Լ����;
select line from log_lines where line =~ /paul@influx.com/
 
# ����30m���ӽ��оۺϣ�ʱ�䷶Χ�Ǵ����������������server1��;
select mean(value) from cpu_idle group by time(30m) where time > now() �C 1d and hostName = 'server1'
select column_one  from foo  where time > now() �C 1h limit 1000;
select reqtime, url from web9999.httpd where reqtime > 2.5;
select reqtime, url from web9999.httpd where time > now() �C 1h limit 1000;
 
# url�������溬��login�����ۣ�����login��ͷ;
select reqtime, url from web9999.httpd where url =~ /^\/login\//;
 
# ���ݵ�merge;
select reqtime, url from web9999.httpd merge web0001.httpd;

������˵�����ݵĻ�ۣ��ۺ�ɶ�ġ�

# count();
SELECT COUNT(column_name) FROM series_name group by time(10m) ��

# min();
SELECT MIN(column_name) FROM series_name group by time(10m) ��

# MAX();
SELECT MAX(column_name) FROM series_name group by time(10m) ��

# mean();
SELECT MEAN(column_name) FROM series_name group by time(10m) ��

# count();
SELECT COUNT(column_name) FROM series_name group by time(10m) ��
 
# min();
SELECT MIN(column_name) FROM series_name group by time(10m) ��
 
# MAX();
SELECT MAX(column_name) FROM series_name group by time(10m) ��
 
# mean();
SELECT MEAN(column_name) FROM series_name group by time(10m) ��
```
1. [influxdb����SQL����](https://blog.csdn.net/gongpulin/article/details/81103515)-�Ƽ�byArvin

```
influxdb����SQL����
https://blog.csdn.net/gongpulin/article/details/81103515
```