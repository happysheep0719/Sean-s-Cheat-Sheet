<extoc></extoc>

# Combination of Data Structures

## LRU Cache

use cases:

- add()
- get()
    - HashMap
- deleteOldest()
- adjustToNewest()

- for deleteOldest() and adjustToNewest()
    - Array
        - time O(n)
    - LinkedList
        - time O(1)
        - (easy to implement if using Doubly Linked List)
    - Min Heap