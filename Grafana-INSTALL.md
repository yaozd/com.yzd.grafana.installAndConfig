## 01：Grafana -CentOS 7.4.1708 (Core) 安装
```
grafana版本：grafana-5.1.4-1.x86_64.rpm （百度云有备份）
==
当前安装用户是root用户
1.查看当前系统
cat /etc/centos-release
2.whereis grafana (查看grafana命令目录，确认本地是否已安装grafana)
3.mkdir /usr/grafana
4.wget https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana-5.1.4-1.x86_64.rpm
5.yum localinstall grafana-5.1.4-1.x86_64.rpm
6.systemctl start grafana-server
7.systemctl start grafana-server
8.验证grafana是否安装成功
ps aux|grep 'grafana'|grep -v 'grep'
netstat -nptl (查看端口-grafana默认端口是3000)
9.浏览器打开-（grafana的登录页还是很酷的）
http://192.168.0.28:3000
==
参考文档：
5分钟搭建网站实时分析：Grafana+日志服务实战
https://yq.aliyun.com/articles/227006
grafana官方文档
http://docs.grafana.org/installation/rpm/
centos7.2 grafana的安装与简单使用
https://blog.csdn.net/weixin_41004350/article/details/78492448

```
### 02：grafana重置grafana密码
```
使用grafana cli重置grafana密码
https://blog.csdn.net/jailman/article/details/79096150
1.情况一：在你丢失admin密码
grafana-cli admin reset-admin-password ...（）
2.情况二：你没有丢失admin密码，最好是在grafana的UI中设置
2.1通过管理页面更改--byArvin推荐
2.2通过restfu api更改--不推荐
curl -X PUT -H "Content-Type: application/json" -d '{
  "oldPassword": "admin",
  "newPassword": "newpass",
  "confirmNew": "newpass"
}' http://admin:admin@<your_grafana_host>:3000/api/user/password

```