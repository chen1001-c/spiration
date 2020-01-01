## 安装Apache

### httpd简介

当今主流的开源Web服务器软件有`httpd(Apache),lighttpd,nginx,thttpd`等，而httpd是迄今为止使用量多的web服务器，据统计目前httpd的全球占有量是47%左右，虽然有所下降但是使用两仍然是最多的，统计web服务器使用率的网站是：`http://news.netcraft.com/httpd`。

```shell
#安装Apache
[root@ localhost ~]# yum -y install httpd

#启动Apache
[root@ localhost ~]# service httpd restart

#设置开机自启
[root@ localhost ~]# chkconfig httpd on		

#查看httpd进程
[root@ localhost ~]# ps -ef|grep httpd		

#查看httpd端口号
[root@ localhost ~]# ss -lntp|grep 80			
LISTEN     0      128                      :::80                      :::*      users:
```



```shell
#常见配置及参数详解
vim /etc/httpd/conf/httpd.conf

ServerRoot "/etc/httpd"			#用于指定Apache运行的根目录
Listen 80						#监听80端口
MaxClients  256					#指定同时能访问服务器的客户机数量为256
DocumentRoot "/var/www/html"	#网页文件存放的目录
DirectoryIndex index.html index.html.var	#默认网站主页
Include conf.d/*.conf			#读取/etc/httpd/conf/conf.d/目录中所有以.conf结尾的文件
ServerName www.wg.com			#域名
ServerAdmin						#设置管理员的邮箱
Include conf.d/*.conf			#包含的子配置文件
User apache						#用户是apache
Group apache					#用户组是apache
Directory 						#认证授权和访问控制

##################################
<IfModule prefork.c>     #当httpd服务使用的profork模型的时候：
 StartServers      10    #默认启动10个作业进程
 MinSpareServers    10    #空闲进程数不低于10个
 MaxSpareServers    20    #空闲进程数最大20个
 ServerLimit      256    #最多可以启动256个进程
 MaxClients       256    #最大并发客户端数为256个
 MaxRequestsPerChild 4000 #每个进程可以处理4000个请求，超过此数目进程被杀死并重新创建
</IfModule>


需要注意的是：ServerLimit最大值为20000个，并且：由于profork是单一线程的进程，所以每个进程在同一时间里仅能处理一个请求(也就是一个请求一个进程)，所以MaxClients的值要和ServerLimit一致。而且，profork的开销比较大，不过稳定性比较强。
```

```shell
#安装PHP
[root@ localhost ~]# yum -y install php php-gd

#修改配置文件
[root@ localhost ~]# vim /etc/httpd/conf/httpd.conf

#添加一行PHP
AddType application/x-httpd-php .php

#添加一个PHP页面
DirectoryIndex index.php index.html index.html.var

#编写PHP页面
[root@ localhost ~]# vim /var/www/html/index.php
<?php
phpinfo();
?>

#重启Apache
[root@ localhost ~]# service httpd restart
Stopping httpd:                                            [  OK  ]
Starting httpd: httpd: Could not reliably determine the server's fully qualified domain name, using localhost.localdomain for ServerName
                                                           [  OK  ]
#测试页面
测试本机IP
```

