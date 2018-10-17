<extoc></extoc>

# Sorting Algorithms

## Compare

- **Stablity**
    - remains the **relative order of records with equal keys**
- **Cache Locality**
    - 访问的时候，cache会读取一部分连续的内存，连续访问容易出现cache hit，可以利用Cache读取快的特性。
    - 访问消耗：Memory 100ns, L1 cache 1ns

Sorting Algorithms | Time (worst case) | Time (average) | Space (worst case) | Space (average)| Stable | Locality
----|----|----|----|----|----|----
quick sort | $$O(n^2)$$   | $$O(nlogn)$$ | $$O(n)$$ | $$O(logn)$$ | unstable | good
merge sort | $$O(nlogn)$$ | $$O(nlogn)$$ | $$O(n)$$ | $$O(n)$$    | stable   | unknown
heap sort  | $$O(nlogn)$$ | $$O(nlogn)$$ | $$O(1)$$ | $$O(1)$$    | unstable | bad

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
    - Time O(k^2 * n)
    - Space O(kn)
    - Best when only using memory
- S2. binary reduction
    - Time O(klogk * n)
    - Space O(kn)
- S3. heap k-way altogether
    - Time O(klogk * n)
    - Space O(k)
    - Best when data is to big to fit in memory, Least writing times
    - Online Algortihm (Can input n streams)

-----
## Quick Sort

快排是一种采用分治思想的排序算法，大致分为三个步骤。

- **定基准** - 首先随机选择一个元素最为基准
- **划分区** — `XXXXXXP` -> `AAABBBP` -> `AAAPBBB`
    - 具体做法，一开始把基准元素换到最左边或者最右边，然后对剩下区域进行分区，最后把基准元素交换到中间。
    - **必须把基准元素放在中间**
        - **到递归下一层的子问题时，子问题不处理基准。保证每次调用必然会减少问题规模**。
        - 保证最终答案基准在排好序的位置。
        - `5, 3, 2, 4` 选择第一个元素作为pivot，如果子问题不去除掉基准会无法减小问题规模。
    - 具体做法，一开始把基准元素换到最左边或者最右边，然后对剩下区域进行分区，最后把基准元素交换到中间。
- **递归调用** - `AAAPBBB` -> `AAA` + `BBB`
    - **循环退出条件 `left >= right`**
        - **必须包含等于**

__特点__

- **Worst Case** - `pivot`选择不lucky，最差是$$O(n^2)$$

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
    - poll出来放在最后，Inplace地利用原数组。

__特点__

- typical runtime overhead 额外运行时间 - 建立堆需要额外的时间
- poor spatial locality, might swap from first to last (prefer to access data nearby / poor use of cache memory)
- **hard to parallelize/distribute**
