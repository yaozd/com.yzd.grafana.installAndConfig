### 1.[Prometheus ϵͳ��ط���һ����](http://www.cnblogs.com/vovlie/p/Prometheus_CONCEPTS.html)
```
1.
Prometheus��һ�׿�Դ�ļ��&����&ʱ���������ݿ����ϣ���ʼ����SoundCloud��˾�����ġ����ŷ�չ��Խ��Խ�๫˾����֯���ܲ���Prometheus������Ҳʮ�ֻ�Ծ�����Ǳ㽫�������ɿ�Դ��Ŀ�������й�˾��������google SRE������Ҳ���ᵽ������BorgMon���ϵͳ���Ƶ�ʵ����Prometheus�����������Kubernetes��������ϵͳ�У�ͨ�������Prometheus���м�ء�
Prometheus ���ŵ�
�ǳ��ٵ��ⲿ��������װʹ�ó���
�Ѿ��зǳ����ϵͳ���� ���磺docker HAProxy Nginx JMX�ȵ�
�����Զ�������
ֱ�Ӽ��ɵ�����
���˼���ǰ��շֲ�ʽ��΢����ܹ���ʵ�ֵ�
2.
Prometheus ��������������
Counter
Counter �����ۼ�ֵ������ ��¼ ��������������������������������
һֱ���ӣ�������١�
�������̺󣬻ᱻ���á�
���磺http_response_total{method="GET",endpoint="/api/tracks"} 100
10���ץȡ http_response_total{method="GET",endpoint="/api/tracks"} 100
==
Gauge
Gauge ������ֵ������ �¶ȱ仯���ڴ�ʹ�ñ仯��
�ɱ�󣬿ɱ�С��
�������̺󣬻ᱻ����
���磺 memory_usage_bytes{host="master-01"} 100 < ץȡֵ
memory_usage_bytes{host="master-01"} 30
memory_usage_bytes{host="master-01"} 50
memory_usage_bytes{host="master-01"} 80 < ץȡֵ
==
Histogram
Histogram �������Ϊ��״ͼ����˼�������ڸ����¼������Ĺ�ģ�����磺�����ʱ����Ӧ��С�����ر�֮���ǿ��ԶԼ�¼�����ݽ��з��飬�ṩ count �� sum ȫ��ֵ�Ĺ��ܡ�
���磺{С��10=5�Σ�С��20=1�Σ�С��30=2��}��count=7�Σ�sum=7�ε����ֵ
==
Summary
Summary��Histogramʮ�����ƣ������ڸ����¼������Ĺ�ģ�����磺�����ʱ����Ӧ��С��ͬ���ṩ count �� sum ȫ��ֵ�Ĺ��ܡ�
���磺count=7�Σ�sum=7�ε�ֵ��ֵ
���ṩһ��quantiles�Ĺ��ܣ����԰�%�Ȼ��ָ��ٵĽ�������磺quantileȡֵ0.95����ʾȡ����ֵ�����95%���ݡ�
��һ��˵˵Prometheus��װ���̡�
```
### Prometheus-���ݲɼ�����
```

```
### Prometheus-�ο�����
- 1.[Prometheus�ɼ��õ�exporter](https://blog.csdn.net/felix_yujing/article/details/75571073)
- 2.[����jmx_exporter��ȡkafka metrics����](https://blog.csdn.net/sweatott/article/details/79090175)
- 3.[Prometheus ͨ��consul��̬�޸�Targets����](https://blog.csdn.net/poorcoder_/article/details/79120218)
- 4.[����Prometheus����ά�ȵ��������](https://blog.csdn.net/zqg5258423/article/details/52714306?locationNum=2&fps=1)
- 5.[Consul+Prometheusϵͳ���֮������](https://www.jianshu.com/p/242c25332374)
- 6.[Prometheus���úͻ���Consul�ķ�����](http://ibash.cc/frontend/article/89/)
- 7.[�Զ���Metrics����Prometheus������Ӧ�ó���](http://dockone.io:82/article/3298)
- 8.[Prometheus ��� Nginx ���� (����](https://blog.csdn.net/u011537073/article/details/77455530)



### 2.Consul-INSTALL

1.Consul-run.bat
```
//-dev �����ǿ���ģ�岻�洢�ڴ��̣����ݴ洢���ڴ�
consul agent -dev
```
2.Consul-open-consul.bat
```
//Windows dos��
start http://127.0.0.1:8500/ui/dc1/services
```
�ο���[��΢����No.1��Consul��������windows�¼�ʹ��](https://www.cnblogs.com/yanbigfeg/p/9199590.html)


### Prometheus-�ɼ�JAVAʾ��
```
�ٶ���->Prometheus-�ɼ�JAVAʾ��-2018-09-05-bak.rar(ʾ������)
jmx_exporter(�汾jmx_prometheus_javaagent-0.3.1.jar)
https://github.com/prometheus/jmx_exporter

1.
java -XX:+UseG1GC -Xmx100m -Xms32m -jar app.discovery.service.jar
2.
java -javaagent:./jmx_prometheus_javaagent-0.3.1.jar=18080:config.yaml -jar .\ms-service-1.jar
==
java -javaagent:./jmx_prometheus_javaagent-0.3.1.jar=18080:config.yaml -XX:+UseG1GC -Xmx70m -Xms32m -jar .\ms-service-1.jar

//Windows dos��
start http://127.0.0.1:18080
```
### ��ذ���
```
1.
Jenkins: Performance and health overview
https://grafana.com/dashboards/306
2.
Kafka Exporter Overview
https://grafana.com/dashboards/7589
3.
����Ⱥ��ء�JMX exporter+Prometheus+Grafana���Hadoop��Ⱥ
4.


```
### [Prometheus�ɼ��õ�exporter](https://blog.csdn.net/felix_yujing/article/details/75571073)
```
1.
[Prometheus�ɼ��õ�exporter](https://blog.csdn.net/felix_yujing/article/details/75571073)
2.
[����Prometheus����ά�ȵ��������](https://blog.csdn.net/zqg5258423/article/details/52714306?locationNum=2&fps=1)
��prometheus�Ĺ�����https://prometheus.io/download/ �������ص��ܶ�����exporter�ɼ����� 
blackbox_exporter 
consul_exporter 
graphite_exporter 
haproxy_exporter 
memcached_exporter 
mysqld_exporter 
node_exporter 
pushgateway 
statsd_exporter
Node/system metrics exporter
AWS CloudWatch exporter
Blackbox exporter
Collectd exporter
Consul exporter
Graphite exporter
HAProxy exporter
InfluxDB exporter
JMX exporter
Memcached exporter
Mesos task exporter
MySQL server exporter
SNMP exporter
StatsD exporter

����֮�⣬���кܶ�������ṩ��exporter�ɼ�������������һ������֪���ġ���һ��ù�ʲô�ȽϺõģ�Ҳ����һ�����һ�¡�

https://github.com/percona/mongodb_exporter

https://github.com/wrouesnel/postgres_exporter

https://github.com/prometheus/jmx_exporter 
jmx_prometheus_httpserver 
http://central.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_httpserver/ 
jmx_prometheus_javaagent 
http://central.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/

https://github.com/oliver006/redis_exporter 
������һ�£��о�metricsָ���е��٣���grafana��dashboard����Ĳ�ƥ�䡣��

https://github.com/lovoo/jenkins_exporter
```