## PlayBook

Ansible是新出现的自动化运维工具,基于Python开发,集合了众多运维工具（puppet、cfengine、chef、func、fabric）的优点,实现了批量系统配置、批量程序部署、批量运行命令等功能,ansible是基于模块工作的,本身没有批量部署的能力,真正具有批量部署的是ansible所运行的模块,ansible只是提供一种框架.

Playbook与Ad-Hoc相比,是一种完全不同的运用方式,而且是非常强大的,也是系统ansible命令的集合,其利用yaml语言编写,运行过程ansbile-playbook命令根据自上而下的顺序依次执行,简单来说Playbook是一种简单的配置管理系统与多机器部署系统的基础,与现有的其他系统有不同之处,且非常适合于复杂应用的部署.

## PlayBook语法实例

playbook是由一个或多个play组成的列表,play的主要功能在于将事先归并为一组的主机装扮成事先通过Ansible中的tasks定义好的角色(play的内容被称为tasks,即任务),从根本上来讲所谓tasks无非是调用Ansible的一个module,将多个play组织在一个playbook中即可以让它们联同起来按事先编排的机制一同工作.

下面来看一个基础的playbook,其中只包含一个tasks任务:

```
---
- hosts: web_server                   #指定执行的主机组  
vars:                               #声明了2个变量  
  http_port: 80  
  max_clients: 200  
remote_user: root                   #使用root权限执行   
tasks:  
- name: ensure apache is at the latest version   
  yum: pkg=httpd state=latest  
- name: write the apache config file  #将apache配置文件拷贝到指定主机    
  template: src=/etc/httpd/conf/httpd.conf dest=/etc/httpd.conf    
  notify:                             #当上面拷贝工作完成以后,执行消息发送    
  - restart apache  - name: ensure apache is running      #设置开机自启动    
  service: name=httpd state=started 
handlers:    
  - name: restart apache             #接收消息,并执行重启apache服务      
  service: name=httpd state=restarted
```

第一行中,文件开头为---,这是YAML将文件解释为正确的文档的要求,YAML允许多个文档存在于一个文件中,每个文档由 --- 符号分割,但Ansible只需要一个文件存在一个文档即可,因此这里需要存在于文件的开始行第一行.

YAML对空格非常敏感,并使用空格来将不同的信息分组在一起,在整个文件中应该只使用空格而不使用制表符,并且必须使用一致的间距,才能正确读取文件,相同缩进级别的项目被视为同级元素.

以 - 开头的项目被视为列表项目.作为散列或字典操作,它具有key：value格式的项,YAML文档基本上定义了一个分层的树结构,其中位于左侧是包含的元素.YAML文件扩展名通常为.yaml或者.yml,接下来,我们将分别讲解 playbook 语言的多个特性.

| 命 令 参 数  | 参 数 解 释                                                  |
| :----------- | :----------------------------------------------------------- |
| hosts        | 指定要执行指定任务的主机                                     |
| remote_user  | 指定远程主机上的执行任务的用户,此处的意思是以root身份执行    |
| user         | 与remote_user相同                                            |
| sudo         | 如果设置为yes执行该任务组的用户在执行任务的时候,获取root权限 |
| sudo_user    | 指定使用那个用户授权执行                                     |
| connection   | 通过什么方式连接到远程主机,默认为ssh                         |
| gather_facts | setup模块默认自动执行                                        |

![playbook](C:\Users\Administrator\Desktop\playbook.png)

![playbook语法](C:\Users\Administrator\Desktop\playbook语法.png)

![playbook-nginx](C:\Users\Administrator\Desktop\playbook-nginx.png)

