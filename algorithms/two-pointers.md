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
    
## 相向双指针

### 2-Sum

## Two Pointers in two arrays

### Common element problems

Assumptions:

- optimized time or space?
- sorted or unsorted?
- duplicate?
- keep one or all?
- data size
- data type

What about optimized time?

- if we only keep one element: use a hashset
- time O(n) space O(n)

What if the arrays are already sorted?

- use two pointers
- time O(n) space O(1)

What if the arrays are already sorted, but the size are very different(m<<n)?

- binary search
- for each element in the small array, do a binary search in the large array
- time O(m log n)

What if unsorted, but we want to optimize space?

- sort them first
- what if the data range is very limited?
    - array[26]
    
#### find common elements in 3 sorted arrays of similar size

#### find common elements in k sorted arrays of similar size

Different from **k-way merge**

Solution 1: iterative

- time O(kn)
- space O(n)

Solution 2: Binary Reduction

- time (1 + 1/2 + 1/4 + ...) * kn = O(kn)
- space O(kn)

// Not an useful method
Solution 3: Min Heap

- time O(kn * logk)
- space