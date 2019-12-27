Docker

什么是 **Docker** 

Docker 最初是 dotCloud 公司创始人 Solomon Hykes 在法国期间发起的一个公司内部项目， 它是基于 dotCloud 公司多年云服务技术的一次革新，并于 2013 年 3 月以 Apache 2.0 授权 协议开源，主要项目代码在 GitHub 上进行维护。Docker 项目后来还加入了 Linux 基金会， 并成立推动 开放容器联盟（OCI）。 

Docker 自开源后受到广泛的关注和讨论，至今其 GitHub 项目已经超过 4 万 6 千个星标和一 万多个 fork。甚至由于 Docker 项目的火爆，在 2013 年底，dotCloud 公司决定改名为 Docker。Docker 最初是在 Ubuntu 12.04 上开发实现的；Red Hat 则从 RHEL 6.5 开始对 Docker 进行支持；Google 也在其 PaaS 产品中广泛应用 Docker。 

Docker 使用 Google 公司推出的 Go 语言 进行开发实现，基于 Linux 内核的 cgroup，namespace，以及 AUFS 类的 Union FS 等技术，对进程进行封装隔离，属于 操作 系统层面的虚拟化技术。由于隔离的进程独立于宿主和其它的隔离的进程，因此也称其为容 器。最初实现是基于 LXC，从 0.7 版本以后开始去除 LXC，转而使用自行开发的 libcontainer，从 1.11 开始，则进一步演进为使用 runC 和 containerd。 

 ![Docker 架构](https://docs.microsoft.com/en-us/virtualization/windowscontainers/deploy-containers/media/docker-on-linux.png) 

Docker 在容器的基础上，进行了进一步的封装，从文件系统、网络互联到进程隔离等等，极 大的简化了容器的创建和维护。使得 Docker 技术比虚拟机技术更为轻便、快捷。

下面的图片比较了 Docker 和传统虚拟化方式的不同之处。传统虚拟机技术是虚拟出一套硬件 后，在其上运行一个完整操作系统，在该系统上再运行所需应用进程；而容器内的应用进程 直接运行于宿主的内核，容器内没有自己的内核，而且也没有进行硬件虚拟。因此容器要比 传统虚拟机更为轻便。 

 ![传统虚拟化](https://yeasy.gitbooks.io/docker_practice/content/introduction/_images/virtualization.png) 

 ![传统虚拟化](https://yeasy.gitbooks.io/docker_practice/content/introduction/_images/virtualization.png) 



# 1.2、为什么要使用 Docker？

作为一种新兴的虚拟化方式，`Docker` 跟传统的虚拟化方式相比具有众多的优势。

## 更高效的利用系统资源

　　由于容器不需要进行硬件虚拟以及运行完整操作系统等额外开销，`Docker` 对系统资源的利用率更高。无论是应用执行速度、内存损耗或者文件存储速度，都要比传统虚拟机技术更高效。因此，相比虚拟机技术，一个相同配置的主机，往往可以运行更多数量的应用。

## 更快速的启动时间

　　传统的虚拟机技术启动应用服务往往需要数分钟，而 `Docker` 容器应用，由于直接运行于宿主内核，无需启动完整的操作系统，因此可以做到秒级、甚至毫秒级的启动时间。大大的节约了开发、测试、部署的时间。

## 一致的运行环境

　　开发过程中一个常见的问题是环境一致性问题。由于开发环境、测试环境、生产环境不一致，导致有些 bug 并未在开发过程中被发现。而 `Docker` 的镜像提供了除内核外完整的运行时环境，确保了应用运行环境一致性，从而不会再出现 *「这段代码在我机器上没问题啊」* 这类问题。

## 持续交付和部署

　对开发和运维（[DevOps](https://zh.wikipedia.org/wiki/DevOps)）人员来说，最希望的就是一次创建或配置，可以在任意地方正常运行。

使用 `Docker` 可以通过定制应用镜像来实现持续集成、持续交付、部署。开发人员可以通过 [Dockerfile](https://yeasy.gitbooks.io/docker_practice/content/image/dockerfile) 来进行镜像构建，并结合 [持续集成(Continuous Integration)](https://en.wikipedia.org/wiki/Continuous_integration) 系统进行集成测试，而运维人员则可以直接在生产环境中快速部署该镜像，甚至结合 [持续部署(Continuous Delivery/Deployment)](https://en.wikipedia.org/wiki/Continuous_delivery) 系统进行自动部署。

而且使用 [`Dockerfile`](https://yeasy.gitbooks.io/docker_practice/content/image/build.html) 使镜像构建透明化，不仅仅开发团队可以理解应用运行环境，也方便运维团队理解应用运行所需条件，帮助更好的生产环境中部署该镜像。

## 更轻松的迁移

　　由于 `Docker` 确保了执行环境的一致性，使得应用的迁移更加容易。`Docker` 可以在很多平台上运行，无论是物理机、虚拟机、公有云、私有云，甚至是笔记本，其运行结果是一致的。因此用户可以很轻易的将在一个平台上运行的应用，迁移到另一个平台上，而不用担心运行环境的变化导致应用无法正常运行的情况。

## 更轻松的维护和扩展

`　　Docker` 使用的分层存储以及镜像的技术，使得应用重复部分的复用更为容易，也使得应用的维护更新更加简单，基于基础镜像进一步扩展镜像也变得非常简单。此外，`Docker` 团队同各个开源项目团队一起维护了一大批高质量的 [官方镜像](https://hub.docker.com/search/?type=image&image_filter=official)，既可以直接在生产环境使用，又可以作为基础进一步定制，大大的降低了应用服务的镜像制作成本。

## 对比传统虚拟机总结

| 特性       | 容器               | 虚拟机      |
| ---------- | ------------------ | ----------- |
| 启动       | 秒级               | 分钟级      |
| 硬盘使用   | 一般为 `MB`        | 一般为 `GB` |
| 性能       | 接近原生           | 弱于        |
| 系统支持量 | 单机支持上千个容器 | 一般几十个  |

**CentOS 7（使用 yum 进行安装）**

```
#1: 安装必要的一些系统工具
	yum install -y yum-utils device-mapper-persistent-data lvm2
#2: 添加软件源信息
	yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
#3: 更新并安装Docker-CE
	yum makecache fast
	yum -y install docker-ce
#4: 开启Docker服务
	service docker start
```

—镜像常用命令

```
docker images        　											//查看镜像
docker search　文件名　 　 										//搜索镜像
docker pull    文件名　　　										//下载镜像
docker push　　文件名　　 											//上传镜像
docker load < 文件名.tar  						//导入镜像文件（格式为.tar)　例：docker load <nginx.tar
docker save image_name > xx.tar  		 //导出镜像包，镜像名可以docker images查看，REPOSITORY下面名字
docker run -it 镜像名称：镜像标签　启动命令　　		//启动运行镜像　例：docker run -it night:night01 bash
//-i 表示交互　-t表示终端
例：docker run -it centos /usr/bin/python 						//只要可以执行的命令都可以
[root@docker_1 ~]# docker run -it centos /bin/ls
anaconda-post.log  dev home  lib64  mnt  proc run   srv  tmp var
bin   etc lib   media  opt  root sbin  sys  usr
docker tag 														//修改镜像名称和标签
```

docker inspect  镜像名称：镜像标签　// 获取容器/镜像的元数据。主要查看CMD后面的命令

            "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "CMD [\"nginx\" \"-g\" \"daemon off;\"]"

```
docker ps　									       	//  查看已开启的容器加　-a 查看所有容器
docker history 镜像名　							    	//查看镜像制作历叱
docker rmi 镜像名　								     	//删除本地镜像
docker save　镜像名 > 文件名.tar　　 					 //镜像另存为tar包
```

—容器常用命令

-－后面加容器ＩＤ

docker run //运行容器

//-i交互式　-t终端　-d后台进程

//注意：启用一个有交互式的进程又要放后台进程用-itd , 单纯无交互放后台直接-d即可

```
docker ps 					//查看容器列表　没加-a表示正在运行的容器　加-a查看所有容器　-q查看ＩＤ号
docker stop 				//关闭容器
[root@docker_1 docker]# docker stop $(docker ps -q) //停用全部运行中的容器
docker start 				//启动容器
docker restart 				//重启容器
docker attach|exec 			//进入容器　退出挂后台要用ＣＴＲＬ＋Ｐ+Ｑ
docker inspect 				//查看容器底层信息 常用于查看服务ＩＰ和端口
docker top 					//查看容器进程列表　相当于在容器里执行ps查看这个容器的进程
//容器的进程在运行它的物理机上可以查看到，隔离性没有ＫＶＭ那么好
docker rm 					//删除容器
[root@docker_1 docker]# docker rm $(docker ps -qa)  			//删除所有容器
[root@docker_1 docker]# docker stop $(docker ps -q) & docker rm $(docker ps -aq)
docker exec -it 　容器ＩＤ　 								//进入容器　建议用这个连接容器，exit退出后
[root@docker_1 docker]# docker exec -it 19c535ae17b3 bash　		//要加命令
[root@docker_1 ~]# docker run -d -p 80:80 nginx 
```



虚拟机：
   通过虚拟化技术我们可以在服务上运行多个不同环境的虚拟机，大大提高我们对服务器的利用率！
   虚拟机的硬件的弹性扩展也方便了我们后期虚拟机配置的提升
   统一的管理平台也会大大降低我们的维护成本

容器：
    容器本身的意思是指可以存放东西的器皿，我们这里可以把容器想想成是一个盒子、箱子！里面存放的就是我们要运行的应用：如一个nginx、tomcat
    容器技术相对于虚拟机具有哪些特点？
       1.体积小
       2.启动速度快
       3.性能接近原生
       4.单节点支持的容器的数量多
       6.环境一致性
 docker的安装

```
Centos7.6
  1.配置docker的yum源，可以使用阿里云的
  2.安装docker-ce
  yum -y install docker-ce
  3.关闭防火墙
  systemctl stop firewalld
  setenforce
  4.启动Docker
  systemctl start docker
  systemctl enable docker
```

```
  Docker三个基本概念
  	1.镜像仓库(hub.docker.com 镜像仓库)
  	2.镜像
  	3.容器
  Docker常用命令:
    对镜像的操作：
    1.获取镜像
      增：
       docker pull  镜像名:TAG
      删：
       删除镜像，我们不能直接删除有容器依赖的镜像
        docker rmi     镜像名/ID
        docker rmi -f  镜像名/ID
      改：
        docker tag
      查：
        查看本地镜像
        docker images

对容器的操作:
   增：
     1.创建并运行容器
        docker run  --name 容器名字  -d  -p  宿主机端口:容器端口   基础镜像

   			例子: docker run --name web1 -d -p 80:80 nginx:latest
            docker  run --name learn1  -it busybox /bin/sh  以可交互的方式运行一个容器
       删：
         删除容器，我们不能直接删除一个正在运行的容器，需要先停止再删除，或者-f,强制删除
         docker rm web1
         docker rm -f web1
       改：
          容器重命名
          docker rename       修改容器名字
          容器启动和停止
          docker  start/stop/restart  容器名
          docker  pause      容器名     \\暂停容器
          docker  unpause    容器名      \\取消暂停容器
          docker  update                \\更新容器的配置
          docker  cp                    \\容器和宿主机之间复制文件，默认覆盖已有的文件
          docker  exec                  \\在运行的容器中执行一条命令
          docker  exec -it  web1 /bin/bash  \\以交互的方式进入web1容器操作


       查：
          查看正在运行的容器
          docker ps
          查看所有的容器
          docker ps -a
          docker stats 容器名  \\查看容器运行状态（CPU\内存\网络IO\磁盘IO使用情况）
          docker top  容器名   \\查看容器正在运行的进程
          docker inspect 容器/镜像   \\查看容器或者镜像的底层信息，元数据，比如查看ip、主机名、数据卷、CMD等信息
          docker logs [-f]   \\查看容器内部进程的日志


​          
```

构建镜像：

基于一个容器构建一个新镜像

1.运行一个基于（Centos/Ubuntu/alpine）启动一个容器，在容器内部执行更改操作，比如安装一个工具或者服务！
2.使用docker commit 将容器提交更改并生成一个新的镜像，比如有个叫ztt的容器，基于它创建一个镜像nginx:1.0
例子：docker  commit  ztt  nginx:1.0

补全命令：

yum -y install bash-completion-extras.noarch pletion

### **数据卷**

```
数据卷的增删改查
docker volume create 卷名    //创建一个数据卷
						 ls				   	//查看已有的数据卷
						 rm 				 //删除一个或多个数据卷
						 prune				 //删除所有未被使用的数据卷
						 inspect		 	  //显示一个或者多个卷的详细信息
默认创建的数据卷放在：/var/lib/docker/volume
数据卷的服务对象是容器，当容器创建的时候可以指定挂在那个卷
docker run --name wed1 -d -p 80:80  -v html:/usr/share/nginx/html  10.30.5.120/docker/nginx
```



### **匿名卷**

```
自动创建
docker run --name wed1 -d -p 80:80 -v /usr/share/nginx/html  10.30.5.120/docker/nginx
我们也可以在构建镜像的时候，将一些重要的目录里设置为挂载点，如果容器内某个目录被定义为挂载点，name在创建的时候，这个挂载点，如果不指定挂载数据卷的话，那么将会自动挂载一个匿名卷到挂载点，保证这个挂载点下的数据肯定是写入到卷当中的！
```

Docker部署wordpress

需要运行两个容器，一个mysql容器一个wordpress容器，他们都有自带的一些变量，方便我们去部署他们

#####################################################################################

```
mysql镜像内置变量
    WORDPRESS_DB_HOST							//MySQL数据库主机IP地址
    WORDPRESS_DB_PORT							//MySQL服务的端口
    WORDPRESS_DB_NAME							//数据库名字
    WORDPRESS_DB_PASSWORD                  //数据库密码
    WORDPRESS_DB_DATABASE					//创建数据库名
```

创建MySQL容器

```
docker run --name mysql -d -p 3306:3306 -v data:/var/lib/mysql  \
> -e MYSQL_ROOT_PASSWORD=123 \
> -e MYSQL_DATABASE=wordpress \
> -e MYSQL_USER=tom \
> -e MYSQL_PASSWORD=123456  --restart always  10.30.5.120/docker/mysql:5.6
```

#####################################################################################

```
wordpress镜像内置的变量
	WORDPRESS_DB_HOST            \\MySQL数据库主机ip地址
	WORDPRESS_DB_PORT				\\Mysql服务的端口
	WORDPRESS_DB_NAME				\\数据库的名字
	WORDPRESS_DB_USER               \\登录MySQL的用户
	WORDPRESS_DB_PASSWORD            \\登录用户密码
```

```
创建wordpress容器
docker run --name wordpress -d -p 80:80 \
-e WORDPRESS_DB_HOST=192.168.189.171 \
-e WORDPRESS_DB_NAME=wordpress \
-e WORDPRESS_DB_USER=tom \
-e WORDPRESS_DB_PASSWORD=123456 --restart always --link mysql 10.30.5.120/docker/wordpress
```

