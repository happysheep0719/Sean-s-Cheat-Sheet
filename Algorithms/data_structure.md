<extoc></extoc>

# Data Storage

## Array


## LinkedList
_Reference: Laioffer Class 4_

### Notes 注意事项

1. Never lose the control of the head pointer of the LinkedList.
2. When dereferencing a ListNode, ensure that pointer is not NULL.
3. When changing the links of the nodes, be very careful and do not lose the pointees.


### Tricks 解题技巧

__1. Dummy head__

- _Situation 1._ When the head of the returning linkedlist could be changed, we should use dummy head.

__2. Fast and Slow pointers__

- _Situation 1._ to find the middle node of the linkedlist

- _Situation 2._ to find if there exists a circle in the linkedlist

Q. Why do we use fast and slow pointers instead of treverse two times?

A. Online algorithm vs. Offline algorithm: We can stop in the middle of the program and record the two nodes without losing information.


### Basic Problems

#### Treverse

__P1. reverse a linked list__

- 改变link方向时，需要使用next或者prev去记录因为改变link可能丢失的节点。

__P2. find middle node of a linked list__

- 快慢指针
- 尽量去找middle左边的节点，方便后续调用。

__P3. determine if there exists a circle in a linkedlist__

- 快慢指针

__P3 Follow-up. 寻找环的开始__

- 快慢指针相遇后，在head节点新放一只慢速指针，最终会和slow相遇。

__P4. insert a node in a sorted linked list__

- corner case - node插入在head之前，tail之后。
- 使用dummy head，因为node可能需要插在head之前。

__P5. merge two linked list__

- 使用dummy head


### Composed Problems

__P5 Follow-up. change N1->N2->...->Nn->null into N1->Nn->N2->Nn-1->...__

- Step 1 - find the middle node
- Step 2 - reverse the second hal
- Step 3 - merge two halves into one solution

__P6. Partition List__

- 把节点小于target放在左边，大于等于的放在右边。
- Step 1 - 使用两个dummy head
- Step 2 - 分配节点
- Step 3 - 合并两个linkedlist
- 易错点 - 合并需要两个步骤，循环+剩余节点链接。

__P7. Merge Sort__

- Step 1 - Find the middle
- Step 2 - Split the list into two halves
- Step 3 - Recurse: sort each half
- Step 4 - Merge two halves

__P8. Add Two Numbers__

- Step 1 - Reverse two linkedlists
- Step 2 - Add the number and create one new Linkedlist
- Step 3 - Reverse the new linkedlist

__P9. Check if a linked list is palindrome__

- Step 1 - findMiddle
- Step 2 - Reverse
- Step 3 - Compare


# Logic Data Structure

## Queue & Stack
_Reference: Laioffer Class 3_

### Definition

**Queue**
- FIFO (First in first out)

**Stack**
- FILO (First in last out)

**Deque**
- 左右都可以进出的队列

### Operations
|    Operations    |    Queue      |    Stack    |
|       ----       |     ----      |     ----    |
| Add one element  |   offer / add   |    push / add |
| Remove one element | poll / remove | pop / remove  |
|See the first element| peek / element| peek / element|


**Difference of two interfaces in Java**

**For Queue** - offer, poll and peek cannot cause exception, while add, remove and element can.
In Java, Queue is an interface and realized by LinkedList.

**For Stack** - peek and pop can both cause exception.
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


## Binary Tree
_Reference: Laioffer Class 5_

### Definition

**Binary Tree**
- _Structure_ - For each node, there are at most two children nodes.

**Balanced Binary Tree**
- _Structure_ - For every node, the depth of the left and right subtrees differ by 1 or less. 对于每个节点，左右子树高度差都小于等于 1。
- Height = O(log2(N))

**Complete Binary Tree**
- _Structure_ - 除了最后一层的节点可以为null，其他都不为null。并且最后一层的节点都挤在左边。

**Perfect Binary Tree**
- _Structure_ - 所有节点都不为null节点。

**Binary Search Tree**
- _Structure_ - 没有要求。
- _Value_ - 任何节点，左子节点一定是小于父节点。柚子节点一定大于父节点。不可以等于父节点的值。
- 中序遍历In-order的遍历结果是从小到大排序的序列。

### Basic Problems

Problem can be seen as different types of basic tree problems.

#### Recursion & Tree

**两种信息传递方式**
1. 把信息**从上往下**传 - 用**函数参数parameters**传递
2. 把信息**从下往上**传 - 用**返回值return type**传递 


**两种算法写法** - _有的问题可以用两种思路写，但是一般会有一种思路写法更简单，实际中选择好写的写法。_

**1. 在从上往下的过程中，就可以提前终止程序**

取决于是否存在这样的可能，在还没有遍历到底部，就可以终止的情况。如果存在这种可能，说明判断的信息

- **determine if it is BST**

    @ parameter: the should-be range of root
    下层节点为BST = 上层节点为BST
    可能提前终止
    
- **isSymmetric/isIdentical(Node root1, Node root2)**

    @ return: boolean isSymmetric
    对称 = 该层key相同 && 该层结构相同
    上层对称 = 该层对称 + 下层对称
    base case 最下层对称
    可能提前终止

**2. 只有在从下往上的过程里，才能结束程序** - 需要遍历到最底层、需要遍历所有节点的情况

- **getHeight(Node root) **

    @ return: int Height
    上层的层数 = Max(左子树的层数, 右子树的层数) + 1
    base case 最下层高度为1
    上层对高度的计算依赖对下层的遍历
        
- **isBalanced(Node root)**

    @ return: boolean isbalanced
    上层节点是否平衡 = 下层节点平衡 && 左右子树高度差小于等于1
    base case 最下层平衡 && 最下层高度为1
    上层对高度的计算和平衡的判断依赖对下层的遍历

    
- **Assign the value of each note to be the total number of nodes that belong its left subtree. 左子树数字之和**


#### Treverse & Tree

__P1. Pre-order treverse__

__P2. In-order treverse__

__P3. Post-order treverse__


## Heap

# Hashmap 实现
存储方式：array+linkedlist（用来避免碰撞）
存储分配：hashcode函数。Java1.8的hashmap的hashcode：(h = k.hashCode()) ^ (h >>> 16)
扩容问题：容量、负载因子。用capacity*load factor作为新容量。然后rehash
工作方式：通过hash方法，通过put和get存储和获取对象。通过K/V对决定存储的位置。
The time complexity of a get() call in a hash map is in O(1). X（Usually O(1), worst case: walking through all the entries in the same bucket O(n)）
