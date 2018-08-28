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