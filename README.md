# 单机搭建Hadoop集群
Hadoop的master和slave分别运行在不同的Docker容器中，其中hadoop-master容器中运行NameNode和ResourceManager，hadoop-slave容器中运行DataNode和NodeManager。NameNode和DataNode是Hadoop分布式文件系统HDFS的组件，负责储存输入以及输出数据，而ResourceManager和NodeManager是Hadoop集群资源管理系统YARN的组件，负责CPU和内存资源的调度。

# 构建镜像

下载docker镜像

	sudo docker pull sciatta/hadoop:2.7.2.RELEASE

或者通过Dockerfile构建

	git clone https://github.com/sciatta/hadoop-cluster-docker.git
	cd hadoop-cluster-docker
	sudo docker build -t sciatta/hadoop:2.7.2.RELEASE .

# 运行

下载GitHub仓库

	git clone https://github.com/sciatta/hadoop-cluster-docker.git

创建Hadoop网络

	sudo docker network create --driver=bridge hadoop

运行Docker容器

	cd hadoop-cluster-docker
	sh ./start-container.sh

运行结果

	start hadoop-master container...
	start hadoop-slave1 container...
	start hadoop-slave2 container...
	root@hadoop-master:~#

* 启动了3个容器，1个master，2个slave
* 运行后就进入了hadoop-master容器的/root目录

启动Hadoop，运行wordcount

	sh ./start-hadoop.sh
	sh ./run-wordcount.sh

运行结果

	input file1.txt:
	Hello Hadoop
	input file2.txt:
	Hello Docker
	wordcount output:
	Docker	1
	Hadoop	1
	Hello	2

Hadoop网页管理地址

	NameNode: http://192.168.0.29:50070/
	ResourceManager: http://192.168.0.29:8088/

* 192.168.0.29为运行容器的主机IP。

# N节点Hadoop集群搭建步骤

指定容器数量CONTAINERNO，可以任意指定CONTAINERNO（CONTAINERNO>1）

	export CONTAINERNO=5

重新构建Docker镜像

	sh ./resize-cluster.sh $CONTAINERNO

启动Docker容器

	sh ./start-container.sh $CONTAINERNO

启动Hadoop，运行wordcount

	sh ./start-hadoop.sh
	sh ./run-wordcount.sh