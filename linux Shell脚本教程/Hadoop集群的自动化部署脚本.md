# Hadoop集群的自动化部署脚本

hellmonky

## 自动化部署需求：
目前准备使用Hadoop原生包替换原来支持自动化部署的CDH包，所以在搭建集群的时候需要用bash脚本来完成自动化部署。
之所以使用原生Hadoop包进行替换，原因在于CDH套件需要使用的资源过大，造成对服务器的负担。从当前使用的服务主要为存储服务来看，CDH套件的很多组件并没有用上，反而需要耗费很多的资源，那么从原生出发，就可以最小限度的压缩不需要的组件，并且方便自己定制。

## bash自动化部署脚本编写过程：
在确定了需要自动化部署的方案之后，就需要选择方案：采用linux系统脚本、采用程序脚本和使用自动化部署工具。最后确定使用bash脚本来完成自动化部署工作。

### 自动化部署脚本编写思路：
所谓的自动化部署脚本，就是让运行环境的搭建按照预设的步骤和方法逐步执行，并且在这个过程中可以使用外部定义的一些变量来修正细节，但是不会改变整体流程。那么这个过程就像一个剧本，演员就是子脚本或者具体的执行代码块，可以根据环境来即兴添加一些修饰，但是整个故事还是要按照剧本编写的来严格执行。
为了让整个脚本可以流畅和流程化的执行，就一定先整理清楚整个剧本的关键点和主要流程，这样在把握了关键点的前提下来组织各个流程来最终完成脚本。

#### 首先，需要明确自动化脚本要达到的自动化程度
在使用自动化部署过程中，一定要明确自动化的程度，只有确定了边界才不会越做越麻烦。
因为脚本可以方便的完成很多事情，那么对自动化的程度的预期也会随着可以完成的事情而膨胀，这个时候一定要先确定自动化的边界是哪里，这样在确定整个方案的时候就能控制变化。
然后在这个基础上考虑后续的扩展性，这样才能更为脚踏实地的设计，快速的完成。
讨论后，确定了自动化的过程为：从一个proxmox镜像克隆出整个集群的所有节点，然后在每一个节点上执行脚本来完成这个节点的初始化和安装，再到每一个节点上执行服务启动，最后还是在每一个节点上完成服务的停止。
也就是说，这个脚本完成了对每一个节点初始化设置，每一个节点的服务启动，集群的基础服务启动和集群的服务关闭的功能。

#### 其次，需要将脚本的主要流程整理出来
确定了自动化脚本要达到的功能之后，就将这个功能拆解，分成独立的步骤。


#### 接着，逐一实现各个主要流程的具体脚本代码

#### 最后，将整个自动化过程用主要流程搭建起来


### 关于自动化脚本的测试：



## 使用脚本语言完成自动化部署：

## 相关知识：

HDFS服务启动和重新格式化：
(1)首先关闭SSH的yes确认：
参考：[How can I avoid SSH's host verification for known hosts?](http://superuser.com/questions/125324/how-can-i-avoid-sshs-host-verification-for-known-hosts)
编辑/root/.ssh文件夹下的config，添加：
StrictHostKeyChecking no
然后删除known_hosts文件，重启sshd服务：
systemctl sshd restart
(2)然后删除hdfs主节点上的name，data和log：
按照hadoop中的hadoop.tmp.dir值进入目录清空
(3)然后删除datanode上的数据：
按照hadoop中的hadoop.tmp.dir值进入目录清空
(4)最后，在主节点格式化：
hadoop namenode -format
(5)重启dfs服务：
./start-dfs.sh

参考：[Hadoop中重新格式化namenode](https://my.oschina.net/HIJAY/blog/220816)

在HDFS中新建目录，并且提供读写权限：
默认创建文件夹后的权限为：
Permission	Owner	Group	    Size	Replication	    Block Size	Name
drwxr-xr-x	root	supergroup	0 B	    0	            0 B	        datasong

使用777更改权限后：
Permission	Owner	Group	    Size	Replication     Block Size	Name
drwxrwxrwx	root	supergroup	0 B	    0	            0 B	        datasong





