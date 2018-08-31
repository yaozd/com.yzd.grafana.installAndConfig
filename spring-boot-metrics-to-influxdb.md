# InfluxDBʾ���ο�����
## Collect the metric spring-actuator and send them to the InfluxDB
1.[spring-boot-metrics-to-influxdb](https://github.com/ypvillazon/spring-boot-metrics-to-influxdb)

```
spring-boot-metrics-to-influxdb
https://github.com/ypvillazon/spring-boot-metrics-to-influxdb
https://github.com/yaozd/spring-boot-metrics-to-influxdb�����ݣ�
```

2.[gasmiddleware](https://github.com/JupiterMouse/gasmiddleware)

```
gasmiddleware
ȼ�����ϵͳ�м�����֡�kafka��Influxdb��haselcast��lombok��devtools��actuator
https://github.com/JupiterMouse/gasmiddleware
https://github.com/yaozd/gasmiddleware�����ݣ�

```
3.spring boot 1.x�ĸ�������ָ��˵��
```
spring-boot �ٳ�(3) actuator
https://www.cnblogs.com/yjmyzz/p/spring-boot-actuator-tutorial.html
http://localhost:1101/admin/metrics ���Կ����������������
{
    mem: 466881,
    mem.free: 289887,
    processors: 4,
    instance.uptime: 10947,
    uptime: 18135,
    systemload.average: 3.12646484375,
    heap.committed: 411648,
    heap.init: 131072,
    heap.used: 121760,
    heap: 1864192,
    nonheap.committed: 56192,
    nonheap.init: 2496,
    nonheap.used: 55234,
    nonheap: 0,
    threads.peak: 27,
    threads.daemon: 19,
    threads.totalStarted: 32,
    threads: 22,
    classes: 6755,
    classes.loaded: 6755,
    classes.unloaded: 0,
    gc.ps_scavenge.count: 8,
    gc.ps_scavenge.time: 136,
    gc.ps_marksweep.count: 2,
    gc.ps_marksweep.time: 193,
    httpsessions.max: -1,
    httpsessions.active: 0
}
jvm���ڴ棬cpu�������߳�����gc���һĿ��Ȼ������ָ���ź�������(���ϳ�����)

ϵͳ��Ϣ��
    ��������������processors������ʱ��uptime��instance.uptime��ϵͳƽ������systemload.average��
mem.*��
    �ڴ��Ҫ��Ϣ�����������Ӧ�õ����ڴ������Լ���ǰ���е��ڴ���������Щ��Ϣ����java.lang.Runtime��
heap.*��
    ���ڴ�ʹ���������Щ��Ϣ����java.lang.management.MemoryMXBean�ӿ���getHeapMemoryUsage������ȡ��java.lang.management.MemoryUsage��
nonheap.*��
    �Ƕ��ڴ�ʹ���������Щ��Ϣ����java.lang.management.MemoryMXBean�ӿ���getNonHeapMemoryUsage������ȡ��java.lang.management.MemoryUsage��
threads.*��
    �߳�ʹ������������߳������ػ��߳�����daemon�����̷߳�ֵ��peak���ȣ���Щ���ݾ�����java.lang.management.ThreadMXBean��
classes.*��
    Ӧ�ü��غ�ж�ص���ͳ�ơ���Щ���ݾ�����java.lang.management.ClassLoadingMXBean��
gc.*��
    �����ռ�������ϸ��Ϣ�������������մ���gc.ps_scavenge.count��������������ʱ��gc.ps_scavenge.time�����-����㷨�Ĵ���gc.ps_marksweep.count�����-����㷨������ʱ��gc.ps_marksweep.time����Щ���ݾ�����java.lang.management.GarbageCollectorMXBean��
httpsessions.*��
    Tomcat�����ĻỰʹ��������������Ự��httpsessions.max�ͻ�Ծ�Ự��httpsessions.active���ö���ָ����Ϣ����������Ƕ��ʽTomcat��ΪӦ��������ʱ��Ż��ṩ��
gauge.*��
    HTTP���������ָ��֮һ������Ҫ������ӳһ��������ֵ����������ʾ���е�gauge.response.hello: 5������ʾ��һ��hello������ӳ�ʱ��Ϊ5���롣
counter.*��
    HTTP���������ָ��֮һ������Ҫ��Ϊ��������ʹ�ã���¼���������ͼ�����������ʾ����counter.status.200.hello: 11����������hello���󷵻�200״̬�Ĵ���Ϊ11

�������һЩ���߰���Щ��Ϣ�ɼ���grafana����еõ�һϵ�к�ʵ�õļ��ͼ�����ݣ����磺����
```