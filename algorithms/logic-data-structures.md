<extoc></extoc>

# Logic Data Structure

## Queue & Stack
_Reference: Laioffer Class 3_

- __Queue__ - FIFO (First in first out)

- __Stack__ - FILO (First in last out)

- __Deque__ - 左右都可以进出的队列


## Binary Tree
_Reference: Laioffer Class 5, Practice Class 7, 8_

__Definition__

- **Binary Tree**
- _Structure_ - For each node, there are at most two children nodes.

- **Balanced Binary Tree**
- _Structure_ - For every node, the depth of the left and right subtrees differ by 1 or less. 对于每个节点，左右子树高度差都小于等于 1。
- Height = O(log2(N))

- **Complete Binary Tree**
- _Structure_ - 除了最后一层的节点可以为null，其他都不为null。并且最后一层的节点都挤在左边。

- **Perfect Binary Tree**
- _Structure_ - 所有节点都不为null节点。

- **Binary Search Tree**
- _Structure_ - 没有要求。
- _Value_ - 任何节点，左子节点一定是小于父节点。柚子节点一定大于父节点。不可以等于父节点的值。
- 中序遍历In-order的遍历结果是从小到大排序的序列。

### Basic Problems

#### Recursion & Tree

__两种信息传递方式__

- 把信息**从上往下**传 - 用**函数参数 parameters**传递
- 把信息**从下往上**传 - 用**返回值 return type**传递

__两种算法写法__ - _有的问题可以用两种思路写，但是一般会有一种思路写法更简单，实际中选择好写的写法。_

1. 在从上往下的过程中，就可以提前终止程序

取决于是否存在这样的可能，在还没有遍历到底部，就可以终止的情况。如果存在这种可能，说明判断的信息
- **P1. determine if it is BST**
- @ parameter: the should-be range of root
- 下层节点为BST = 上层节点为BST
- 可能提前终止
- **P2. isSymmetric/isIdentical (Node root1, Node root2)**
- @ return: boolean isSymmetric
- 对称 = 该层key相同 && 该层结构相同
- 上层对称 = 该层对称 + 下层对称
- base case 最下层对称
- 可能提前终止

2. 只有在从下往上的过程里，才能结束程序 - 需要遍历到最底层、需要遍历所有节点的情况

- **P3. getHeight (Node root)**
- @ return: int Height
- 上层的层数 = Max(左子树的层数, 右子树的层数) + 1
- base case 最下层高度为1
- 上层对高度的计算依赖对下层的遍历
- **P4. isBalanced (Node root)**
- @ return: boolean isbalanced
- 上层节点是否平衡 = 下层节点平衡 && 左右子树高度差小于等于1
- base case 最下层平衡 && 最下层高度为1
- 上层对高度的计算和平衡的判断依赖对下层的遍历

- **Assign the value of each note to be the total number of nodes that belong its left subtree. 求左子树数字之和**


#### Treverse & Tree

- __P1. Pre-order treverse__
    - root, root.left, root.right

- __P2. In-order treverse__

- __P3. Post-order treverse__

## Graph

**Graph** can be represented using **Adjacency Matrix** and **Adjacency List**.

Following is an example undirected graph with 5 vertices.

![Graph](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/undirectedgraph.png)

![Adjacency Matrix](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/adjacencymatrix.png)

![Adjecency List](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/listadjacency.png)

## Heap

# Hashmap 实现
存储方式：array+linkedlist（用来避免碰撞）
存储分配：hashcode函数。Java1.8的hashmap的hashcode：(h = k.hashCode()) ^ (h >>> 16)
扩容问题：容量、负载因子。用capacity*load factor作为新容量。然后rehash
工作方式：通过hash方法，通过put和get存储和获取对象。通过K/V对决定存储的位置。
The time complexity of a get() call in a hash map is in O(1). X（Usually O(1), worst case: walking through all the entries in the same bucket O(n)）