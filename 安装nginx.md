## 编译安装nginx

### 1、Nginx介绍

Nginx (engine x) 是一个轻量的，高性能的HTTP和反向代理服务器，也是一个IMAP/POP3/SMTP服务器。Nginx是由伊戈尔·赛索耶夫所研发，因它的稳定性、丰富的功能集、示例配置文件和低系统资源的消耗而闻名。

其特点是占有内存少，并发能力强， nginx的并发能力在同类型的网页服务器中表现较好，中国大陆使用nginx网站用户有：百度、京东、新浪、网易、腾讯、淘宝等。

在高连接并发的情况下，Nginx是Apache服务器不错的替代品。

### 2、安装依赖

```shell
[root@ c6m01 ~]# yum -y install gcc gcc-c++ pcre-devel openssl-devel wget
```

### 3、下载nginx包

```shell
[root@ c6m01 ~]# wget http://nginx.org/download/nginx-1.12.2.tar.gz
```

### 4、解压nginx包

```shell
[root@ c6m01 ~]# tar -zxvf nginx-1.12.2.tar.gz
```

### 5、切换目录

```shell
[root@ c6m01 ~]# cd nginx-1.12.2
```

### 6、配置和检测环境

```shell
[root@ c6m01 nginx-1.12.2]# ./configure --prefix=/usr/local/nginx
```

### 7、编译

```shell
[root@ c6m01 nginx-1.12.2]# make
```

### 8、编译安装

```shell
[root@ c6m01 nginx-1.12.2]# make install
```

### 9、启停及检查语法

```shell
[root@ c6m01 nginx-1.12.2]# /usr/local/nginx/sbin/nginx		#启动nginx

[root@ c6m01 nginx-1.12.2]# nginx -t		#检查语法
nginx: the configuration file /usr/local/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /usr/local/nginx/conf/nginx.conf test is successful

[root@ c6m01 nginx-1.12.2]# ps -ef|grep nginx		#查看进程
root       4245      1  0 11:26 ?        00:00:00 nginx: master process nginx
nobody     4246   4245  0 11:26 ?        00:00:00 nginx: worker process
root       4250   1763  0 11:26 pts/3    00:00:00 grep --color=auto nginx

[root@ c6m01 nginx-1.12.2]# /usr/local/nginx/sbin/nginx -s stop		#停止nginx
[root@ c6m01 nginx-1.12.2]# ps -ef|grep nginx
root       4254   1763  0 11:27 pts/3    00:00:00 grep --color=auto nginx

[root@ c6m01 ~]# /usr/local/nginx/sbin/nginx -s reload		#当子配置文件发生变化，重新载入配置文件
```

