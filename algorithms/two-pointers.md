<extoc></extoc>

# Two Pointers

[jiuzhang Chapter 7]

- 使用`Pivot`分隔数组。
- 使用**循环**`loop`不断地移动指针`pivot`。
- 使用**分类讨论**`if-else`控制指针`pivot`的移动。

__适用问题__

- 要求space complexity为$$O(1)$$的问题

__问题类型__

- 同向双指针 - Two Sum
- 相向双指针
- Partition - Quick Select
    - k-th smallest
- 双数组双指针
    - k-th smallest in two sorted array

    

## 同向双指针
    
P1. Remove Particular Char    
P2. Remove all leading/trailing and duplicate empty spaces
P3. Remove duplicated and adjacent letters
P4. Remove duplicated and adjacent letters repeatedly


第一层次：使用额外的数据结构

第二层次：in-place双指针，每次一定移动fast指针

案例1

- 使用额外的Queue - P1/P2/P3
    - 比较Queue的结尾和i指针的元素
- slow指针选择性移动（右移/不移）

案例2

- 使用额外的Stack - P4
    - 比较Stack的栈顶和i指针的元素
- slow指针（右移/不移/左移）

