# InfluxDB示例参考代码
## Collect the metric spring-actuator and send them to the InfluxDB
1.[spring-boot-metrics-to-influxdb](https://github.com/ypvillazon/spring-boot-metrics-to-influxdb)

```
spring-boot-metrics-to-influxdb
https://github.com/ypvillazon/spring-boot-metrics-to-influxdb
https://github.com/yaozd/spring-boot-metrics-to-influxdb（备份）
```

2.[gasmiddleware](https://github.com/JupiterMouse/gasmiddleware)

```
gasmiddleware
燃气监测系统中间件部分。kafka、Influxdb、haselcast、lombok、devtools、actuator
https://github.com/JupiterMouse/gasmiddleware
https://github.com/yaozd/gasmiddleware（备份）

```
3.spring boot 1.x的各项运行指标说明
```
spring-boot 速成(3) actuator
https://www.cnblogs.com/yjmyzz/p/spring-boot-actuator-tutorial.html
http://localhost:1101/admin/metrics 可以看到类似以下输出：
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
jvm的内存，cpu核数，线程数，gc情况一目了然。其它指标大概含义如下(网上抄来的)

系统信息：
    包括处理器数量processors、运行时间uptime和instance.uptime、系统平均负载systemload.average。
mem.*：
    内存概要信息，包括分配给应用的总内存数量以及当前空闲的内存数量。这些信息来自java.lang.Runtime。
heap.*：
    堆内存使用情况。这些信息来自java.lang.management.MemoryMXBean接口中getHeapMemoryUsage方法获取的java.lang.management.MemoryUsage。
nonheap.*：
    非堆内存使用情况。这些信息来自java.lang.management.MemoryMXBean接口中getNonHeapMemoryUsage方法获取的java.lang.management.MemoryUsage。
threads.*：
    线程使用情况，包括线程数、守护线程数（daemon）、线程峰值（peak）等，这些数据均来自java.lang.management.ThreadMXBean。
classes.*：
    应用加载和卸载的类统计。这些数据均来自java.lang.management.ClassLoadingMXBean。
gc.*：
    垃圾收集器的详细信息，包括垃圾回收次数gc.ps_scavenge.count、垃圾回收消耗时间gc.ps_scavenge.time、标记-清除算法的次数gc.ps_marksweep.count、标记-清除算法的消耗时间gc.ps_marksweep.time。这些数据均来自java.lang.management.GarbageCollectorMXBean。
httpsessions.*：
    Tomcat容器的会话使用情况。包括最大会话数httpsessions.max和活跃会话数httpsessions.active。该度量指标信息仅在引入了嵌入式Tomcat作为应用容器的时候才会提供。
gauge.*：
    HTTP请求的性能指标之一，它主要用来反映一个绝对数值。比如上面示例中的gauge.response.hello: 5，它表示上一次hello请求的延迟时间为5毫秒。
counter.*：
    HTTP请求的性能指标之一，它主要作为计数器来使用，记录了增加量和减少量。如上示例中counter.status.200.hello: 11，它代表了hello请求返回200状态的次数为11

结合其它一些工具把这些信息采集到grafana里，就有得到一系列很实用的监控图表数据，比如：　　
```