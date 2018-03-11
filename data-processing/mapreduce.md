# MapReduce
是Google提出的一个软件架构，用于大数据集的并行运算。Map和Reduce的思想是从函数式编程里面借来的。

## TopK问题
统计+排序

## 写法注意
在Map端排序一次，在交给reduce，减少reduce的工作量。