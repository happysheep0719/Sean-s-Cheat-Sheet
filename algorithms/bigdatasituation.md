<extoc></extoc>

# Big data situations

Source: C18

**Situations**

- 单机单核内存足
- 单机单核内存不足
- 单机多核内存足
- 多机内存足
- 多机内存不足

**Problems often comes with data that can not fit into the memory or comes by stream**

## find median

**P1. Given a stream, keep track of the median of the numbers.**

- Data structure
    - Both halves have roughly the same size
    - max(smaller half) <= min(larger half)
    - median = max(smaller half) if odd
    - median = (max(smaller half) + min(larger half)) / 2 if even

Smaller half | Larger half
---|---
max heap | min heap

- Maintain the data structure
    - insert the `cur` into the smaller half or the larger half
    - make the quantity of the two halves equal by moving the largest of the smaller half to the larger half or the opposite.

**Follow-up. Data cannot be fit into the memory situation**

- Data structure
    - Let's say, set the limit of the memory of the two heaps to be 1G.

Smaller sorted array | Smaller max heap | Larger min heap | Larger sorted array
---|---|---|---
on disk | in memory | in memory | on disk

- Maintain the data structure
    - insert the `cur` into the smaller heap or the larger heap
    - make the quantity of the two halves equal by moving the largest of the smaller half to the larger half or the opposite.
    - reorganize heap and sorted array if one of two situations meet
        - size(heap) is about to exceed 500M
            - merge the max heap and the samller sorted array
            - put the largest 250M elements in the max heap
            - put the remaining data in smaller sorted array
        - max(smaller sorted array) > max(max heap)

**Input is not a stream**


只有2G内存的pc机，在一个存有10G个整数的文件，从中找到中位数，写一个算法。

1. 外排序
思想：排序-归并
把部分排序结果输出到一个临时文件中。

2. 堆排序
step 1. 先求第1G大：建立一个最小值堆，把所有数都装进去，超出内存的舍弃。
step 2. 利用第1G大，求得第2G大：构造一个最小堆，然后把剩下的数一一丢进去。
step 3. 重复以上直到得到中位数。

3. 位运算
根据内存大小，取整数的前几位，排序全量数据。

4. 桶排序
step 1. 第一次扫描：统计每个区间的数量。
step 2. 统计结果，得到中位数所在区间
step 3. 第二次扫描：拿到区间的所有数字，然后取中位数。

## find certain percentile

**find 95th percentile of all urls' length**

- Solution 0 - sort O(nlogn)
- Solution 1 - max heap(95%) + min heap(5%)
    - for each step O(logn)
    - total time O(nlogn)
- Solution 2 - bucket sort
    - insight: max length of URLs <= 4096
    - calculate the histogram and its CDF

## sort