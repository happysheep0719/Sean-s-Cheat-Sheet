<extoc></extoc>

# Java Collections

[Collections Framework Overview](https://docs.oracle.com/javase/8/docs/technotes/guides/collections/overview.html)

[Java 集合系列01之 总体框架](http://www.cnblogs.com/skywang12345/p/3308498.html)


## Interface - List

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

## Class - ArrayList

- **inital capacity 10** and expand by **1.5 times** when there is no unused cells available 
- **size** = `ArrayList.size()`
- **capacity** = `ArrayList.length` 当前内存容量
- 在删除很多元素后，容量减少到一定程度之后，ArrayList不会主动trimToSize，一般需要人工调用该方法。


## Interface - Queue & Deque

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

## Class - LinkedList & ArrayDeque

- Most popular implementation class: `LinkedList`, `ArrayDeque`.
- `ArrayDeque` is a newer implementation by **circular array** for `Deque`. No null values in Deque.
- For a queue or stack, we can just use `LinkedList`, as it implements both `Queue` and `Deque` interfaces.
- Java的LinkedList是Doubly Linked List，存有Head/Tail


__Circular Array__

- use varible `head` to record the index of the node before the head.
- use varible `tail` to record the index of the node after the tail.
- can store `n-1` elements with n-length array.

## Class - ArrayList vs. LinkedList

_How do we choose ArrayList or LinkedList?_

1. if there are **very many random access**, use ArrayList.
2. **always add/remove at the end**, use ArrayList.
3. If time complexity is similar for both, use ArrayList. Because LinkedList is memory-cost.
4. **Queue/Stack** -> LinkedList
5. Stack & Vector现在不用了，这两个是线程安全的，但是额外消耗了很多开销。
    Stack->use LinkedList(ArrayDeque)
    Vector->use ArrayList
    
## Class - PriorityQueue

- It implements the queue interface but it is not a FIFO queue. It is actually a min heap.
- It arranges the order of the elements by comparing any pair of elements.
- **Time Complexity** of size n `PriorityQueue`
    - `offer(E e)` - $$O(logn)$$
    - `peek()` - $$O(1)$$
    - `poll()` - $$O(logn)$$
    - `remove()` - $$O(logn)$$ - should not be used
    - `size()` - $$O(1)$$
    - `isEmpty()` - $$O(1)$$
    - `private heapify()` - $$O(n)$$
- **Order** of the elements
    - It is defaulted by returning -1 if x1 < x2;
    - `Comparator.compare(E o1, E o2)` provided when newing a PriorityQueue
    - `Comparable.compareTo(E another)` interface in class

    ```java    
    class Cell implements Comparable<Cell>{
        public int row;
        public int col;
        public int value;
        public Cell(int row, int col, value){
            this.row = row;
            this.cell = cell;
            this.value = value;
        }
        
        @Override
        public int compareTo(Cell another){
            if (this.value == another.value){
                return 0;
            }
            return this.value < another.value ? -1:1;
        }
    }
    
    // will use compareTo() in the class
    PriorityQueue<Cell> minHeap = new PriorityQueue<Cell>(11); 

    //interface Comparator<E>{
    //    int compare(E o1, E o2);
    //}
    
    class MyComparator implements Comparator<Cell>{
        @Override
        public int compare(Cell c1, Cell c2){
            if (c1.value == c2.value){
                return 0;
            }
            // !IMPORTANT needs to return -1 or 1, or it might over MAX_INT.
            return c1.value - c2.value ? -1:1; 
        }
    }
    
    // will use compare() in the provided Comparator
    PriorityQueue<Cell> minHeap = new PriorityQueue<Cell>(11, new MyComparator()); 
    ```