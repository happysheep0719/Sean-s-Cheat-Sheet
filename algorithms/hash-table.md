<extoc></extoc>

# Hash Table

## Hashmap 实现
存储方式：array+linkedlist（用来避免碰撞）
存储分配：hashcode函数。Java1.8的hashmap的hashcode：(h = k.hashCode()) ^ (h >>> 16)
扩容问题：容量、负载因子。用capacity*load factor作为新容量。然后rehash
工作方式：通过hash方法，通过put和get存储和获取对象。通过K/V对决定存储的位置。
The time complexity of a get() call in a hash map is in O(1). X（Usually O(1), worst case: walking through all the entries in the same bucket O(n)）

## Hash Set


Eg. __P. Kth Smallest Sum From Two Sorted Array__
can be used to store visited nodes.
time complexity $$O(n)$$ -> $$O(k)$$