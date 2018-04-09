<extoc></extoc>

# Java

## Coding Style
[Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)

1. Naming - use upperCamelCase for class names and all upper cases for const variable, otherwise lowerCamelCase.

2. Separate reversed words and bracelets. 
reversed words - 保留字

- Eg. ```for ()```
- Eg. ```a && b```

3. Add spaces on both sides of binary or ternary operators.

- Eg. ```a + b```


## Primitive types vs. Class types

__Primitive types:__

- `boolean`/`byte`/`char`/`short`/`int`/`long`/`float`/`double`
- `5`/`5.5` are objects.
- Strings are objects.
- Arrays are objects.

### Array

```java
int[][] array = new int[2][];
array[0] = new int[1];
array[1] = new int[3];
```

取subarray，使用arrays工具箱。


## Static & Final

__1. static__

- class variable vs. instance varible
- class method vs. instance method
- unlike C++, local static varible is not allowed.

__2. final__

- final class: A class that cannot be dereived. 最终类。不能被继承。
- final method: A method that cannot be overridden.
- final field/var: A varible that once assigned, cannot be assigned again.

define a **constant var** in Java:

```
// Cannot change the value
final int value = 10;
```

define a **constant reference** in Java:

```
// Cannot change the reference value
final Boy b1 = new Boy(10);

// Can change the object field varibles
b1.girlFriend = new Girl("Lady gaga");
```

## parameter passing

**Java parameters are always passed by value.**

- **primitive type**: copy of the value itself
- **objects**: copy of the object reference

## Java Interfaces & Classes

- 为什么要用List作为Interface？

    ```java
    List<Integer> myList = new LinkedList<>();
    ```

    把接口和实现分开实现。因为这里我们仅仅需要List的语义，我们要的不是一个特定的List。实现可能会变化。
    
    Eg.
     
    ```java
    List<Integer> myList = creatListFromConfig(conf);
    ```
    
- 父类List有的功能，子类LinkedList一定有。


__Abstract class vs. interfaces__

[Java docs](https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html)

Abstract class | Interface
----|----
using **extends** | **implements**
methods can be declared without implementation | same
cannot instantiate | same
doesn't support multiple inheritance | support
... | ...


```java
interface A {
    public Integer get(int index);
}

interface B {
    public void put(int index, E e);
}

A myDict = new A(); // wrong

class myList implements A, B {
    @override
    public Integer get(int index) {
    }
    @override
    public void put(int index, E e) {
    }    
}
```

## Java Collection

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