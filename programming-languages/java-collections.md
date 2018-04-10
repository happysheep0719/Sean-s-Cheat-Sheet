<extoc></extoc>

# Java Collections

[Collections Framework Overview](https://docs.oracle.com/javase/8/docs/technotes/guides/collections/overview.html)

[Java 集合系列01之 总体框架](http://www.cnblogs.com/skywang12345/p/3308498.html)



### Interface List

- Random Access:
    - `set(int index, E e)`
    - `get(int index)`
    - `add(int index, E e), add(E e)`
    - `remove(int index)`

- Search
- Iterator
- Range-View
- `isEmpty()`
- `size()`

### Class ArrayList

- **inital capacity 10** and expand by **1.5 times** when there is no unused cells available 
- **size** = `ArrayList.size()`
- **capacity** = `ArrayList.length` 当前内存容量
- 在删除很多元素后，容量减少到一定程度之后，ArrayList不会主动trimToSize，一般需要人工调用该方法。


### Interface Queue & Deque

- Java里面实现Stack最好的接口是Deque，用LinkedList实现，不能用List，更不能直接用LinkedList。

- Queue - FIFO (exception PriorityQueue)
    - `offer()` - offer at the **tail**
    - `poll()` - poll at the **head**
    - `peek()` - look at the **head** without polling it out

- Deque - FIFO & LIFO (both queue and stack)
    - `offer()` = `offerLast()`
    - `push()` = `offerFirst()`
    - `poll()` = `pop()` =  `pollFirst()` and `pollLast()`
    - `peek()` = `peekFirst()` and `peekLast()`

__Operations of Queue and Stack__

|    Operations    |    Queue      |    Stack    |
|       ----       |     ----      |     ----    |
| Insert  |   `offer`/`add`|`push`/`add` |
| Remove | `poll`/`remove` | `pop`/`remove`  |
| Examine| `peek`/`element`| `peek`/`element`|
*Note:* throw exception / return null

### Class LinkedList & ArrayDeque

- Most popular implementation class: `LinkedList`, `ArrayDeque`.
- `ArrayDeque` is a newer implementation by **circular array** for `Deque`. No null values in Deque.
- For a queue or stack, we can just use `LinkedList`, as it implements both `Queue` and `Deque` interfaces.
- Java的LinkedList是Doubly Linked List，存有Head/Tail


__Circular Array__

- use varible `head` to record the index of the node before the head.
- use varible `tail` to record the index of the node after the tail.
- can store `n-1` elements with n-length array.

### ArrayList vs. LinkedList

How do we choose ArrayList or LinkedList?
1. if there are **very many random access**, use ArrayList.
2. **always add/remove at the end**, use ArrayList.
3. If time complexity is similar for both, use ArrayList. Because LinkedList is memory-cost.
4. **Queue/Stack** -> LinkedList
5. Stack & Vector现在不用了，这两个是线程安全的，但是额外消耗了很多开销。
    Stack->use LinkedList(ArrayDeque)
    Vector->use ArrayList