# InfluxDBʾ���ο�����
## 1.�������ռ�����Ӧ������ָ��
1.Parallel GCģʽ ��jdk1.8 Ĭ�������ռ���Parallel Scavenge����������+Parallel Old�����������

| Tables   |      name      |
|----------|:-------------:|
| ��������մ���  |gc.ps_scavenge.count|
| ���������ʱ�� | gc.ps_scavenge.time | 
| ��������մ��� | gc.ps_marksweep.count |
| ���������ʱ�� | gc.ps_marksweep.time | 
�ο���Java GC �����ּ�(https://blog.csdn.net/firecoder/article/details/7225654)

==

2.G1 GCģʽ  Ĭ�ϣ�(�����ʹ��G1)��������ʹ��G1��

| Tables   |      name      |
|----------|:-------------:|
| ��������մ���  |gc.g1_young_generation.count|
| ���������ʱ�� | gc.g1_young_generation.time | 
| ��������մ��� | gc.g1_old_generation.count |
| ���������ʱ�� | gc.g1_old_generation.time | 
�ο���[������ǳ��Java�������ջ���](http://www.importnew.com/1993.html)

==

2.CMS GCģʽ Ĭ�ϣ�(�����ʹ��CMS)��������ʹ��ParNew��

| Tables   |      name      |
|----------|:-------------:|
| ��������մ���  |gc.parnew.count|
| ���������ʱ�� | gc.parnew.time | 
| ��������մ��� | gc.concurrentmarksweep.count |
| ���������ʱ�� | gc.concurrentmarksweep.time | 

���г�ʼ��ǡ����±��������������Ȼ��Ҫ��Stop The World��

�ο���[������ǳ��Java�������ջ���](http://www.importnew.com/1993.html)


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
4.[ʹ��JConsole��ؽ��̡��̡߳��ڴ桢cpu�������](http://www.51testing.com/html/95/115295-804841.html)
```
ʹ��JConsole��ؽ��̡��̡߳��ڴ桢cpu�������
http://www.51testing.com/html/95/115295-804841.html
===
Heap and Non-heap�ڴ�

JVM���������ڴ棺heap��non-heap�ڴ棬�����ڴ涼����JVM����ʱ������

Heap memory������ʱ������������JVMΪ���ж���ʵ���Ͷ��з�����ڴ档Heap����Ϊ�̶�ֲ���߿ɱ�ֵ�������ռ�����һ�����ڻ��ն���ռ�õ�heap�ڴ���Զ����ڴ����ϵͳ��

Non-heap memory ����һ���������̹߳���ķ�������method area�����ڲ����̻�JVM�Ż�������ڴ档���洢��ÿһ����Ľṹ���������г����أ��ֶκͷ������ݣ����캯���ͷ����Ĵ��롣���������߼����� heap��һ���֣�����������ʵ�֣�JVM���ܲ����������ռ���ѹ������heapһ���������������Ϊ�̶���ɱ��С��������������Ҫ���ڴ�û�б�Ҫ���� ���ġ�

���˷�������֮�⣬һ��JVMʵ�ֵ��ڲ����̻��Ż�������ڴ�Ҳ����non-heap�ڴ档����JIT������Ϊ��������ܶ����ڴ洢���ػ�����������ڴ档
===
lUsed����ǰʹ�õ��ڴ�������ʹ�õ��ڴ�������ָ���еĶ���ռ�õ��ڴ棬�����ɴ�Ͳ��ɴ�Ķ���

lCommitted��JVM��ʹ�õ��ڴ�����Committed�ڴ�����������ʱ��仯���仯��JAVA��������ܽ�ĳЩ�ڴ��ͷţ���������ϵͳ��committed�ڴ���ܱ�����ʱ��ʼ������ڴ���Ҫ�١�Committed�ڴ����Ǵ��ڵ���used�ڴ档
===
Summary

Uptime��JVM������ʱ����

Total compile time�������ڼ�ʱ���루JIT compilation���е�ʱ�䡣

Process CPU time��JVM���ѵ���CPUʱ�䡣

Threads

Live threads����ǰ���daemon�̼߳�non-daemon�߳�������

Peak����JVM�����󣬻�̷߳�ֵ��

Daemon threads����ǰ���Daemon�߳�������

Total started����JVM�������������߳�����������daemon,non-daemon����ֹ�˵ģ�

Memory

Current heap size���ѣ�heap��ռ�õ��ڴ�������KΪ��λ��

Committed memory��Ϊ�ѷ�����ڴ�����

Maximum heap size����ռ�õ�����ڴ�����

Objects pending for finalization���ȴ�������finalization���Ķ���������

Garbage collector information��GC��Ϣ�������������������ƣ���ִ�е��������մ�����ִ�����������ܺ�ʱ��

Classes

Current classes loaded����ǰ�����ص��ڴ��classes����

Total classes loaded����JVM�����󱻼��ص��ڴ��classes��������������ж�صġ�

Total classes unloaded����JVM�����󣬴��ڴ�ж�ص�classes������

Operating System��

Total physical memory�������ڴ�����

Free physical memory�������ڴ������

Committed virtual memory��Ϊ�����еĽ��̷���������ڴ�����

�����ڴ����ģ�
Memoryѡ��ṩ���ڴ����ĺ��ڴ����Ϣ��
```
