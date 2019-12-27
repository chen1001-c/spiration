# **Ansible**

## **一.单元 Ansible简介和安装**

### **1 - Ansible是什么？**

关于Ansible

Ansible是一种IT自动化工具。它可以帮助我们批量配置系统，部署软件以及协调更高级的IT任务，例如连续部署或零停机滚动更新。

Ansible的主要目标是让工作变得简单和易操作，它同时也非常关注安全性和可靠性，传输过程是基于**openssh**来实现的，保证了传输的数据的安全性！大大降低安全风险！

### **2 - Ansible的特点**

Ansible采用**无代理方式（agentless）**管理机器，因为Ansible的**通信是通过**openssh来实现的，所以你无需考虑如何远程升级受管机器的代理程序！只要可以保证openssh可以正常通信即可！因为现在几乎所有的**Linux平台都自带了openssh**，Ansible在部署阶段无需考虑在远程机器上安装客户端软件！这样极大的减**少了前期部署的工作**！

Ansible有丰富的模块**可以让你直接使用，当然在Ansible的社区也有很多优秀的开发者在贡献新的模块，所以你总会找到适合自己的模块，当然你也可以自己开发模块！

**Ansible是使用python开发**，所以关于Ansible的二次开发和模块开发成本相对较低

### **3 - Ansible的工作流程**

![img](D:\有道云笔记\c13522837182@163.com\896f3cc3d80b4ef8b14bf1df48b35ff0\wps1.jpeg)

 

### **4  - Ansible的一些基本概念**

#### **1 - 控制节点**

任何装有Ansible的机器都可以叫做控制节点。您可以从任何控制节点调用/usr/bin/ansible执行一条任务，或执行/usr/bin/ansible-playbook命令读取剧本执行多个任务

#### **2 - 受管节点**

使用Ansible管理的的网络设备和服务器，都可以叫做受管节点！受管节点有时也可以叫做“主机“，受管节点无需安装ansible

#### **3 - 清单（** inventory **）**

受管节点的列表。Ansible在管理某个节点前，需要先将节点添加到清单文件中！清单文件有时也称为“主机清单文件”。清单文件可以为每个受管节点指定信息，例如IP地址、端口等信息！也可以把主机分成主机组管理！

#### **4 - 模块（Modules）**

Ansibe执行代码的单位。Ansible自带了很多模块，每个模块都有特定的用途。我们可以通过任务调用单个模块，例如shell模块，可以调用shell命令在管理主机执行。

也可以在剧本中调用多个不同的模块！想要了解更多模块信息可以访问官方模块列表地址：[https://docs.ansible.com/ansible/latest/modules/modules_by_category.html#modules-by-category](#modules-by-category)

#### **5 - 任务（Tasks）**

Ansible执行的单位，可以使用临时命令一次执行一个任务

#### **6 - 剧本（Playbooks）**

任务的有序列表文件，所以我们可以重复读取剧本文件重复运行剧本内的任务！这个是我们执行任务的主要方式

### **5 - Ansible的安装**

环境要求

Ansible要求主机上有Python2.7或者python3.5以上的环境，在Red Hat，Debian，CentOS，macOS，任何BSD等系统上可以直接安装。但是控制节点不支持windonws平台！

我们这里准备3台Centos系统的虚拟机，一台为Centos7用来安装Ansible扮演我们的控制节点，另外两台我们可以使用Centos6，扮演受管节点

#### **1 - 在Centos上安装控制节点**

```
在Centos6版本的系统上ansible安装包还未被加入到yum的base源中，**需要安装epel源之后才可以安装ansible
yum -y install epel-release
yum -y install ansible
```

```
在Centos7上时，ansible安装包已经被加入到了yum的base源中，所以可以直接使用yum安装
yum -y install ansible
```

```
新版本安装包可以去官方获取：
https://releases.ansible.com/ansible/rpm/release/epel-7-x86_64/
```

当然安装方式还支持源码安装，我们可以去Github上获取源码或者使用python的pip安装都是可以的：

大家可以参考官方的文档：[https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#what-version-to-pick](#what-version-to-pick)

Ansible安装完毕后可以直接使用，无需启动！

#### **2 - 在受管节点要注意的事项**

```
在受管节点上，您需要一种通信方式，通常是ssh，还需要有Python 2（2.6版或更高版本）或Python 3（3.5版或更高版本）
这些环境在Centos6以上版本的系统上都是默认满足的！所以可以不用做任何配置！
但是如果受管节点上启用了SElinux，那么需要安装libselinux-python，这个我们可以直接使用yum安装：
yum -y install libselinux-python
```

#### **3 - ssh无密码连接配置**

控制节点在和受管节点在通信时是通过openssh建立的，所以控制节点在和受管节点建立通信时肯定需要账号和密码的认证！每次执行任务都需要输入账号和密码在使用过程当中是很不方便的！所以我们这里要建立起控制节点和受管节点的授信配置，通过公钥认证来实现控制节点和受管节点ssh的无密码连接！

```
在控制节点操作：
生成密钥对
ssh-keygen -t rsa
```

```
拷贝公钥到受管节点
ssh-copy-id  root@ip
```

首次拷贝需要再输入一次密码才可以将公钥复制过去，输入完毕后以后再连接就不需要输入账号密码了！

#### **4 - 编辑主机清单文件（I**nventory**）**

我们需要将所有受管节点**以主机名或者ip的形式添加的主机清单文件**中

```
主机清单文件安装后默认存放路径：/etc/ansible/hosts
例如如下格式添加：
192.0.2.50
aserver.example.org
bserver.example.org
```

```
当然我们也可以分组：
[webservers]
192.0.2.50
aserver.example.org
bserver.example.org
```

中括号中的webservers就是定义的组名，下面3台服务器是这个组的成员主机

```
我们也可以按如下格式添加主机
[webservers]
192.0.2.[50:100]
web[a:f]server.example.org
```

#### **5 - 测试**

```
ansible执行一条任务的语法格式:
ansible  主机/主机组  -m  模块  -a ‘模块的参数‘
```

```
我们使用ping模块ping清单文件中所有节点，查看是否可达
ansible all -m ping
```

有如下返回说明节点都可达，all代表所有主机

![img](D:\有道云笔记\c13522837182@163.com\fd17a44003804d37ae0a7d0e740c33ca\wps2.jpeg)

 

```
当然我们也可以指定组或者主机操作
ansible webservers -m ping
```

```
我们再来在受管节点执行一条命令，查看受管节点的ip信息
ansible all -a 'ifconfig'
```

发现我们这条命令没有指定调用哪个模块，那么他会使用默认模块，**默认模块为command,**作用是在受管节点执行普通命令

类似的模块还有很多，下面我们会列举一些常用的模块讲解！

#### **6 - Ansible的配置文件**

Ansible中的某些设置可以通过配置文件（ansible.cfg）进行调整，对于大多数环境默认配置就足够使用了，但是也可能会有一些特殊的原因我们需要修改这些配置参数！

配置文件路径

在Centos上yum安装的ansible，默认的配置文件路径如下：

**配置文件：**/etc/ansible/ansible.cfg

# Ansible模块**

## ping

```
ping模块用来检查目标主机是否在线
例子：ansible webserver -m ping
```

## yum

```
yum模块用来在Centos系统上使用yum命令安装软件包
选项：
	name: 指定安装包的名字
	state：latest 安装最新版  present 默认安装  installed 安装  absent 卸载
	removed 卸载
例子：ansible webservers -m yum -a ‘name=httpd state=latest’
```

## command

```
command模块用来执行系统命令，但是不支持shell下的特殊符号 如：| &&等
例子：ansible webservers -m command  -a ‘echo 李想’
```

## shell

```
shell模块和command模块使用方法基本一致，但是他可以支持shell的特殊符号，如： | && 等
例子：ansible webservers -m shell  -a “cd /opt/ && touch lixiang”
```

## service

```
service模块用来管理centos上的服务的启动、关闭、重启和重载
选项：
	name： 服务名字
	state：  started(启动)  stopped(停止) restarted(重启)  reloaded(重载)
	enabled： 默认是no，将服务设置为开机自启
例子：ansible wedservers -m service -a 'name=httpd state=started enabled=yes'
```

## file

```
file模块用来创建文件、目录、链接文件
选项：
    group：定义文件/目录的属组
    mode：定义文件/目录的权限
    owner：定义文件/目录的属主
    path：必选项，定义文件/目录的路径
    recurse：递归的设置文件的属性，只对目录有效
    src：要被链接的源文件的路径，只应用于state=link的情况
    dest：被链接到的路径，只应用于state=link的情况
    state：
        directory：如果目录不存在，创建目录
        file：即使文件不存在，也不会被创建
        link：创建软链接
        hard：创建硬链接
        touch：如果文件不存在，则会创建一个新的文件，如果文件或目录已存在，则更新其最后修改时间
        absent：删除目录、文件或者取消链接文件
   例子：ansible wedservers -m file -a 'path=/opt/ls state=touch'
```

## user

```
user模块用来创建用户
选项：
    home： 指定创建的家目录
    groups：指定用户组
    uid：指定UID
    password：设置密码，密码必须是密文
  		Openssl passwd
    name：创建的用户名字
        createhome：是否创建家目录(yes/no)
        state:  是创建还是删除。（present，absent），默认是创建
        shell： 指定用户登录的shell环境
        remove：删除用户家目录，默认为no
    group
        group用来创建用户组
    选项
        gid：指定用的gid。 
        name：指定用户名。 
        state：是创建还是删除。（present，absent） 

```

## copy

```
copy模块用来复制文件至目标主机
选项：
    src：文件在管理主机的据对路径或者相对路径
    dest：将文件复制到目标主机的路径
    backup：是否将目标主机的同名文件备份，默认为no
    mode: 授权
    directory_mode：递归授权
例子：
	ansible webservers -m copy  -a ‘src=/root/nginx.sh  dest=/opt/’
```

## unarchive

```
unarchive模块用来解压文件
选项：
    copy：在解压文件之前，是否先将文件复制到远程主机，默认为yes。若为no，则要求目标主机上压缩包必须存在
    creates：指定一个文件名，当该文件存在时，则解压指令不执行
    dest：远程主机上的一个路径，即文件解压的绝对路径。
    group：解压后的目录或文件的属组
    mode：解压后文件的权限
    src：如果copy为yes，则需要指定压缩文件的源路径
    owner：解压后文件或目录的属主
例子：
	ansible  webservers -m unarchive -a ‘src=/root/nginx.tar.gz  dest=/opt/ group=www ower=www mode=777 ’
```

## get_url

```
get_url模块，该模块主要用于从http、ftp、https服务器上下载文件（类似于wget
选项：
	url： 指定要下载的文件的URL地址
例子：
	ansible webservers -m get_url -a ‘url= http://nginx.org/download/nginx-1.15.7.tar.gz  dest=/root/’
```

## synchronize

```
使用rsync同步文件，将主控方目录推送到指定节点的目录下,使用此模块需要先安装rsync
delete： 删除不存在的文件，delete=yes 使两边的内容一样（即以推送方为主），默认no
src： 要同步到目的地的源主机上的路径; 路径可以是绝对的或相对的。如果路径使用”/”来结尾，则只复制目录里的内容，如果没有使用”/”来结尾，则包含目录在内的整个内容全部复制
dest：目的地主机上将与源同步的路径; 路径可以是绝对的或相对的。
dest_port：默认目录主机上的端口 ，默认是22，走的ssh协议。
mode: push或pull，默认push，一般用于从本机向远程主机上传文件，pull 模式用于从远程主机上取文件。
rsync_opts：通过传递数组来指定其他rsync选项。
```

## fetch

```
fetch模块它用于从远程机器获取文件，并将其本地存储在由主机名组织的文件树中。
选项：
    src：远程系统上要获取的文件。 这必须是一个文件，而不是一个目录。 后续版本可能会支持递归提取。
    dest：保存文件的目录
```

## setup

```
setup 模块用于收集远程主机的一些基本信息。
选项：
    filter参数：用于进行条件过滤。如果设置，仅返回匹配过滤条件的信息。
    常用的过滤关键词：
    ansible_all_ipv4_addresses：仅显示ipv4的信息
    ansible_devices：仅显示磁盘设备信息
    ansible_distribution：显示是什么系统，例：centos,suse等
    ansible_distribution_major_version：显示是系统主版本
    ansible_distribution_version：仅显示系统版本
    ansible_machine：显示系统类型，例：32位，还是64位
    ansible_eth0：仅显示eth0的信息
    ansible_hostname：仅显示主机名
    ansible_kernel：仅显示内核版本
    ansible_lvm：显示lvm相关信息
    ansible_memtotal_mb：显示系统总内存
    ansible_memfree_mb：显示可用系统内存
    ansible_memory_mb：详细显示内存情况
    ansible_swaptotal_mb：显示总的swap内存
    ansible_swapfree_mb：显示swap内存的可用内存
    ansible_mounts：显示系统磁盘挂载情况
    ansible_processor：显示cpu个数(具体显示每个cpu的型号)
    ansible_processor_vcpus：显示cpu个数(只显示总的个数)
    ansible_python_version：显示python版本
例子：
获取目标主机的ipv4地址
	ansible webservers -m setup -a 'filter=ansible_all_ipv4_addresses'
```

