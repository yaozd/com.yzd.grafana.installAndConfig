https://grafana.com/dashboards/4701
A dashboard for Micrometer instrumented applications (Java, Spring Boot).

Features
JVM memory
Process memory (provided by micrometer-jvm-extras)
CPU-Usage, Load, Threads, File Descriptors, Log Events
JVM Memory Pools (Heap, Non-Heap)
Garbage Collection
Classloading
Direct-/Mapped-Buffer
minimalist I/O Overview
HTTP - Rate, Errors, Duration
TOMCAT/JETTY - Saturation
Note
Instead of using the job tag to distinct different applications, this dashboard makes use of a common tag called application applied to every metric. In case this is an unfortunate decision please let me know.

Compatibility
micrometer:1.0.0+
micrometer-jvm-extras:0.1.2
Contact
For suggestions or bug reports, please contact me on Twitter or contact/DM mweirauch in the Micrometer Slack.
===
https://micrometer.io/

