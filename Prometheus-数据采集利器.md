### 1.[Prometheus 系统监控方案一介绍](http://www.cnblogs.com/vovlie/p/Prometheus_CONCEPTS.html)
```
1.
Prometheus是一套开源的监控&报警&时间序列数据库的组合，起始是由SoundCloud公司开发的。随着发展，越来越多公司和组织接受采用Prometheus，社区也十分活跃，他们便将它独立成开源项目，并且有公司来运作。google SRE的书内也曾提到跟他们BorgMon监控系统相似的实现是Prometheus。现在最常见的Kubernetes容器管理系统中，通常会搭配Prometheus进行监控。
Prometheus 的优点
非常少的外部依赖，安装使用超简单
已经有非常多的系统集成 例如：docker HAProxy Nginx JMX等等
服务自动化发现
直接集成到代码
设计思想是按照分布式、微服务架构来实现的
2.
Prometheus 的四种数据类型
Counter
Counter 用于累计值，例如 记录 请求次数、任务完成数、错误发生次数。
一直增加，不会减少。
重启进程后，会被重置。
例如：http_response_total{method="GET",endpoint="/api/tracks"} 100
10秒后抓取 http_response_total{method="GET",endpoint="/api/tracks"} 100
==
Gauge
Gauge 常规数值，例如 温度变化、内存使用变化。
可变大，可变小。
重启进程后，会被重置
例如： memory_usage_bytes{host="master-01"} 100 < 抓取值
memory_usage_bytes{host="master-01"} 30
memory_usage_bytes{host="master-01"} 50
memory_usage_bytes{host="master-01"} 80 < 抓取值
==
Histogram
Histogram 可以理解为柱状图的意思，常用于跟踪事件发生的规模，例如：请求耗时、响应大小。它特别之处是可以对记录的内容进行分组，提供 count 和 sum 全部值的功能。
例如：{小于10=5次，小于20=1次，小于30=2次}，count=7次，sum=7次的求和值
==
Summary
Summary和Histogram十分相似，常用于跟踪事件发生的规模，例如：请求耗时、响应大小。同样提供 count 和 sum 全部值的功能。
例如：count=7次，sum=7次的值求值
它提供一个quantiles的功能，可以按%比划分跟踪的结果。例如：quantile取值0.95，表示取采样值里面的95%数据。
下一章说说Prometheus安装过程。
```
### Prometheus-数据采集利器
```

```
### Prometheus-参考文章
- 1.[Prometheus采集用的exporter](https://blog.csdn.net/felix_yujing/article/details/75571073)
- 2.[利用jmx_exporter获取kafka metrics数据](https://blog.csdn.net/sweatott/article/details/79090175)
- 3.[Prometheus 通过consul动态修改Targets接入](https://blog.csdn.net/poorcoder_/article/details/79120218)
- 4.[基于Prometheus做多维度的容器监控](https://blog.csdn.net/zqg5258423/article/details/52714306?locationNum=2&fps=1)
- 5.[Consul+Prometheus系统监控之服务发现](https://www.jianshu.com/p/242c25332374)
- 6.[Prometheus配置和基于Consul的服务发现](http://ibash.cc/frontend/article/89/)
- 7.[自定义Metrics：让Prometheus监控你的应用程序](http://dockone.io:82/article/3298)
- 8.[Prometheus 监控 Nginx 流量 (三）](https://blog.csdn.net/u011537073/article/details/77455530)



### 2.Consul-INSTALL

1.Consul-run.bat
```
//-dev 代表是开发模板不存储在磁盘，数据存储在内存
consul agent -dev
```
2.Consul-open-consul.bat
```
//Windows dos下
start http://127.0.0.1:8500/ui/dc1/services
```
参考：[【微服务No.1】Consul服务发现在windows下简单使用](https://www.cnblogs.com/yanbigfeg/p/9199590.html)


### Prometheus-采集JAVA示例
```
百度云->Prometheus-采集JAVA示例-2018-09-05-bak.rar(示例代码)
jmx_exporter(版本jmx_prometheus_javaagent-0.3.1.jar)
https://github.com/prometheus/jmx_exporter

1.
java -XX:+UseG1GC -Xmx100m -Xms32m -jar app.discovery.service.jar
2.
java -javaagent:./jmx_prometheus_javaagent-0.3.1.jar=18080:config.yaml -jar .\ms-service-1.jar
==
java -javaagent:./jmx_prometheus_javaagent-0.3.1.jar=18080:config.yaml -XX:+UseG1GC -Xmx70m -Xms32m -jar .\ms-service-1.jar

//Windows dos下
start http://127.0.0.1:18080
```
### 监控案例
```
1.
Jenkins: Performance and health overview
https://grafana.com/dashboards/306
2.
Kafka Exporter Overview
https://grafana.com/dashboards/7589
3.
【集群监控】JMX exporter+Prometheus+Grafana监控Hadoop集群
4.


```
### [Prometheus采集用的exporter](https://blog.csdn.net/felix_yujing/article/details/75571073)
```
1.
[Prometheus采集用的exporter](https://blog.csdn.net/felix_yujing/article/details/75571073)
2.
[基于Prometheus做多维度的容器监控](https://blog.csdn.net/zqg5258423/article/details/52714306?locationNum=2&fps=1)
在prometheus的官网上https://prometheus.io/download/ 可以下载到很多服务的exporter采集器： 
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

除此之外，还有很多第三方提供的exporter采集器，这里整理一下我所知道的。大家还用过什么比较好的，也可以一起分享一下。

https://github.com/percona/mongodb_exporter

https://github.com/wrouesnel/postgres_exporter

https://github.com/prometheus/jmx_exporter 
jmx_prometheus_httpserver 
http://central.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_httpserver/ 
jmx_prometheus_javaagent 
http://central.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/

https://github.com/oliver006/redis_exporter 
试用了一下，感觉metrics指标有点少，和grafana的dashboard里面的不匹配。。

https://github.com/lovoo/jenkins_exporter
```