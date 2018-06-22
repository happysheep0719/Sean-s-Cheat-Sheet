<extoc></extoc>

# Java Collections

[Collections Framework Overview](https://docs.oracle.com/javase/8/docs/technotes/guides/collections/overview.html)

[Java 集合系列01之 总体框架](http://www.cnblogs.com/skywang12345/p/3308498.html)

## Overview

__Interface__

- `List`
    - `ArrayList`
    - _`Stack`_ (Not Recommended)
    - `LinkedList`
- `Queue`
    - `LinkedList`
    - `ArrayDeque`
    - `PriorityQueue`
- `Deque` (inherited from `Queue`)
    - `LinkedList`
    - `ArrayDeque`

__List vs. Queue__

- List有index概念，支持随机访问
- Queue没有index概念
- java的Stack被淘汰了，因为性能不够好。

## Interface - List

__API__

- `size()`
- `isEmpty()`
- **Random Access**
    - `set(int index, E e)`
    - `E get(int index)`
    - `add(int index, E e)`
    - `add(E e)`
    - `remove(int index)`
    - `remove(E e)`
- Search
- Iterator
- Range-View

## Class - ArrayList

- **inital capacity 10** and expand by **1.5 times** when there is no unused cells available 
- **size** = `ArrayList.size()`
- **capacity** = `ArrayList.length` 当前内存容量
- 在删除很多元素后，容量减少到一定程度之后，ArrayList不会主动trimToSize，一般需要人工调用该方法。

### Create an ArrayList from an Array

[Initialization of an arraylist in one line](https://stackoverflow.com/questions/1005073/initialization-of-an-arraylist-in-one-line)

[create arraylist from array](https://stackoverflow.com/questions/157944/create-arraylist-from-array/13421319#13421319?newreg=32b203911ced49a097bb491d40217190)

[how to convert int[] into list<integer> in java](https://stackoverflow.com/questions/1073919/how-to-convert-int-into-listinteger-in-java)

## Interface - Queue & Deque

[Java Doc Deque](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html)

- Queue is a FIFO queue. (exception PriorityQueue)
- Deque is short for double-ended queue.  Deque is FIFO & LIFO. (both queue and stack)
- Java里面实现Stack最好的接口是Deque，用LinkedList实现，不能用List，更不能直接用LinkedList。

__API__

- Queue
    - `offer(E e)` - offer at the **tail**
    - `E poll()` - poll at the **head**
    - `E peek()` - look at the **head** without polling it out

- Deque
    - `offerFirst(E e)`
    - `offerLast(E e)` = `offer(E e)`
    - `addFirst(E e)` = `push(E e)`
    - `E pollFirst()` = `E poll()`
    - `E pollLast()`
    - `E removeFirst()` = `E pop()`
    - `E peekFirst()` = `E peek()`
    - `E peekLast()`

```
Locations-------First-----------------Last
Operations-----add/push---------------offer
--------------remove/pop------------------
----------------poll----------------------
```

__Operations of Queue and Stack__

|    Operations    |    Queue      |    Stack    |
|       ----       |     ----      |     ----    |
| Insert  |   `offer`/`add`|`push`/`add` |
| Remove | `poll`/`remove` | `pop`/`remove`  |
| Examine| `peek`/`element`| `peek`/`element`|

_Note:_

- `add`, `remove` and `get` throw exception if error happens
- `offer`, `poll` and `peek` return special value if error happens

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
- **heapify** - use one `Collection` as initial argument
- **Order** of the elements
    - It is defaulted by returning -1 if x1 < x2;
    - be CAREFUL not to return an overflowed value.
    - `Comparator.compare(E o1, E o2)` provided when newing a PriorityQueue
        - needs not to change the original class
    - `Comparable.compareTo(E another)` interface in class
    - use `Collections.reverseOrder()`
    - use `Collections.reverseOrder(new myComparator)`
- **Possible ways to provide a comparator class**
    - top-level class (recommended) 
    - Static nested class
    - Anonymous class (not recommended)
    - Lambda expressions (since Java 8)

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
    PriorityQueue<Cell> minHeap = new PriorityQueue<Cell>(11, Collections.reverseOrder());
    // self-defined comparator class
    PriorityQueue<Cell> minHeap = new PriorityQueue<Cell>(11, new MyComparator()); 
    // anonymous comparator class
    PriorityQueue<Cell> minHeap = new PriorityQueue<Cell>(11, new Comparator<Cell>(){
        public int compare(Integer one, Integer two){
            return 0;
        }
    });
    // lambda
    PriorityQueue<Cell> minHeap = new PriorityQueue<Cell>(11, (lhs, rhs) ->{
        return 0;
     }
    );
    ```

__Heap Implementation__

- `percolateUp(int index)`
    - when need to move up one element
    - eg. offering a new element into the heap.
- `offer()` - use `percolateUp`
- `percolateDown(int index)`
    - when need to poll the root element from the heap.
- `poll()` - use `percolateDown`
- `heapify()`
    - convert an array into a heap in $$O(n)$$ time.
    - perform `percolateDown` action in the order of from the nodes on the deepest level to the root. Only needs to do for the first half of the array. range: $$[0, n/2-1]$$
        - No need to know how to prove
    - if we perform `offer()` and `percolateUp`, the time complexity becomes $$O(nlogn)$$
- `update()`
    - find the element in $$O(n)$$
    - use either `percolateUp` or `percolateDown`
