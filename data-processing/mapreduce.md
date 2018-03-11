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

## 如何解决数据倾斜
单机的运行时间远超于其他单机。
A. 调整计算并行度：把数据量大的partition的数据分开，用不同的task处理。
具体实现：比如可以自定义partition，groupbykey的时候如果单个partition太大，就hash到其他地方。

B. 输入数据分配时处理
大表小表join时：把小的表放在左边，使用leftjoin。
大表大表join时：把造成数据倾斜的空值key，随机分配到不同的reduce上。
把有数据量大、多条重复key的数据，进行hash拆解为几个数据量小的key。但是会可能增加shuffle的工作量。

## 写法注意
全局的排序问题，在Map端排序一次，在交给reduce，减少reduce的工作量。
确保每个Reducer的输入是按键排序的

## TopK问题
统计+排序（单机可以用：快速选择，堆排序）
