# InfluxDB示例参考代码
## 1.各垃圾收集器对应的性能指标
1.Parallel GC模式 （jdk1.8 默认垃圾收集器Parallel Scavenge（新生代）+Parallel Old（老年代））

| Tables   |      name      |
|----------|:-------------:|
| 青年代回收次数  |gc.ps_scavenge.count|
| 青年代回收时间 | gc.ps_scavenge.time | 
| 老年代回收次数 | gc.ps_marksweep.count |
| 老年代回收时间 | gc.ps_marksweep.time | 
参考：Java GC 调试手记(https://blog.csdn.net/firecoder/article/details/7225654)

==

2.G1 GC模式  默认：(老年代使用G1)（新生代使用G1）

| Tables   |      name      |
|----------|:-------------:|
| 青年代回收次数  |gc.g1_young_generation.count|
| 青年代回收时间 | gc.g1_young_generation.time | 
| 老年代回收次数 | gc.g1_old_generation.count |
| 老年代回收时间 | gc.g1_old_generation.time | 
参考：[—深入浅出Java垃圾回收机制](http://www.importnew.com/1993.html)

==

2.CMS GC模式 默认：(老年代使用CMS)（新生代使用ParNew）

| Tables   |      name      |
|----------|:-------------:|
| 青年代回收次数  |gc.parnew.count|
| 青年代回收时间 | gc.parnew.time | 
| 老年代回收次数 | gc.concurrentmarksweep.count |
| 老年代回收时间 | gc.concurrentmarksweep.time | 

其中初始标记、重新标记这两个步骤仍然需要“Stop The World”

参考：[—深入浅出Java垃圾回收机制](http://www.importnew.com/1993.html)


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
4.[使用JConsole监控进程、线程、内存、cpu、类情况](http://www.51testing.com/html/95/115295-804841.html)
```
使用JConsole监控进程、线程、内存、cpu、类情况
http://www.51testing.com/html/95/115295-804841.html
===
Heap and Non-heap内存

JVM管理两种内存：heap和non-heap内存，两种内存都是在JVM启动时建立。

Heap memory是运行时数据区域，用于JVM为所有对象实例和队列分配的内存。Heap可能为固定植或者可变值。垃圾收集器是一个用于回收对象占用的heap内存的自动化内存管理系统。

Non-heap memory 包含一个在所有线程共享的方法区域（method area）和内部进程或JVM优化所需的内存。它存储了每一个类的结构，比如运行常量池，字段和方法数据，构造函数和方法的代码。方法区域逻辑上是 heap的一部分，但是依赖于实现，JVM可能不进行垃圾收集或压缩。像heap一样，方法区域可能为固定或可变大小。方法区域所需要的内存没有必要是连 续的。

除了方法区域之外，一个JVM实现的内部进程或优化所需的内存也属于non-heap内存。比如JIT编译器为了提高性能而用于存储本地机器码所需的内存。
===
lUsed：当前使用的内存总量。使用的内存总量是指所有的对象占用的内存，包括可达和不可达的对象。

lCommitted：JVM可使用的内存量。Committed内存数量可能随时间变化而变化。JAVA虚拟机可能将某些内存释放，还给操作系统，committed内存可能比启动时初始分配的内存量要少。Committed内存总是大于等于used内存。
===
Summary

Uptime：JVM已运行时长。

Total compile time：花费在即时编译（JIT compilation）中的时间。

Process CPU time：JVM花费的总CPU时间。

Threads

Live threads：当前活动的daemon线程加non-daemon线程数量。

Peak：自JVM启动后，活动线程峰值。

Daemon threads：当前活动的Daemon线程数量。

Total started：自JVM启动后，启动的线程总量（包括daemon,non-daemon和终止了的）

Memory

Current heap size：堆（heap）占用的内存量，以K为单位。

Committed memory：为堆分配的内存总量

Maximum heap size：堆占用的最大内存量。

Objects pending for finalization：等待析构（finalization）的对象数量。

Garbage collector information：GC信息，摆阔垃圾回收器名称，已执行的垃圾回收次数和执行垃圾回收总耗时。

Classes

Current classes loaded：当前被加载到内存的classes数量

Total classes loaded：自JVM启动后被加载到内存的classes总量，包括后来卸载的。

Total classes unloaded：自JVM启动后，从内存卸载的classes总量。

Operating System：

Total physical memory：物理内存总量

Free physical memory：物理内存空闲量

Committed virtual memory：为运行中的进程分配的虚拟内存总量

监视内存消耗：
Memory选项卡提供了内存消耗和内存池信息。
```
