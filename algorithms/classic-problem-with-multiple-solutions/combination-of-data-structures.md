<extoc></extoc>

# Combination of Data Structures

## LRU Cache

加强6 Q3.1

use cases:

- add()
- get()
    - HashMap
- deleteOldest()
- adjustToNewest()

- for deleteOldest() and adjustToNewest()
    - Array
        - time O(n)
    - X Deque (Deque cannot delete in the middle)
    - LinkedList
        - time O(1)
        - (easy to implement if using Doubly Linked List)
    - X Min Heap

## keep track of first non-repeating character in a stream

加强6 Q3.2

use cases:
    - non-repeating
        - use HashMap
    - record the order of characters
        - use Array
        - use LinkedList
        - X use Deque (Deque cannot delete in the middle)


A good solution:

- use a HashMap and a doubly linked list
    - if key is not in the hashmap
        - it never appears in the previous input;
    - if key is in the hashmap and the value is null
        - it appears more than once
    - if key is in the hashmap and the value is linked to the node in the linked list
        - it appears once










