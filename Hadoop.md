# Hadoop

[TOC]



## 什么是Hadoop？

1. Hadoop是Apache旗下的一套开源的**软件平台**
2. Hadoop可以利用**服务器集群**，根据用户的自定义业务逻辑，对**海量数据**进行分布处理



## Hadoop的核心模块：

四大核心，三大模块(除去common)

1. Common 支持hadoop模块的常用工具
2. HDFS 分布式文件系统，可以提供应用程序的高吞吐量访问
3. YARN 分布式作业（资源）调度系统
4. MapReduce 一种用于**并行**处理大型数据集的计算框架，基于yarn资源调度系统



## Hadoop生态圈

广义上来说，hadoop通常指的是一个更广泛的概念——hadoop生态圈

![aa11dbf4af93433fb0c1910c0a233729_th](/Users/xiajun/Downloads/aa11dbf4af93433fb0c1910c0a233729_th.jpg)



#### 个人理解：

hadoop生态可以分为4层

1. 存储层——HDFS 一个系统中最重要的就是文件系统了
2. 资源管理层——YARN
3. 逻辑/计算层——MapReduce、Spark
4. 最顶层——基于MapReduce、Spark等计算引擎的高级封装及工具，如Hive、Pig、Mahout等等

我是类比着一个Web应用看的 。存储层相当于我们的数据库（当然这里是文件），Yarn负责从我们的存储中获取我们需要的资源，而MapReduce使用我们获取的资源进行一系列运算。得出来的结果可以供别人进行使用，比如机器学习，人工智能之类的balabala。




**HDFS**：分布式存储系统

**YARN**：分布式资源调度系统

**MapReduce**：分布式计算框架

**Hive**：数据仓库工具

**HBase**：分布式海量存储数据库

**zookeeper**： 分布式协调服务

**flume**： 分布式日志采集工具

**sqoop**：数据导入导出工具

**mahout**：机器学习算法库

**oozie/azkaban**：工作流调度平台



#### 什么是分布式系统？

分布式系统会划分成**多个子系统或者模块**，各自运行在不同的机器上，子系统或模块之间**通过网络通信进行协作**，实现最终的**整体功能**。



## HDFS

**设计思想：**

分而治之：将大文件、大批量文件，分布式存放在大量服务器上，以便于采用分而治之的方式对海量数据进行运算分析

**作用：**为各类分布式运算框架（MapReduce、Spark…）提供数据存储服务

**重点概念：**文件切块，副本存放，元数据



### 概念

首先，它**是一个文件系统**，用于存储文件，通过统一的命名空间——目录树来定位文件
其次，它是**分布式**的，由很多服务器联合起来实现其功能，集群中的服务器有各自的角色：

namenode——HDFS集群主节点

datanode——HDFS集群存储节点

secondarynamenode——HDFS集群**检查节点**   *<u>==和namenode不一样==</u>

*关于这几个角色的详细介绍后续补充*...



### 重要特性

1. HDFS中的文件在物理上是**分块存储（block）**，块的大小可以通过配置参数( dfs.blocksize)来规定，默认大小在hadoop2.x版本中是128M，老版本中是64M **

2. HDFS文件系统会给客户端提供一个**统一的抽象目录树**，客户端通过路径来访问文件，形如：hdfs://namenode:port/dir-a/dir-b/dir-c/file.data

3. **目录结构及文件分块位置信息(元数据)**的管理由namenode节点承担

   namenode是HDFS集群主节点，负责维护整个hdfs文件系统的目录树，以及每一个路径（文件）所对应的block块信息（block的id，及所在的datanode服务器）

4. 文件的各个block的存储管理由datanode节点承担

   datanode是HDFS集群从节点，每一个block都可以在多个datanode上存储多个副本（副本数量也可以通过参数设置dfs.replication）

5. HDFS是设计成适应一次写入，多次读出的场景，且不支持文件的修改

> 综上，HDFS适合用来做数据分析，并不适合用来做网盘应用，因为不便修改，延迟大，网络开销大，成本太高了



关于HDFS集群搭建&HDFS常用命令，请移步[Hadoop集群搭建]()



## MapReduce



## YARN

