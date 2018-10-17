<extoc></extoc>

# Binary Search

__Two types of problems__

- Search problems in **Binary Search Tree** or **Sorted Array**
    - Using **Binary Search**
    - 广义的适用问题范围：每次循环会减少解空间，不能死循环；不能在循环中，把正确答案排除掉。
- Binary Search Tree operation problems

__Idea__

- 使用**循环**`loop`不断地移动指针`curr`。
- 使用**分类讨论**`if-else`控制指针`curr`的进入其中一个分支，扔掉一半的选项。

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
    - **使用一个元素的input调试，检测死循环**
    - 使用如下的会触发边界条件的例子测试, Eg. `[0]`, `[0, 1]`, `[0, 1, 2]`
- __二分计算__
    - `mid = start + (end - start) / 2`

### P1. Find the largest element that is smaller than target

```java
public int largestSmaller(int[] nums, int target) {
    if (nums == null || nums.length == 0) {
        return -1;
    }
    int left = 0, right = nums.length - 1;
    # Here, the entry condition should be left + 1 < right.
    # because when left == 0 and right == 1, then mid = 0
    # and the start may not be updated.
    while (left + 1 < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid;
        } else {
            right = mid - 1; // IMPORTANT
        }
    }
    if (nums[right] < target) {
        return right;
    }
    return left;
}
```

```java
public int largestSmaller(int[] nums, int target) {
    if (nums == null || nums.length == 0) {
        return -1;
    }
    int left = 0, right = nums.length - 1;
    int res = -1;
    # Here, the entry condition should be left + 1 < right.
    # because when left == 0 and right == 1, then mid = 0
    # and the start may not be updated.
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            res = mid;
            left = mid + 1;
        } else {
            right = mid - 1; // IMPORTANT
        }
    }
    return res;
}
```

### P2. Find smallest in a rotated sorted array

- test cases
    - `2 4 5 6 0 1`
    - `6 0 1 2 4 5`
- cases
    - case 1: `array[mid] > array[right]` => `array[left:mid]` is sorted and continue to search in `array[mid+1:right]`
    - case 2: `array[mid] < array[right]` => `array[mid:right]` is sorted and continue to search in `array[left:mid]`
- if we have duplication in input
    - case 3: `array[mid] == array[right]`
        - worst case - all the elements are the same

### P3. Binary Search in 2D sorted matrix

### P4. Find the first occurance of target

### Follow-up. Find the last occurance of target

### Follow-up. Find the closest number to target

### Follow-up. Find the K closest number to target

- Find largest smaller or equal number.
- Find the kth cloest number using linear scan or binary elimination

### P5. Find mountain peak in array

- `1 3 7 23 57 ... 100 99 86 44 32 21`
- 根据单调性来判断

### P6. Binary Search in a sorted array with unknown size

- Step 1 - jump out
- Step 2 - jump in

| | step = 2 | step = 10 |
|----|----|----|
| Worst case | $$n=2^{k-1}+1$$ | $$n=10^{k-1}+1$$ |
| Jump out - Time | $$log_{2}n$$ | $$log_{10}n$$ |
| Jump in - Time | $$log_{2}10n$$ | $$log_{2}2n$$ |

### P7. find the kth smallest / median in two sorted array

Binary Reduction on candidates

- xxxxxxxxxx   XXXXXXXXXX
- 0            m
- yyyyyyyyyy   YYYYYYYYYY
- 0            n
- move m or n to the right until $$m + n == k - 1$$
    - choose one from m and n by comparing the A[m2] and B[n2]
    - moving step initially set to `k`
    - moving step decrease by half for each time `k -> k - k/2`

### P7. find kth in unsorted array

Quick Selection

- `xxxxxxxxxxN` -> `xxxxxxxNyyy`
- partition the array into two parts
- remove one part from the two
- keep doing until the pivot is exactly at the kth position

