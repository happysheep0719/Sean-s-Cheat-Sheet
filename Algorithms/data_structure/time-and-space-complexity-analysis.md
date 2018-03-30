#

1. Recursive call分析

分析时间：对遍历的所有节点消耗时间的累加。
分析空间：call stack的最大长度，和call tree的深度有关系。

2. Amortized分析方法

一次大量耗时的Action为之后很多次Action节省时间。
注意：Amortized time仍然可能有worst case， Amortized分析只针对不适合对算法的单次操作进行分析。