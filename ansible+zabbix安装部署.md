### 安装zabbix

```
1.安装zabbix官方yum源
rpm -ivh http://repo.zabbix.com/zabbix/4.4/rhel/7/x86_64/zabbix-release-4.4-1.el7.noarch.rpm
```

```
2.安装zabbix相关组件和数据库MySQL
yum -y install zabbix-server-mysql zabbix-web-mysql zabbix-agent mariadb mariadb-server
```

```
3.给zabbix创建数据库并授权账号
systemctl start mariadb
mysql
create database zabbix charset utf8;
grant all on zabbix.* to tom@'localhost' identified by '123';
flush privileges;
exit
```

```
4.导入初始的数据
zcat /usr/share/doc/zabbix-server-mysql-4.4.3/create.sql.gz | mysql  zabbix
```

```
5.修改zabbix-server配置文件，（连接数据库：数据库主机、数据库名字、账号、密码、端口）
vim /etc/zabbix/zabbix_server.conf
DBUser=tom
DBPassword=123
```

```
6.修改时区
vim /etc/httpd/conf.d/zabbix.conf
修改：php_value date.timezone Asia/Shanghai
<IfModule mod php5.c>
​          php_value max_ execution_ time 300 
​          php_value memory_ limit 128M
​          php_value post_ max_ size 16M
​          php_value upload max_ filesize 2M
​          php_value max input time 300
​          php_value max input vars 10000
​          php_value a Lways populate raw post data - 1
​          php_value date. timezone Asia/ Shanghai
</IfModuLe>
```

```
7.关闭防火墙
systemctl stop firewalld
setenforce 0
```

```
8.启动所有服务（httpd、zabbix-server、zabbix-agent）
systemctl restart httpd zabbix-server zabbix-agent
```

```
9.访问zabbix完成zabbix-web的安装
http://192.168.189.171/zabbix
```

