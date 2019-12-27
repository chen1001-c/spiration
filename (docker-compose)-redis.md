Redis

```
创建目录
	mkdir redis
切换目录
	cd redis
```

vim docker-compose.yml

![1576290244891](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1576290244891.png)

```
创建集群
	docker run --rm -it 10.30.5.120/docker/redis-trib create --replicas 1 10.0.0.71:7001 10.0.0.71:7002 10.0.0.71:7003 10.0.0.71:7004 10.0.0.71:7005 10.0.0.71:7006
```

![1576290500811](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1576290500811.png)

```
测试任意一个节点
	docker-compose exec redis1 redis-cli -c -h 10.0.0.71 -p 7001
	-c是使用集群的方式连接redis
	-h 是redis主机ip地址
	-p 是redis主机的端口
```

查看集群信息

![1576291040714](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1576291040714.png)

查看集群各个节点信息

![1576291100944](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1576291100944.png)

测试高可用

目前我们的name键值对的数据存在redis2上，我们停掉redis2，查看数据是否收影响

![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1576291228689.png) 

然后我们在登录到集群中查看各个节点的状态，

![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1576291317740.png) 

我们可以看到7002端口对应的redis2已经断开连接，处于fail状态，但是7005对应的redis5已经成为了新的master（可以根据覆盖的槽来辨别）

我们再来获取数据测试，数据是否正常读取和写入

![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1576291356251.png) 

我们发现数据依然可以正常从redis5上获取

至此redis-cluster集群搭建并测试完毕