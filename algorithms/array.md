<extoc></extoc>

# Array

__Five types of problems__

- **Sorting** Problems
    - See **Sorting Algorithms**.
- **Binary Search** in Sorted Array & Binary Search Tree
    - See **Binary Search**.
- Selectively Copying Problems
    - See **Two Pointers**
- Partition Problems
    - See **Two Pointers**.
- String Problems
    - String Problems can be seen as char array problems.
    - See **String**

## Array vs. Linked List Comparison

- Memory Layout
    - Array: consecutive allocated, no **overhead**
    - Linked List: non-consecutive, **overhead** of multiple objects with the `next` reference
- Random access time
    - Array: $$O(1)$$
    - Linked List: worst case $$O(n)$$
- Search time in unsorted list
    - Array, Linked List: $$O(n)$$
- Search time in sorted list
    - Array: $$O(logn)$$
    - Linked List: $$O(n)$$