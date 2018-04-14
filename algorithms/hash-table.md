<extoc></extoc>

# Hash Table

- (key, value) pairs
- **NO duplicate keys**
- Hash Table is a general data structure
    - `HashMap` and `HashSet` are its implementationclasses in Java.
- hash collision
    - chaining
    - open address (probe + rehash)

__Open Addressing__

- Linear probing - low cache miss when load factor is low.
- Quadratic probing
- Double hashing

## Problems

__P1. Top k frequent words__

- Step 1 - iterate over the composition for each word and count the words' frequencies using a hashtable.
- Step 2 - maintain a min heap of size k and get top k frequent candidates

__P2. find the one missing number in an unsorted array__

__P3. find the common numbers between two sorted arrays a[N] b[M]__


## Hash Set

Eg. __P. Kth Smallest Sum From Two Sorted Array__
can be used to store visited nodes.
time complexity $$O(n)$$ -> $$O(k)$$



