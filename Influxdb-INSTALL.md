## 01：InfluxDB -CentOS 7.4.1708 (Core) 安装
```
安装InfluxDB前先安装Grafana
当前登录密码：admin/123456
==
InfluxDB版本：influxdb-1.5.2.x86_64.rpm （百度云有备份）
==
当前安装用户是root用户
1.查看当前系统
cat /etc/centos-release
2.whereis influxdb (查看grafana命令目录，确认本地是否已安装grafana)
3.mkdir /usr/grafana (目前influxdb与grfana放在同一目录下)
// (但wget一般下太慢，可以直接从百度云下载)
4.wget https://repos.influxdata.com/centos/7/x86_64/stable/influxdb-1.5.2.x86_64.rpm
5.yum localinstall influxdb-1.5.2.x86_64.rpm
6.# 配置
vi /etc/influxdb/influxdb.conf
#配置修改内容begin=

reporting-disabled = true ( 这个要设置真，关闭定时上传数据到influxdata.com)
[http]
enabled = true
bind-address = ":8086"
auth-enabled = false (初次启动时先设置为false，等设置完管理员用户后再设置为true)

#配置修改内容end=

# 启动 service influxdb start
systemctl start influxdb
# 设为开机启动
systemctl enable influxdb
 
# 添加用户
influx
CREATE USER admin WITH PASSWORD '123456' WITH ALL PRIVILEGES
exit

#修改配置文件：
[http]
enabled = true
bind-address = ":8086"
auth-enabled = true

# 重新启动
systemctl restart influxdb

==
参考：
CentOS安装InfluxDB
https://blog.csdn.net/sdulsj/article/details/80922707
centos7.2 influxdb安装与简单使用
https://blog.csdn.net/weixin_41004350/article/details/78492397
influxdb用户权限篇
http://www.mamicode.com/info-detail-1642928.html
InfluxDB 权限验证相关
https://blog.csdn.net/vblegend_2013/article/details/80904845

```
## 01：InfluxDB 权限验证相关
```
influxdb用户权限篇
http://www.mamicode.com/info-detail-1642928.html
InfluxDB 权限验证相关
https://blog.csdn.net/vblegend_2013/article/details/80904845

```
## 02：InfluxDB是否收费
```
InfluxDB的Cluster功能收费，单机功能免费使用。
```
## 03：如何看待influxdb集群功能不再开源
```
https://zhidao.baidu.com/question/458141350483851565.html
结论：单机版性能已经足够支撑个人和小公司的业务了
我在实际使用中，0.10以上的单机版可以满足需要了，这个TSM的引擎实力很强了
我司一月的数据量是1400个点*3000万秒=四千亿个点
存储查询的速度也很好，而且还是按一段时间7000秒左右进行存取的，存大概15秒，取几秒
压缩性特别棒，存储文件小得可爱
我估计了下，存下我司一年的业务也才500G硬盘
综上，也就用不着上集群了
所以，集群功能真心是更大的业务才用得着了，这个收费的话，这种大业务对应的大公司，妥妥地付得起。
另外：时间序列数据库的翘楚，PI，按百万起，石油电力用得飞起，性能更是强到变态。广告中写每秒1 万点数据存储一年，仅需要4G 的空间。一分钱一分货啊。可惜我司买不起。
```
## 04：InfluxDB介绍
```
InfluxDB
一个开源的时间序列数据库
InfluxDB是一个开源的没有外部依赖的时间序列数据库。适用于记录度量，事件及执行分析。
特性
内置HTTP API，所以不用再写服务端代码来启动和运行。
数据可以被标记，允许非常灵活的查询。
类似SQL的查询语言
安装和管理简单，数据输入和输出速度快
它旨在实时响应查询。这意味着point数据写入即被索引并立即可供响应时间应小于100ms的查询使用
```