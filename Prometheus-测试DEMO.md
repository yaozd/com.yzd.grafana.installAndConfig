### A.�ο�����Ŀ
- 1.[spring-boot-metrics-to-influxdb](https://github.com/yaozd/spring-boot-metrics-to-influxdb.git)-(dev-yzd)-�汾��influxdb-1.5.2.x86_64.rpm ���ٶ����б��ݣ�
- 2.[consul-client](https://github.com/yaozd/consul-client)-�汾��Consul 1.2.2
- 3.[jmx_exporter](https://github.com/prometheus/jmx_exporter)-(prometheus)-�汾��jmx_prometheus_javaagent-0.3.1.jar

### B.Consul-��װ

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


### C.Prometheus-�ɼ�JAVAʾ��
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
config.yaml������ģ�壨byArvin�Ƽ�config.yaml�в��ӹ�������ʹ�䱣�ּ����ȶ���
```
startDelaySeconds: 0
#hostPort: 127.0.0.1:1234#��ص�ǰjar����metrics��Ϣ������Ҫ���hostPort��Ϣ
===
ע��config.yaml�в���Ҫ����hostPort��Ϣ��hostPort��Ϣ��ָԶ��jar����Ķ˿ڡ�
```

### D.Prometheusͨ��consulʵ���Զ�����
```
com.yzd.jutils�£�
com.yzd.jutils.consul->ConsulTest
<!--consul-client begin-->
<dependency>
   <groupId>com.orbitz.consul</groupId>
   <artifactId>consul-client</artifactId>
   <version>1.2.3</version>
</dependency>
<!--consul-client end-->
```
### D.Prometheus�������ռ���������influxdb��grafana����ʾ
```
ע��ƥ�������ʱû��ʵ�֣��ɲο�����Ŀ
[spring-boot-metrics-to-influxdb](https://github.com/yaozd/spring-boot-metrics-to-influxdb.git)-(dev-yzd)

```