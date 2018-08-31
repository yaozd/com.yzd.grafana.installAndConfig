## Grafana�汾-5.1.4
### Grafana-Graph-lines-����ʾ����
```
Graph->Display->
Null valueĬ��ֵ��null,��null����Ϊconnected
==
```

### $timeFilter 
```
The $timeFilter or $__timeFilter Variable
1.�ϰ汾
$timeFilter
2.�°汾
$__timeFilter
eg:
$timefilter���ص�ǰѡ���ʱ�䷶ΧΪ��
���磬time range���ʱ��ΪLast 7 days �����ʽΪtime > now() - 7d��
Grafana ���Զ���� $timeFilter,influxDB��Ҫ�ֶ����
�����ʹ��ԭʼ��ѯ��������ȷ��where��$timeFilter��Ҳ����ʱ������;ۺϺ������ܡ� ����InfluxDB �����׷��س�ǧ�������ݵ��ṩ�����
�ο���
Using InfluxDB in Grafana,influxDB��grafana��ʹ��
https://www.cnblogs.com/michellexiaoqi/p/7271880.html
```
### $interval 
```
The $interval or $__$interval Variable
1.�ϰ汾
$$interval
2.�°汾
$__$interval
eg:
For relatively short time range(24 hours) 5 min resolution is OK and query might look like:
SELECT sum(��bytes_per_5min��)*8/300 as ��bitrate�� FROM ��SomeMeasurement�� WHERE $timeFilter GROUP BY time(5m),��device�� fill(null)
For longer time range (90 days) 5 minutes steps are usually not needed and 1day steps might be enough.
So, the query should look like:
SELECT sum(��bytes_per_5min��)*8/86400 FROM ��SomeMeasurement�� WHERE $timeFilter GROUP BY time(1d),��device�� fill(null)
==
$interval:û���ر�ָ����Ĭ����5���ӣ�$interval��autoһ����˼ :group by time(5m) ����group by time(auto)
������߿��Ըı�$interval��ֵ������д��ʱ�� ����Ҫ����5���ӣ�Ŀǰ���Ǻ����ԭ��
Group by time�Ǻ���Ҫ�ģ�����Grafana��ѯ�᷵�س�ǧ��������ݵ����������
����ÿ����ѯ����ʱ���ֶη���Ϊ�գ�������ͼ��ʱ�䷶Χ�����ؿ�ȼ�����顣
���ʹ��fill��0����fill��null������ʱ����Ϊ�Զ�������һ������
����ֻ��������ѯ�İ���ʱ��ѡ�������á�
�ڼ��֮ǰ���һ������ķ���������һ�����ޡ�
���磺���InfluxDB��metrics Ϊÿ60��
�ο���
Time(interval) grouping and data scaling
https://community.grafana.com/t/time-interval-grouping-and-data-scaling/154
Using InfluxDB in Grafana,influxDB��grafana��ʹ��
https://www.cnblogs.com/michellexiaoqi/p/7271880.html
```
