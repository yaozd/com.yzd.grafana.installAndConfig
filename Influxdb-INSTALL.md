## 01��InfluxDB -CentOS 7.4.1708 (Core) ��װ
```
��װInfluxDBǰ�Ȱ�װGrafana
��ǰ��¼���룺admin/123456
==
InfluxDB�汾��influxdb-1.5.2.x86_64.rpm ���ٶ����б��ݣ�
==
��ǰ��װ�û���root�û�
1.�鿴��ǰϵͳ
cat /etc/centos-release
2.whereis influxdb (�鿴grafana����Ŀ¼��ȷ�ϱ����Ƿ��Ѱ�װgrafana)
3.mkdir /usr/grafana (Ŀǰinfluxdb��grfana����ͬһĿ¼��)
// (��wgetһ����̫��������ֱ�ӴӰٶ�������)
4.wget https://repos.influxdata.com/centos/7/x86_64/stable/influxdb-1.5.2.x86_64.rpm
5.yum localinstall influxdb-1.5.2.x86_64.rpm
6.# ����
vi /etc/influxdb/influxdb.conf
#�����޸�����begin=

reporting-disabled = true ( ���Ҫ�����棬�رն�ʱ�ϴ����ݵ�influxdata.com)
[http]
enabled = true
bind-address = ":8086"
auth-enabled = false (��������ʱ������Ϊfalse�������������Ա�û���������Ϊtrue)

#�����޸�����end=

# ���� service influxdb start
systemctl start influxdb
# ��Ϊ��������
systemctl enable influxdb
 
# ����û�
influx
CREATE USER admin WITH PASSWORD '123456' WITH ALL PRIVILEGES
exit

#�޸������ļ���
[http]
enabled = true
bind-address = ":8086"
auth-enabled = true

# ��������
systemctl restart influxdb

==
�ο���
CentOS��װInfluxDB
https://blog.csdn.net/sdulsj/article/details/80922707
centos7.2 influxdb��װ���ʹ��
https://blog.csdn.net/weixin_41004350/article/details/78492397
influxdb�û�Ȩ��ƪ
http://www.mamicode.com/info-detail-1642928.html
InfluxDB Ȩ����֤���
https://blog.csdn.net/vblegend_2013/article/details/80904845

```
## 01��InfluxDB Ȩ����֤���
```
influxdb�û�Ȩ��ƪ
http://www.mamicode.com/info-detail-1642928.html
InfluxDB Ȩ����֤���
https://blog.csdn.net/vblegend_2013/article/details/80904845

```
## 02��InfluxDB�Ƿ��շ�
```
InfluxDB��Cluster�����շѣ������������ʹ�á�
```
## 03����ο���influxdb��Ⱥ���ܲ��ٿ�Դ
```
https://zhidao.baidu.com/question/458141350483851565.html
���ۣ������������Ѿ��㹻֧�Ÿ��˺�С��˾��ҵ����
����ʵ��ʹ���У�0.10���ϵĵ��������������Ҫ�ˣ����TSM������ʵ����ǿ��
��˾һ�µ���������1400����*3000����=��ǧ�ڸ���
�洢��ѯ���ٶ�Ҳ�ܺã����һ��ǰ�һ��ʱ��7000�����ҽ��д�ȡ�ģ�����15�룬ȡ����
ѹ�����ر�����洢�ļ�С�ÿɰ�
�ҹ������£�������˾һ���ҵ��Ҳ��500GӲ��
���ϣ�Ҳ���ò����ϼ�Ⱥ��
���ԣ���Ⱥ���������Ǹ����ҵ����õ����ˣ�����շѵĻ������ִ�ҵ���Ӧ�Ĵ�˾�����׵ظ�����
���⣺ʱ���������ݿ���̳���PI����������ʯ�͵����õ÷������ܸ���ǿ����̬�������дÿ��1 ������ݴ洢һ�꣬����Ҫ4G �Ŀռ䡣һ��Ǯһ�ֻ�������ϧ��˾����
```
## 04��InfluxDB����
```
InfluxDB
һ����Դ��ʱ���������ݿ�
InfluxDB��һ����Դ��û���ⲿ������ʱ���������ݿ⡣�����ڼ�¼�������¼���ִ�з�����
����
����HTTP API�����Բ�����д����˴��������������С�
���ݿ��Ա���ǣ�����ǳ����Ĳ�ѯ��
����SQL�Ĳ�ѯ����
��װ�͹���򵥣��������������ٶȿ�
��ּ��ʵʱ��Ӧ��ѯ������ζ��point����д�뼴�������������ɹ���Ӧʱ��ӦС��100ms�Ĳ�ѯʹ��
```