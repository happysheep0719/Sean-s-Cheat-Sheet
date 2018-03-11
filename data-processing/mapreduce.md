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

# 算法实现
## TopK问题
统计+排序（单机可以用：快速选择，堆排序）

## 写法注意
在Map端排序一次，在交给reduce，减少reduce的工作量。