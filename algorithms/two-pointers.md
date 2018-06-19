<extoc></extoc>

# Two Pointers

[jiuzhang Chapter 7]

- 使用`Pivot`分隔数组。
- 使用**循环**`loop`不断地移动指针`pivot`。
- 使用**分类讨论**`if-else`控制指针`pivot`的移动。

__适用问题__

- 要求space complexity为$$O(1)$$的问题

__问题类型__

- **同向双指针**
    - Array Deduplication
    - Remove leading/tailing spaces
    - Two Sum
- 相向双指针
    - Cannot reserve the initial order of the array
- Partition - Quick Select
    - k-th smallest
- 双数组双指针
    - k-th smallest in two sorted array

    

## 同向双指针 

Problems:

- P1. Remove Particular Char    
- P2. Remove all leading/trailing and duplicate empty spaces
- P3. Remove duplicated and adjacent letters but keep at most one
    - Follow-up. Remove duplicated and adjacent letters but keep at most two
    - Follow-up. Remove duplicated and adjacent letters and keep none
        - use two fast pointers to check the duplicated elements
- P4. Remove duplicated and adjacent letters repeatedly

- Use extra data structure, eg. array/queue/stack
    - compare the end of the Queue and the fast pointed element
    - compare the top of the Stack and the fast pointed element
- **In-place** way of two pointers
    - **a good way of split the array: [0, s), [s, f), [f, len)**
        - imagine the index of the slow pointer is the length of new array
        - if excluding the slow pointer, we do not need to think about too many corner cases
        - usually comes with `s++`
        - if including the slow pointer, use ++s
    - move the fast pointer for each time
    - not necessarily move the slow pointer
    
## 相向shuangzhizh

### 2-Sum

- 证明：循环证明。有点绕，大概意思就是所有被排出的数都可以被之前被排除的数的结论推导得到。
    - assume we have Xi0 + Yj0 < t
    - then we got: for all Xi < Xi0, Xi + Yj0 < t
    - all Xi < Xi0 are excluded with Yj >= Yj0 under only one situation that Xi + Yj < t
        - that is, for all Xi < Xi0, exists Yj1 >= Yj0 that Xi + Yj1 < t
    - for Yj > Yj1, it is excluded with Xi1 <= Xi0 under only one situation that Xi1 + Yj1 < t
        - that is, for all Yj > Yj1, exists Xi2 <= Xi1 that Xi2 + Yj > t
    - conclusion: for all Xi < Xi0, we have Yj >= Yj0, Xi + Yj != t
    
    
    