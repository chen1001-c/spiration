Redis

```
创建目录
	mkdir redis
切换目录
	cd redis
```

```
vim docker-compose.yml
[root@ LocaLhost redis]# vim docker-compose. yml
version: "3 I
services :
  redis 1 :
    image: 10.30.5. 120/docker/ redis-c luster
    environment
      REDIS PORT: 7001
    ports :
      - "7001: 7001
      - "17001 : 17001"
   redis2 :
     image: 10.30.5.120/docker/ redis-cluster
     environment
      REDIS_PORT: 7002
    ports :
      - "7002: 7002"
      - "17002: 17002”
   redis3:
     image: 10.30.5.120/docker/ redis-cluster
     environment
       REDIS_ PORT: 7003
     ports :
       - "7003: 7003
       - "17003: 17003 " 
   redis4:
     image: 10.30.5.120/docker/ redis-c luster
     environment
       REDIS_ PORT: 7004
     ports :
       - "7004: 7004"
       - "17004: 17004"
   redis5:
   image: 10 .30.5.120/ docker/ redis -cluster
   environment
     REDIS_ PORT: 7005
   ports :
     - "7005 : 7005" I
     - "17005: 17005"
   redis6:
   image: 10 .30.5.120/ docker/ redis -cluster
   environment
     REDIS_ PORT: 7006
   ports :
     - "7006: 7006"
     - "17006: 17006"
```



```
创建集群
	docker run --rm -it 10.30.5.120/docker/redis-trib create --replicas 1 10.0.0.71:7001 10.0.0.71:7002 10.0.0.71:7003 10.0.0.71:7004 10.0.0.71:7005 10.0.0.71:7006
```

```
测试任意一个节点
	docker-compose exec redis1 redis-cli -c -h 10.0.0.71 -p 7001
	-c是使用集群的方式连接redis
	-h 是redis主机ip地址
	-p 是redis主机的端口
```

```
查看集群信息
[ root@ LocaLhost redis]# doc ke r-compose exec redis1 redis-cli -C -h 10.0.0.71 -p 7005 
10.0.0.71: 7005> CL USTER INFO
```



```
查看集群各个节点信息
10.0.0.71: 7005> CL USTER NODES
```

```
测试高可用
目前我们的name键值对的数据存在redis2上，我们停掉redis2，查看数据是否收影响
[roote LocaLhost redis ]# doc ker-compose stop redis2
[ roote LocaLhost redis ]# docker-compose ps 
```

```
然后我们在登录到集群中查看各个节点的状态
[ root@ LocaLhost redis ]# doc ke r compose exec redis1 redis-cli C -h 10.0.0.71 p 7005
10.0.0.71: 7005> CLUSTER NODES 
```

```
我们可以看到7002端口对应的redis2已经断开连接，处于fail状态，但是7005对应的redis5已经成为了新的master（可以根据覆盖的槽来辨别）
我们再来获取数据测试，数据是否正常读取和写入
[root@ LocaLhost redis ]# docker-compose exec redis1 redis-cli -C h 10.0.0.71 -p 7006
10.0.0.71: 7006> get name
-> Redirected to slot [5798] Located at 172.22.0.1: 7005
”tom”
172.22.0.1:7005> 

```

