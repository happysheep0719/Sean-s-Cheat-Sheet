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

### k-way merge

- S1. iterative reduction
    - Time O(kn * logk)
    - Space O(kn)
    - Best when only using memory
- S2. binary reduction
    - Time O(kn * logk)
    - Space O(kn)
- S3. heap k-way altogether
    - Time O(kn * logk)
    - Space O(k)
    - Best when data is to big to fit in memory
    - Least writing times

-----
## Quick Sort
快排是一种采用分治思想的排序算法，大致分为三个步骤。

- **定基准** - 首先随机选择一个元素最为基准
- **划分区** — 所有比基准小的元素置于基准左侧，**比基准大或者等于基准**的元素置于右侧，基准元素放在中间
    - **必须把基准元素放在中间，保证每次调用必然会减少问题规模**。
    - 否则的话，`5, 3, 2, 4`选择第一个元素作为pivot会无法减小问题规模。
    - 措施是，一开始把基准元素换到最左边或者最右边，然后对剩下区域进行分区，最后把基准元素交换到中间。
- **递归调用** - 递归地调用此切分过程。
    - **循环退出条件 - `left >= right` 必须包含等于**

__特点__

- **Worst Case** - `pivot`选择不lucky，最差是$$O(n^2)$$

__Code__

```java
package Array;

import java.util.Arrays;

public class Sorting {
    public int partition(int[] array, int ixs, int ixe){
        int pivotIndex = ixs;
        int pivot = array[pivotIndex];
        swap(array, ixe, pivotIndex);
        // XXXXXXP -> AAABBBP -> AAAPBBB
        // A: < Pivot B: >= Pivot
        int l = ixs, r = ixe - 1;
        while (l <= r){
            if (array[l] < pivot) {
                l++;
            } else {
                swap(array, l, r--);
            }
        }
        swap(array, ixe, r + 1);
        // IMPORTANT!!!  l-1 == r, ixe = l-1 or r
        // IMPORTANT!!!  l-1 == r, ixs = l or r+1
        return r + 1;
    }

    public void helper(int[] array, int ixs, int ixe){
        // recursion base case
        if (ixs >= ixe){
            return;
        }

        int pivotIndex = partition(array, ixs, ixe);
        helper(array, ixs, pivotIndex - 1);
        helper(array, pivotIndex + 1, ixe);

        return;
    }

    public int[] quickSort(int[] array) {
        if (array == null){
            return array;
        }
        helper(array, 0, array.length-1);
        return array;
    }

    public void swap(int[] array, int i, int j){
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }

    public static void main(String[] args) {
        Sorting s = new Sorting();
        int[] array = new int[]{1, 3, 5, 7, 2, 4, 6, 8};
        System.out.println(Arrays.toString(array));
        s.quickSort(array);
        System.out.println(Arrays.toString(array));

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
