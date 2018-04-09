<extoc></extoc>

# Time & Space Complexity Analysis

## 分析方法

- **展开recursion tree进行分析，注意不是针对binary tree分析。**

Eg. isIdentical 四叉树 in Class 03/24

- **注意分析Worst Case**


## Time Complexity Analysis

Step 1 - **分析每个节点花的时间。**
Step 2 - **分析每层花的总时间。**

### Amortized Time Complexity- 平均用时分析方法

一次大量耗时的Action为之后很多次Action节省时间。
注意：Amortized time仍然可能有worst case， Amortized分析只针对不适合对算法的单次操作进行分析。

## Space Complexity Analysis
**分析Call Stack占用的最大内存大小**