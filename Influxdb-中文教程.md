### [Influxdb-���Ľ̳�](https://www.cnblogs.com/michellexiaoqi/category/1044214.html)
1. [influxDB����](https://www.cnblogs.com/michellexiaoqi/p/7259121.html)
2. [influxDB �任�ຯ��](https://www.cnblogs.com/michellexiaoqi/p/7249766.html)
3. [influxDB�ۺ��ຯ��](https://www.cnblogs.com/michellexiaoqi/p/7256005.html)
4. [influxDBѡ���ຯ��](https://www.cnblogs.com/michellexiaoqi/p/7256282.html)
5. [Using InfluxDB in Grafana,influxDB��grafana��ʹ��](https://www.cnblogs.com/michellexiaoqi/p/7271880.html)
6. [influxDB---Data Exploration](https://www.cnblogs.com/michellexiaoqi/p/7297489.html)
7. [influxDB---���ݿ����SQL](https://www.cnblogs.com/michellexiaoqi/p/7338913.html)

### Influxdb����ͳ�����
```
���ԣ�spring-boot-metrics-to-influxdb��dev-yzd��֧
https://github.com/yaozd/spring-boot-metrics-to-influxdb.git
1.heap��ͳ�ƣ�
SELECT mean("heap") FROM "microservice_status" WHERE ("serviceId" =~ /^$app$/) AND $timeFilter GROUP BY time($interval) fill(null)
2.heap.used��ͳ�ƣ�
SELECT mean("heap.used") FROM "microservice_status" WHERE ("serviceId" =~ /^$app$/) AND $timeFilter GROUP BY time($interval) fill(null)
3.young.gc.count(30s)��ͳ�ƣ�spring boot��ֻ�ṩ��GC�ռ����ܴ�������
SELECT LAST("young.gc.count") -FIRST("young.gc.count") FROM "microservice_status" WHERE ("serviceId" =~ /^$app$/) and time > now() - 1h GROUP BY time(30s) fill(null)
4.young.gc.time(30s)��ͳ�ƣ�spring boot��ֻ�ṩ��GC�ռ�����ʱ�䣩��
SELECT LAST("young.gc.time") -FIRST("young.gc.time") FROM "microservice_status" WHERE ("serviceId" =~ /^$app$/) and time > now() - 1h GROUP BY time(30s) fill(null)

```

```
��ʷ��� - influxDB
influxDB---���ݿ����SQL
ժҪ: ��ѯ ��ѯ����ֻ��tag��ǩ��һ��Ҫ����fields�� �磺select val,"����" FROM "���Ա�" WHERE dev = 'cs123' and time> now() - 20m ֱ��д:select "����" FROM "���Ա�" WHERE dev = 'cs123' and �Ķ�ȫ��
posted @ 2017-08-10 13:59 michellexiaoqi �Ķ�(69) | ���� (0) �༭
influxDB---Data Exploration
ժҪ: the group clause group by ���صķ������Ǹ����û�ָ����tag ,time interval�� 1��group by tags 2��group by time intervals group by time()�����ѯ�����û�ָ��ʱ������� �﷨�� Description�Ķ�ȫ��
posted @ 2017-08-07 09:06 michellexiaoqi �Ķ�(79) | ���� (0) �༭
Using InfluxDB in Grafana,influxDB��grafana��ʹ��
ժҪ: grafana���й��ܷḻ������Դ���influxDB��֧�ַḻ�Ĳ�ѯ�༭����ע�ͺ�templating��ģ�棩��ѯ�� ��������Դ��Adding the data source�� Edit/ADD data source name :����Դ���ơ�����������Ͳ�ѯ����������Դ�ķ�ʽ�� defalut�Ķ�ȫ��
posted @ 2017-08-02 08:26 michellexiaoqi �Ķ�(492) | ���� (0) �༭
influxDB����
ժҪ: һ���������� 1��database--���ݿ⣬���ͬ��ͳ���ݿ�����ݿ��� 2��measurement--���ݱ���InfluxDB�У�measurement��Ϊ������ã�ͬ��ͳ���ݿ��е�table����һ�¡� �������봫ͳ���ݿ��е��������Ƚ� ����InfluxDB���и��� 1��tag--��ǩ����I�Ķ�ȫ��
posted @ 2017-07-30 14:42 michellexiaoqi �Ķ�(98) | ���� (0) �༭
influxDBѡ���ຯ��
ժҪ: 1��TOP()���� ���ã�����һ���ֶ�������N��ֵ���ֶ����ͱ����ǳ����ͻ�float64���͡� �﷨�� N = 3 N = 1 2��BOTTOM()���� ���ã�����һ���ֶ�����С��N��ֵ���ֶ����ͱ����ǳ����ͻ�float64���͡� �﷨�� N = 1 3��FIRST()���� ���ã�����һ���ֶ������Ķ�ȫ��
posted @ 2017-07-29 16:22 michellexiaoqi �Ķ�(440) | ���� (0) �༭
influxDB�ۺ��ຯ��
ժҪ: 1��count()���� ����һ����field���ֶ��еķǿ�ֵ�������� ˵�� water_level����ֶ��� h2o_feet���й���15258�����ݡ� ע�⣺�ۺϺ��������û��ָ��ʱ��Ļ�����Ĭ���� epoch 0 (1970-01-01T00:00:00Z) ��Ϊʱ�䡣 ������where �м����Ķ�ȫ��
posted @ 2017-07-29 15:14 michellexiaoqi �Ķ�(670) | ���� (0) �༭
influxDB �任�ຯ��
ժҪ: 1��DERIVATIVE()���� ���ã�����һ���ֶ���һ��series�еı仯�ʡ� InfluxDB����㰴��ʱ�����������ֶ�ֵ֮��Ĳ��죬������Щ���ת��Ϊ��λ�仯�ʡ����У���λ����ָ����Ĭ��Ϊ1s�� �﷨�� ���У�unitȡֵ����Ϊ���¼��֣� DERIVATIVE()������������GROUP B�Ķ�ȫ��
posted @ 2017-07-28 13:43 michellexiaoqi �Ķ�(1403) | ���� (0) �༭
```

### ע������
```
1.
��ѯ
��ѯ����ֻ��tag��ǩ��һ��Ҫ����fields��
�磺select val,"����" FROM "���Ա�" WHERE dev = 'cs123' and time> now() - 20m 
ֱ��д:select "����" FROM "���Ա�" WHERE dev = 'cs123' and time> now() - 20m ,���ݿⲻ����ʾ���ݡ�
2.
group by ���صķ������Ǹ����û�ָ����tag ,time interval��
1��group by tags
2��group by time intervals
group by time()�����ѯ�����û�ָ��ʱ�������
���������ʹ�������ʾ������������
> SELECT "water_level","location" FROM "h2o_feet" WHERE time >= '2015-08-18T00:00:00Z' AND time <= '2015-08-18T00:30:00Z'
```