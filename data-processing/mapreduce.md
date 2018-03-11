# Hadoop
hadoop是一个大数据解决方案。核心包括，hdfs负责大数据存储，mapreduce负责数据运算。

## hdfs
集群中有两类机器：namenode和datanode。
namenode负责保泽元数据的基本信息
datanode负责存放数据本身

## MapReduce
是Google提出的一个软件架构，用于大数据集的并行运算。Map和Reduce的思想是从函数式编程里面借来的。
集群中有两类机器：jobtracker和tasktracker
jobtracker负责分发任务
tasktracker负责执行任务

## hdfs和mapreduce
都对应了master/slave架构。

## Hive
定义了类似于SQL的查询语言（HQL），把SQL转化为MapReduce任务在Hadoop上面执行，一般用于离线分析。

## FLume日志收集

## Zookeeper
负责分布式环境下数据管理：统一命名，状态同步，集群管理，配置同步。

## hbase
hbase负责随机读写大数据，hdfs只能随机读。



# MapReduce算法实现
Map和Reduce之间通过Key来链接，通过Shuffle操作来保证每个Reducer的输入是同一个key或者同一组keys。

## Shuffle原理
把map的输出，根据key不断地merge，最后分配给reducer。

## 性能瓶颈
磁盘I/O。map的计算是靠近数据的存储位置。

## 写法注意
全局的排序问题，在Map端排序一次，在交给reduce，减少reduce的工作量。
确保每个Reducer的输入是按键排序的

## TopK问题
统计+排序（单机可以用：快速选择，堆排序）
