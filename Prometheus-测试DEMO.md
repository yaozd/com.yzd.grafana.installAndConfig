### A.参考的项目
- 1.[spring-boot-metrics-to-influxdb](https://github.com/yaozd/spring-boot-metrics-to-influxdb.git)-(dev-yzd)-版本：influxdb-1.5.2.x86_64.rpm （百度云有备份）
- 2.[consul-client](https://github.com/yaozd/consul-client)-版本：Consul 1.2.2
- 3.[jmx_exporter](https://github.com/prometheus/jmx_exporter)-(prometheus)-版本：jmx_prometheus_javaagent-0.3.1.jar

### B.Consul-安装

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


### C.Prometheus-采集JAVA示例
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
config.yaml的配置模板（byArvin推荐config.yaml中不加过多配置使其保持简单与稳定）
```
startDelaySeconds: 0
#hostPort: 127.0.0.1:1234#监控当前jar包的metrics信息。不需要添加hostPort信息
===
注：config.yaml中不需要配置hostPort信息，hostPort信息代指远程jar程序的端口。
```

### D.Prometheus通过consul实现自动发现
```
com.yzd.jutils下：
com.yzd.jutils.consul->ConsulTest
<!--consul-client begin-->
<dependency>
   <groupId>com.orbitz.consul</groupId>
   <artifactId>consul-client</artifactId>
   <version>1.2.3</version>
</dependency>
<!--consul-client end-->
```
### D.Prometheus的数据收集，保存在influxdb中grafana再显示
```
注：匹配代码暂时没有实现，可参考此项目
[spring-boot-metrics-to-influxdb](https://github.com/yaozd/spring-boot-metrics-to-influxdb.git)-(dev-yzd)

```