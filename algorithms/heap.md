<extoc></extoc>

# Heap

1. Also called **Priority Queue**
2. It is a **Complete tree** and can be implemented using an array.
    - _index of left child = index of parent * 2 + 1_
    - _index of right child = index of parent * 2 + 2_
3. 任意节点小于它的所有后裔，最小元素在堆的根上（堆序性）。
4. 根最小的堆叫最小堆，根最大的堆叫最大堆。

__Operations__

- `insert` - $$O(logn)$$ - `percolateUp`
- `update` - $$O(logn)$$
- `get` / `top` - $$O(1)$$
- `pop` - $$O(logn)$$ - `percolateDown`
- `heapify` - make an unsorted array into a heap. $$O(n)$$
    - heap sort

## Problems

__Q1. Find smallest k elements from an unsorted array of size n__

- **Solution 0** - sort $$O(nlogn)$$
- **Solution 1** - heap sort using a **min heap of size n** $$O(k log n + n)$$    
    - Step 1 - heapify $$O(n)$$
    - Step 2 - call `pop()` k times to get the k smallest elements $$O(k log n)$$
- **Solution 2** - use a **max heap of size k** as smallest k candidates $$O(k + (n-k) log k)$$
    - Step 1 - heapify the first k elements to form a max-heap of size=k $$O(k)$$
    - Step 2 - iterate over the rest n-k elements one by one to get the real k smallest elements. $$O((n-k)log k)$$
- Compare **Solution 1** vs. **Solution 2**

Compare | min heap of size n | max heap of size k
----|----|----
Time|O(n + klogn)|O(k + (n-k) log k)
k<<n|O(n)|O(n log k)
k~~n|O(n log n)|O(n log n)
- **Solution 3** - quick select
    - average time = $$O(n)$$
    - worst time = $$O(n^2)$$

    