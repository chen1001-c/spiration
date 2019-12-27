```
安装zabbix
    rpm -ivh http://repo.zabbix.com/zabbix/4.4/rhel/7/x86_64/zabbix-release-4.4-1.el7.noarch.rpm
    yum -y install zabbix-server-mysql zabbix-web-mysql zabbix-agent mariadb mariadb-server
```

```
启动MySQL
    systemctl start mariadb
    mysql
    create database zabbix charset utf8;
    grant all on zabbix.* to tom@'localhost' identified by '123';
    flush privileges;

```

修改zabbix的DB名字和密码

![1575620158490](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1575620158490.png)

![1575620187636](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1575620187636.png)

修改httpd的时间，改成上海时间

![1575620301079](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1575620301079.png)

```
重启httpd zabbix-server zabbix-agent
	systemctl restart httpd zabbix-server zabbix-agent
	zcat /usr/share/doc/zabbix-server-mysql-4.4.3/create.sql.gz | mysql  zabbix
```

```
拷贝文件到根目录
	cp /etc/zabbix/zabbix_agentd.conf ./
修改文件名
	mv zabbix_agentd.conf zabbix_agentd.conf.j2
配置文件
	vim zabbix_agentd.conf.j2
```

1. <img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1575620515515.png" style="zoom: 80%;" />

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1575620552855.png" alt="1575620552855" style="zoom: 67%;" />

剧本文件

![1575620913753](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1575620913753.png)

```
检查剧本
	ansible-playbook --syntax-check zabbix-agent.yml 
执行剧本
	ansible-playbook  zabbix-agent.yml
```

查看自动发现设备

![1575621153250](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1575621153250.png)