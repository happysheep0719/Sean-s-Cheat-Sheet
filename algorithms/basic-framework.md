<extoc></extoc>

# Basic Framework

## 算法解题思路

- 使用**循环**拆成相同的子问题 - `loop`
- 使用**分类讨论**拆分多种情况 - `if-else`
- 使用**分治法(divide and conquer)**拆成**可继续拆分的子问题**直到**最小情况(base case)** - `recursion / iteration`

## Binary Search - 二分搜索

对`sorted array`类型的问题，拆分成同样的子问题，使用循环loop和分类讨论if-else实现。

__适用问题__

- 每次循环会减少解空间，不能死循环。
- 不能在循环中，把正确答案排除掉。

__Coding Tricks__

- __循环进入条件__
    - `start + 1 < end` - 取决于最后一次循环是否需要检查左右两个pivot确定答案
    - `start < end`
    - `start <= end`
    
- __调试方法__
    - 使用如下的会触发边界条件的例子测试, Eg. `[0]`, `[0, 1]`, `[0, 1, 2]`
    
- __二分计算__
        - `mid = start + (end - start) / 2`


### Basic Problems

- __P1. Binary Search in Sorted Array__

- __P2. Binary Search in 2D sorted matrix__

- __P3. Find the closest number to target__
    - 循环条件：`left < right - 1`
    
- __P4. Find the first occurance of target__

- __P5. Find the last occurance of target__

- __P6. Find the K closest number to target__
    — Find largest smaller or equal number.

- __P7. Find the smallest element that is larger than target__

### 复杂问题

- __P8. Find mountain peak in array: __

    `1 3 7 23 57 ... 100 99 86 44 32 21`

- __P9. Binary Search in a sorted array with unknown size__

    - Step 1 - jump out
    - Step 2 - jump in
    
    |    | step = 2 | step = 10 |
    |----|----|----|
    | Worst case | $n=2^{k-1}+1$ | $n=10^{k-1}+1$ |
    | Jump out - Time | $log_{2}n$ | $log_{10}n$ |
    | Jump in - Time | $log_{2}10n$ | $log_{2}2n$ |


### Binary Search Template
Reference: [jiuzhang](http://www.jiuzhang.com/solutions/binary-search/)

```java
/**
* @param nums: The integer array.
* @param target: Target to find.
* @return: The first position of target. Position starts from 0.
*/
public int binarySearch(int[] nums, int target) {
    # First consider the case that the input is null or empty array.
    if (nums == null || nums.length == 0) {
        return -1;
    }
    # initial condition. The end is included in the range of the num,
    # because the end is initialized to the length of nums minus one
    int start = 0, end = nums.length - 1;
    # Here, the condition should be start + 1 < end.
    # because when start == 0 and end == 1, then mid = 0
    # and the start may not be updated.
    while (start + 1 < end) { # Note: use start+1<end as the condition to continue
        int mid = start + (end - start) / 2;
        if (nums[mid] == target) {
            end = mid;
        } else if (nums[mid] < target) {
            start = mid;
            // or start = mid + 1
        } else {
            end = mid;
            // or end = mid - 1
        }
    }
    # When the loop is end, decide where the first postion of target is.
    if (nums[start] == target) {
        return start;
    }
    if (nums[end] == target) {
        return end;
    }
    return -1;
}
```

## Divide and Conquer - 分治法

__适用问题__

- 问题缩小到一定规模可以很容易的被解决，子问题相互独立。
- 问题可以分解为若干个规模较小的相同问题，即该问题具有**最优子结构**性质
- 利用该问题分解出的子问题的解可以合并为该问题的解。
- 该问题所分解出的各个子问题是相互独立的，即子问题之间不包含公共的子问题。

__基本问题__

- 是很多算法的基础（快速排序、归并排序）。
- 二叉树相关问题 - 使用二叉树的数据结构目的是，在解决问题时可以用分治法提高速度。

__三个步骤__

- **Divide 分解** - 将原问题分解为若干子问题，这些子问题都是原问题规模较小的实例。
- **Conquer 解决** - 递归地求解各子问题。如果子问题规模足够小，则直接求解。**base case**
- **Combine 合并** - 将所有子问题的解合并为原问题的解。

__Conquer 的顺序__

- recursion 递归 / iteration 迭代
- DFS 纵向 / BFS 横向

### Recursion Template

__Note:__

- The size of call-function is 8M.
- All recursive algorithms can be written as a _iterative_ version. Recursive version is a version using the system's call-function stack.

Example: 
[Subsets Problem](http://www.lintcode.com/zh-cn/problem/subsets-ii/#)
[Subsets Solution](http://www.jiuzhang.com/solutions/subsets/)

```python
# 1. recursive helper parameter and return type
# for return type, if we needs to record a max or min,
# we can use a global varible or put it both in the parameters and return type.
# Eg. subsets problem
# thisnode = (subsetStart, startIndex)
# background = nums
def recurhelper(background, thisnode, results):
    # 2. recursive helper exit
    if GOAL_TEST(thisnode):
        results.add(thisnode)
    
    # 3. expand this node and call recurhelper recursively.
    # EXPAND function returns hard copy of nodes
    for node in EXPAND(thisnode):
        recurhelper(background, node, results)
    
    return results
```

### Generic Tree Search Algorithm (BFS and DFS)

Reference - [USC-CSCI561-Lecture-Week2]

```c
function TREE_SEARCH(problem) return a solution or failure

frontier <- MAKE_QUEUE(MAKE_NODE(problem.INITIAL_STATE))
loop do
    if ISEMPTY(frontiers) then return failure
    node <- REMOVE_FIRST(frontiers)
    if problem.GOAL_TEST() applied to node.STATE succeeds
        then return SOLUTION(node)
    frontiers <- INSERT_ALL(EXPAND(node, problem), frontiers)
```

__Note:__

- Always remove elements from the front
- BFS places new elements at the end of the queue. FIFO.
- DFS places new elements at the front of the queue(stack). LILO.