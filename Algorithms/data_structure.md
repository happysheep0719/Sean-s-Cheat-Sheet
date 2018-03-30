<!-- toc -->

# Data Storage

## Array


## LinkedList
_Reference: Laioffer Class 4_

__Tips__

    1. Never lose the control of the head pointer of the LinkedList.
    2. When dereferencing a ListNode, ensure that pointer is not NULL.
    3. When changing the links of the nodes, be very careful and do not lose the pointees.


__Tricks__

__1. Dummy head__

    - _Situation 1._ When the head of the returning linkedlist could be changed, we should use dummy head.

__2. Fast and Slow pointers__

    - _Situation 1._ to find the middle node of the linkedlist

    - _Situation 2._ to find if there exists a circle in the linkedlist

Q. Why do we use fast and slow pointers instead of treverse two times?

A. Online algorithm vs. Offline algorithm: We can stop in the middle of the program and record the two nodes without losing information.


__Basic Problems__

__P1. reverse a linked list__
改变link方向时，需要使用next或者prev去记录因为改变link可能丢失的节点。

__P2. find middle node of a linked list__
快慢指针
尽量去找middle左边的节点，方便后续调用。

__P3. determine if there exists a circle in a linkedlist__
快慢指针

__P3 Follow-up. 寻找环的开始__
快慢指针相遇后，在head节点新放一只慢速指针，最终会和slow相遇。

__P4. insert a node in a sorted linked list__
corner case - node插入在head之前，tail之后。
使用dummy head，因为node可能需要插在head之前。

__P5. merge two linked list__
使用dummy head


__Composed Problems__

__P5 Follow-up. change N1->N2->...->Nn->null into N1->Nn->N2->Nn-1->...__
Step 1 - find the middle node
Step 2 - reverse the second hal
Step 3 - merge two halves into one solution

__P6. Partition List__
把节点小于target放在左边，大于等于的放在右边。
Step 1 - 使用两个dummy head
Step 2 - 分配节点
Step 3 - 合并两个linkedlist
易错点 - 合并需要两个步骤，循环+剩余节点链接。

__P7. Merge Sort__
Step 1 - Find the middle
Step 2 - Split the list into two halves
Step 3 - Recurse: sort each half
Step 4 - Merge two halves

__P8. Add Two Numbers__
Step 1 - Reverse two linkedlists
Step 2 - Add the number and create one new Linkedlist
Step 3 - Reverse the new linkedlist

__P9. Check if a linked list is palindrome__
Step 1 - findMiddle
Step 2 - Reverse
Step 3 - Compare


# Logic Data Structure

## Queue & Stack
_Reference: Laioffer Class 3_

**Definition**
**Queue** - FIFO (First in first out)
**Stack** - FILO (First in last out)

|    Operations    |    Queue      |    Stack    |
|       ----       |     ----      |     ----    |
| Add one element  |   offer / add   |    push / add |
| Remove one element | poll / remove | pop / remove  |
|See the first element| peek / element| peek / element|


__Difference of two interfaces in Java__

**Queue** - offer, poll and peek cannot cause exception, while add, remove and element can.
In Java, Queue is an interface and realized by LinkedList.

**Stack** - peek and pop can both cause exception.
In Java, Stack is realized.

**Code**
```java
Queue.offer(element);  // add one element. return false when full.
Queue.add(element);    // add one element. throw an exception when full.

Queue.poll();   // remove the first element. return null when empty.
Queue.remove(); // remove the first element. throw an exception when empty.

Queue.peek();      // see the first element. return null when empty.
Queue.element();   // see the first element. throw an exception when empty.
```


## Deque
左右都可以进出的队列

## Binary Tree

### 什么是平衡二叉树
【平衡二叉树 Self-balancing binary search tree AVL tree】左右子树高度差不为1的二叉树。
【二叉搜索树 Binary Search Tree】左子树上的所有节点都小于根节点。右子树上的所有节点均大于根节点。所有节点的值都不相同。


## Heap


# Hashmap 实现
存储方式：array+linkedlist（用来避免碰撞）
存储分配：hashcode函数。Java1.8的hashmap的hashcode：(h = k.hashCode()) ^ (h >>> 16)
扩容问题：容量、负载因子。用capacity*load factor作为新容量。然后rehash
工作方式：通过hash方法，通过put和get存储和获取对象。通过K/V对决定存储的位置。
The time complexity of a get() call in a hash map is in O(1). X（Usually O(1), worst case: walking through all the entries in the same bucket O(n)）
