## harbor安装

```
上传harbor包
harbor-offline- installer-v1.8.1. tgz 
```

```
解压harbor
	tar -zxf harbor-offline-installer-v1.8.1.tgz
```

```
移动目录
	mv harbor /usr/local/
切换目录
	cd /usr/local/harbor
```

```
修改hostname
vim harbor.yml
hostname: 10.0.0.71   ---> 本机ip
```

```
修改harbor密码
harbor_ admin_ password: admin
```

```
环境监测
	./install.sh
```

![1576292229789](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1576292229789.png)

