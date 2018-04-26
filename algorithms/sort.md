<extoc></extoc>

# Sorting Algorithms

-----
## Selection Sort
不断地选择剩余元素中的最小者。

- Step 1 - 找到数组中最小元素并将其和数组第一个元素交换位置。
- Step 2 - 在剩下的元素中找到最小元素并将其与数组第二个元素交换，直至整个数组排序。

__特点__

- 比较次数 = (N-1)+(N-2)+(N-3)+...+2+1~N^2/2
- 交换次数 = N
- **Time** = $$O(n^2)$$
- 运行时间与输入分布无关
- 数据移动最少

-----
## Merge Sort
将两个有序对数组归并成一个更大的有序数组。通常做法为递归排序，并将两个不同的有序数组归并到第三个数组中。典型的分治法应用


__特点__

- Divide Time = $$2n-1 = O(n)$$
- Merge Time = $$n * log2n = O(nlogn)$$
- Time = $$O(nlogn)$$
- Space = $$2n-1 = O(n)$$
- 需要使用额外的空间来存储归并后的数据

-----
## Quick Sort
快排是一种采用分治思想的排序算法，大致分为三个步骤。

- **定基准** - 首先随机选择一个元素最为基准
- **划分区** — 所有比基准小的元素置于基准左侧，比基准大的元素置于右侧，基准元素放在中间
    - 必须把基准元素放在中间，保证每次调用必然会减少问题规模。
    - 否则的话，`5, 3, 2, 4`选择第一个元素作为pivot会无法减小问题规模。
    - 措施是，一开始把基准元素换到最左边或者最右边，然后对剩下区域进行分区，最后把基准元素交换到中间。
- **递归调用** - 递归地调用此切分过程。
    - 循环退出条件 - `left >= right` 必须包含等于

__特点__

- **Worst Case** - `pivot`选择不lucky，最差是$$O(n^2)$$

__Coding Tricks__

- 初始`pivot`选取后，放在最左边或者最右边，循环完之后需要把`pivot`放在中间。


__Code__

```java
public class Solution {
    public void helper(int[] array, int ixs, int ixe){
        // recursion base case
        if (ixs >= ixe){
            return;
        }

        // first partition array into two parts
        // AAAAXBBBBB  X needs to be in the middle, or the program is wrong.
        int l = ixs + 1, r = ixe, threshold = array[ixs]; // IMPORTANT
        while (l <= r){
            if (array[l] < threshold) {
                l++;
            } else {
                // swap the i-th number with the number in the r pivot
                int temp = array[r];
                array[r] = array[l];
                array[l] = temp;

                r--;
            }

        }
        // swap the first number with the middle number.
        // l in [ixs+1, ixe+1], r in [ixs, ixe];
        // A[l] > threshold, A[r] < threshold.
        // A[ixs] should be less than threshold
        // so, we should swap A[ixs] and A[r].
        int temp = array[ixs];
        array[ixs] = array[r];
        array[r] = temp;

        // then partition the two parts of the array separately;
        helper(array, ixs, r-1); // IMPORTANT!!!  l-1 == r, ixe = l-1 or r
        helper(array, r+1, ixe); // IMPORTANT!!!  l-1 == r, ixs = l or r+1

        return;
    }

    public int[] quickSort(int[] array) {
        helper(array, 0, array.length-1);

        return array;
    }

    public static void main(String[] args) {
        Solution s = new Solution();
        for (int i: s.quickSort(new int[]{1,2,3})) {
            System.out.println(i);
        }
        for (int i: s.quickSort(new int[]{4,2,1,6,3,5})) {
            System.out.println(i);
        }
    }
}
```

-----
## Rainbow Sort

```
AAABBBxxxxxxCCC
   |  |    |   
   i  j    k
```
把序列分区为三个部分：

- $$[0, i-1]$$ are all As.
- $$[i, j-1]$$ are all Bs.
- $$[j, k]$$ are all xes.
- $$[k+1, size-1]$$ are all Cs.

__算法步骤__

- Step 1 - if `Array[j]` is A, `swap(i, j), i++, j++`
- Step 2 - if `Array[j]` is B, `j++`
- Step 3 - if `Array[j]` is C, `swap(j, k), k--`

__特点__

- Time = $$O(n)$$


-----
## Heap Sort

- Step 1 - heapify
- Step 2 - pop the heap for k times

-----
## Compare

- **stable** - remains the relative order of records with equal keys
- **Cache Locality** - 连续访问容易会出现cache hit。
    - 内存分层，各部分访问时间：Memory 100ns, L1 cache 1ns
    - 访问的时候，cache会读取一部分连续的内存。所以跳着访问会受到影响。


Sorting Algorithms | Time (worst case) | Time (average) | Space (worst case) | Space (average)| Stable | Locality
----|----|----|----|----|----|----
quick sort | $$O(n^2)$$ | $$O(nlogn)$$ | $$O(n)$$ | $$O(logn)$$ | unstable | good
merge sort | $$O(nlogn)$$ | $$O(nlogn)$$ | $$O(n)$$ | $$O(n)$$ | stable | unknown
heap sort  | $$O(nlogn)$$ | $$O(nlogn)$$ | $$O(1)$$ | $$O(1)$$ | unstable | bad

- **heap sort**
    - poll出来放在最后。
    - typical runtime overhead 额外运行时间 - 建立堆需要额外的时间
    - poor spatial locality, might swao from first to last (prefer to access data nearby / poor use of cache memory)
    - **hard to parallelize/distribute**
