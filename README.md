# �����Hadoop��Ⱥ
Hadoop��master��slave�ֱ������ڲ�ͬ��Docker�����У�����hadoop-master����������NameNode��ResourceManager��hadoop-slave����������DataNode��NodeManager��NameNode��DataNode��Hadoop�ֲ�ʽ�ļ�ϵͳHDFS����������𴢴������Լ�������ݣ���ResourceManager��NodeManager��Hadoop��Ⱥ��Դ����ϵͳYARN�����������CPU���ڴ���Դ�ĵ��ȡ�

# ��������

����docker����

	sudo docker pull sciatta/hadoop:2.7.2.RELEASE

����ͨ��Dockerfile����

	git clone https://github.com/sciatta/hadoop-cluster-docker.git
	cd hadoop-cluster-docker
	sudo docker build -t sciatta/hadoop:2.7.2.RELEASE .

# ����

����GitHub�ֿ�

	git clone https://github.com/sciatta/hadoop-cluster-docker.git

����Hadoop����

	sudo docker network create --driver=bridge hadoop

����Docker����

	cd hadoop-cluster-docker
	sh ./start-container.sh

���н��

	start hadoop-master container...
	start hadoop-slave1 container...
	start hadoop-slave2 container...
	root@hadoop-master:~#

* ������3��������1��master��2��slave
* ���к�ͽ�����hadoop-master������/rootĿ¼

����Hadoop������wordcount

	sh ./start-hadoop.sh
	sh ./run-wordcount.sh

���н��

	input file1.txt:
	Hello Hadoop
	input file2.txt:
	Hello Docker
	wordcount output:
	Docker	1
	Hadoop	1
	Hello	2

Hadoop��ҳ�����ַ

	NameNode: http://192.168.0.29:50070/
	ResourceManager: http://192.168.0.29:8088/

* 192.168.0.29Ϊ��������������IP��

# N�ڵ�Hadoop��Ⱥ�����

ָ����������CONTAINERNO����������ָ��CONTAINERNO��CONTAINERNO>1��

	export CONTAINERNO=5

���¹���Docker����

	sh ./resize-cluster.sh $CONTAINERNO

����Docker����

	sh ./start-container.sh $CONTAINERNO

����Hadoop������wordcount

	sh ./start-hadoop.sh
	sh ./run-wordcount.sh