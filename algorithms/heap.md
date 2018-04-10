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

