## 01��Grafana -CentOS 7.4.1708 (Core) ��װ
```
grafana�汾��grafana-5.1.4-1.x86_64.rpm ���ٶ����б��ݣ�
==
��ǰ��װ�û���root�û�
1.�鿴��ǰϵͳ
cat /etc/centos-release
2.whereis grafana (�鿴grafana����Ŀ¼��ȷ�ϱ����Ƿ��Ѱ�װgrafana)
3.mkdir /usr/grafana
4.wget https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana-5.1.4-1.x86_64.rpm
5.yum localinstall grafana-5.1.4-1.x86_64.rpm
6.systemctl start grafana-server
7.systemctl start grafana-server
8.��֤grafana�Ƿ�װ�ɹ�
ps aux|grep 'grafana'|grep -v 'grep'
netstat -nptl (�鿴�˿�-grafanaĬ�϶˿���3000)
9.�������-��grafana�ĵ�¼ҳ���Ǻܿ�ģ�
http://192.168.0.28:3000
==
�ο��ĵ���
5���Ӵ��վʵʱ������Grafana+��־����ʵս
https://yq.aliyun.com/articles/227006
grafana�ٷ��ĵ�
http://docs.grafana.org/installation/rpm/
centos7.2 grafana�İ�װ���ʹ��
https://blog.csdn.net/weixin_41004350/article/details/78492448

```
### 02��grafana����grafana����
```
ʹ��grafana cli����grafana����
https://blog.csdn.net/jailman/article/details/79096150
1.���һ�����㶪ʧadmin����
grafana-cli admin reset-admin-password ...����
2.���������û�ж�ʧadmin���룬�������grafana��UI������
2.1ͨ������ҳ�����--byArvin�Ƽ�
2.2ͨ��restfu api����--���Ƽ�
curl -X PUT -H "Content-Type: application/json" -d '{
  "oldPassword": "admin",
  "newPassword": "newpass",
  "confirmNew": "newpass"
}' http://admin:admin@<your_grafana_host>:3000/api/user/password

```