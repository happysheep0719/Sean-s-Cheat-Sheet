<extoc></extoc>

# Java Map

[Java Collection Interfaces Overview](https://github.com/CarpenterLee/JCFInternals/blob/master/markdown/1-Overview.md)

## Interface - Map / Set

__API__

- `Map`
    - `V put(K key, V value)`
    - `V get(Object key)`
    - `V remove(K key)`
    - `boolean containsKey(Object key)`
    - get view
        - `Set<Map.Entry<K, V>> entrySet()`
        - `Set<K> keySet()`
        - `Collection<V> values()`
    - `boolean containsValue(V value)` - $$O(n)$$
    - `void clear()`
    - `int size()`
    - `boolean isEmpty()`

- `Set`
    - `boolean add(E e)`
    - `boolean remvoe(Object o)`
    - `boolean contains(Object o)`
    - `void clear()`
    - `int size()`
    - `boolean isEmpty()`

__Implementation Classes__

1. HashSet
    - stores its elements in a hashtable
    - doesn't not gurantee the order of iteration
2. TreeSet
    - stores its elements in a red-black tree(balanced binary search tree)
    - gurantee the order of iteration (inorder traversal)
3. LinkedHashSet
    - It is a HashSet and also a LinkedList.


## Class - HashMap / HashSet

__Implementation__

- `HashMap` and `Hashtable` are like `ArrayList` and `Vector`. 
    - `HashMap` allows one null key.
    - `Vector` and `Hashtable` operations are synchronized.
- `HashSet` is backed up by a `HashMap` instance.
- Data Storage - `array` + `linkedlist`
    - array of entries
    - each entry is actually a single linked list(handle collision)
    - contains the (key, value) pair
- Distribution - hashcode() 
    - Java1.8的hashmap的hashcode：(h = k.hashCode()) ^ (h >>> 16)
- **Capacity Expansion**
    - check load factor if exceeds 0.75 and double the size
    - rehash
- **Access key (get / put)**
    - hash - `int hash = hashCode(key)`
    - index - `int index = hash % table.length()`
    - iterate the bucket
        - check if the key has already existed
        - NO -> add a ney Entry node
        - YES -> update the value of the Entry

__Time Complexity__
    
    Operation | Average | **Worst**
    ----|----|----
    search: containsKey/get | $$O(1)$$ | **$$O(n)$$**
    insert/update: put | $$O(1)$$ | **$$O(n)$$**
    delete: remove| $$O(1)$$ | **$$O(n)$$**


__Check key__

- `==`
    - determine if two primitive type has the same type
    - determine if two reference are pointed to the same object
- `.hashCode()`
- `.equals()`

__Two ways of update__

- `containsKey -> get // two times`
- `Integer sc = hm.get("snap") // one time`

__Contract between equals() and hashCode()__

- true `equals` => same `hashCode`
- reduce collesion as much as you can.

__Override equals(), hashCode()__

```java
public class Element {
    int x;
    int y;
    int sum;
    ...
    @Override
    public boolean equals(Object obj) {
        if (this == obj){
            return ture;
        }
        if (!(obj instanceof Element)) {
            return false;
        }
        Element other = (Element) obj;
        return this.x == other.x && this.y == other.y && this.sum == other.sum;
    }
    
    @Override
    public int hashCode(){
        return this.x * 31 * 31 + this.y * 31 + this.sum;
    }

}
```

__hashCode Design__

```java
return x * 31 + y;
```

```java
return hashNumber & 0x7fffffff;
```

- 需要取绝对值，位运算计算效率最快。
    - 10 % 3 = -1，会影响后续取index
- pair设计hashcode，当交换Pair(A, B)得到Pair(B, A)，应该得到同样的hashcode