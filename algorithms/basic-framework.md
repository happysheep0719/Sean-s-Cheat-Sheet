<extoc></extoc>

# Basic Framework

## 算法解题思路

- 使用**循环**拆成重复的子问题 - `loop`
- 使用**分类讨论**拆分多种情况 - `if-else`
- 使用**分治法(divide and conquer)**拆成**可继续拆分的子问题**直到**最小情况(base case)** - `recursion / iteration`

## Two Pointers - 双指针

- 使用`Pivot`分隔数组。
- 使用**循环**`loop`不断地移动指针`pivot`。
- 使用**分类讨论**`if-else`控制指针`pivot`的移动。

__适用问题__

- 要求space complexity为$O(1)$的问题


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