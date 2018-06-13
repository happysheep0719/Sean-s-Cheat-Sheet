<extoc></extoc>

# Binary Search - 二分搜索

__Two types of problems__

- Search problems in **Binary Search Tree** or **Sorted Array**
    - Using **Binary Search**
    - 广义的适用问题范围：每次循环会减少解空间，不能死循环；不能在循环中，把正确答案排除掉。
- Binary Search Tree operation problems

__Idea__

- 使用**循环**`loop`不断地移动指针`curr`。
- 使用**分类讨论**`if-else`控制指针`curr`的移动。

__Time Complexity in BST__

- `search` - worst case $$O(n)$$, average $$O(logn)$$
- `insert` - worst case $$O(n)$$, average $$O(logn)$$
- `remove` - worst case $$O(n)$$, average $$O(logn)$$

    Worst case happen if the binary tree is structured like a linked list.

    In **Balanced Binary Search Tree**, `search`, `insert` and `remove` operations are guaranteed to be $$O(logn)$$. For example, **AVL Tree**, **Red-Black Tree** are balanced BST.

__优化__

- 怎么样让BST效率更高？ - 更加Balanced
- **balanced binary search tree**
    - Eg. AVL tree, Red-black tree, etc 但是面试不会考定义，可能会借这个定义考基本能力。
    - Red-Black tree Implementations
        - in Java: TreeMap/TreeSet
        - in C++: map/set

-----
## Binary Search Problems

__Coding Tricks__

- __循环进入条件__
    - `left + 1 < right`
        - 取决于最后一次循环是否需要检查左右两个pivot确定答案
        - 需要做post processing
    - `left < right`
    - `left <= right`
- __调试方法__
    - 使用一个元素的input调试，检测死循环
    - 使用如下的会触发边界条件的例子测试, Eg. `[0]`, `[0, 1]`, `[0, 1, 2]`
- __二分计算__
    - `mid = start + (end - start) / 2`

### P1. Binary Search in Sorted Array

```java
public int binarySearch(int[] nums, int target) {
    if (nums == null || nums.length == 0) {
        return -1;
    }
    int start = 0, end = nums.length - 1;
    # Here, the entry condition should be start + 1 < end.
    # because when start == 0 and end == 1, then mid = 0
    # and the start may not be updated.
    while (start + 1 < end) {
        int mid = start + (end - start) / 2;
        if (nums[mid] == target) {
            end = mid;
        } else if (nums[mid] < target) {
            start = mid;
        } else {
            end = mid;
        }
    }
    if (nums[start] == target) {
        return start;
    }
    if (nums[end] == target) {
        return end;
    }
    return -1;
}
```

### Follow-up. Find the largest element that is smaller than target


### P2. Binary Search in 2D sorted matrix
### P3. Find the closest number to target
- 循环条件：`left < right - 1`
### P4. Find the first occurance of target
### P5. Find the last occurance of target
### P6. Find the K closest number to target
- Find largest smaller or equal number.

### P7. Find mountain peak in array
- `1 3 7 23 57 ... 100 99 86 44 32 21`

### P8. Binary Search in a sorted array with unknown size
- Step 1 - jump out
- Step 2 - jump in

| | step = 2 | step = 10 |
|----|----|----|
| Worst case | $$n=2^{k-1}+1$$ | $$n=10^{k-1}+1$$ |
| Jump out - Time | $$log_{2}n$$ | $$log_{10}n$$ |
| Jump in - Time | $$log_{2}10n$$ | $$log_{2}2n$$ |


-----
## Binary Search Tree Maintenance Problems

- 为什么BST里面没有重复数据？
    - 工业界中，BST是用来查找的。

- __P1. Insert in BST__
    - *Problem* : return the new root after the change.
    - corner case: if the root is null, return the new node.

- __P2. Delete in BST__
    - *Problem* : return the new root of the BST.
    - **Step 1**: find the node to be deleted
        - By transforming the problem into ONE sub problem that delete the key in one of the sub tree.
    - **Step 2**: delete the node
        - **case 1** - the node has no children.
        - **case 2** - the node has no left child.
        - **case 3** - the node has no right child.
        - **case 4** - the node has both left and right children.
            - The problem is transformed into three parts
            - **part 1**: find the largest node in the left subtree or the smallest node in the right subtree and record the replacement
            - **part 2**: delete the replacement in the tree - can be realized using recursive call. It must only hit one of case 1, case 2 and case 3.
            - **part 3**: set the children of the replacement