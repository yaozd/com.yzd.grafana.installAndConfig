## Grafana版本-5.1.4
### Grafana-Graph-lines-不显示内容
```
Graph->Display->
Null value默认值：null,把null调整为connected
==
```

### $timeFilter 
```
The $timeFilter or $__timeFilter Variable
1.老版本
$timeFilter
2.新版本
$__timeFilter
eg:
$timefilter返回当前选择的时间范围为表达。
例如，time range表达时间为Last 7 days ，表达式为time > now() - 7d。
Grafana 会自动添加 $timeFilter,influxDB需要手动添加
如果你使用原始查询，请至少确保where有$timeFilter，也总用时间区间和聚合函数功能。 否则InfluxDB 很容易返回成千上万数据点提供浏览。
参考：
Using InfluxDB in Grafana,influxDB在grafana中使用
https://www.cnblogs.com/michellexiaoqi/p/7271880.html
```
### $interval 
```
The $interval or $__$interval Variable
1.老版本
$$interval
2.新版本
$__$interval
eg:
For relatively short time range(24 hours) 5 min resolution is OK and query might look like:
SELECT sum(“bytes_per_5min”)*8/300 as ‘bitrate’ FROM “SomeMeasurement” WHERE $timeFilter GROUP BY time(5m),“device” fill(null)
For longer time range (90 days) 5 minutes steps are usually not needed and 1day steps might be enough.
So, the query should look like:
SELECT sum(“bytes_per_5min”)*8/86400 FROM “SomeMeasurement” WHERE $timeFilter GROUP BY time(1d),“device” fill(null)
==
$interval:没有特别指定，默认是5分钟，$interval与auto一个意思 :group by time(5m) 或者group by time(auto)
设置这边可以改变$interval的值。我这写的时候 基本要大于5分钟，目前不是很清楚原因。
Group by time是很重要的，否则Grafana查询会返回成千上万的数据点会慢下来。
对于每个查询，将时间字段分组为空，并根据图的时间范围和像素宽度计算该组。
如果使用fill（0）或fill（null），则按时间间隔为自动组设置一个低限
下限只能在您查询的按组时间选项中设置。
在间隔之前添加一个更大的符号来设置一个下限。
例如：如果InfluxDB的metrics 为每60秒
参考：
Time(interval) grouping and data scaling
https://community.grafana.com/t/time-interval-grouping-and-data-scaling/154
Using InfluxDB in Grafana,influxDB在grafana中使用
https://www.cnblogs.com/michellexiaoqi/p/7271880.html
```
