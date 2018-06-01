<extoc></extoc>

# Binary Tree

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

__General ways of solving problems about binary tree:__

- __Divide and conquer__ is the nature of binary tree. The problems can usually be divided into three parts:
    - solve sub problems for left/right subtree
    - solve sub problem for root
- __Iteration__
    - could be complicated for binary tree but we need to know how.

-----
## Recursion & Tree Problems

__两种信息传递方式__

- 把信息**从上往下**传 - 用**函数参数 parameters**传递
- 把信息**从下往上**传 - 用**返回值 return type**传递

__算法的几个要点__

- What do you expect from lchild, rchild?
- What do you want to do in the current layer?
- What do you want to report to your parent?

__两种算法写法__ - _有的问题可以用两种思路写，但是一般会有一种思路写法更简单，实际中选择好写的写法。_

1. 在从上往下的过程中，就可以提前终止程序

取决于是否存在这样的可能，在还没有遍历到底部，就可以终止的情况。如果存在这种可能，说明判断的信息
    
- __P1. determine if it is BST__
    - @ parameter: the should-be range of root
    - 下层节点为BST = 上层节点为BST
    - 可能提前终止
    
- __P2. isSymmetric/isIdentical (Node root1, Node root2)__
    - @ return: boolean isSymmetric
    - 对称 = 该层key相同 && 该层结构相同
    - 上层对称 = 该层对称 + 下层对称
    - base case 最下层对称
    - 可能提前终止

2. 只有在从下往上的过程里，才能结束程序 - 需要遍历到最底层、需要遍历所有节点的情况

- __P3. getHeight (Node root)__
    - @ return: int Height
    - 上层的层数 = Max(左子树的层数, 右子树的层数) + 1
    - base case 最下层高度为1
    - 上层对高度的计算依赖对下层的遍历
    
- __P4. isBalanced (Node root)__
    - @ return: boolean isbalanced
    - 上层节点是否平衡 = 下层节点平衡 && 左右子树高度差小于等于1
    - base case 最下层平衡 && 最下层高度为1
    - 上层对高度的计算和平衡的判断依赖对下层的遍历

- __P5. Assign the value of each note to be the total number of nodes that belong its left subtree. 求左子树数字之和__

- __P6. Lowest Common Ancestor 共同子祖先__

    // case 1: root is one or two
    //      1.1: root.left == one or two || root.right == one or two
    //            =>  return root
    //      1.2: root.left != one either two && root.right != one either two
    //            =>  return root
    // ----> root is one or two  =>  return root
    // case 2: root is not one or two
    //      2.1: one of root.left and root.right found one or two
    //            =>  return lres || rres
    //      2.2: both of root.left and root.right found one or two
    //            =>  return root
    //      2.3: return null

- __P7. Tree Node Path__

-----
## Treverse & Tree Problems

__Coding 注意点__

- Iteration写法中，如果需要回到目标节点的上一层，需要加入prev节点。
- 使用prev时，记得先更新prev，再更新curr

__Problems__

- __P1. Pre-order treverse__
    - *Order* : root -> root.left -> root.right
    - Remember to add the right child first, so the left child is popped first.

- __P2. In-order treverse__
    - *Order* : root.left -> root -> root.right
    - 使用Stack记录访问顺序 - 但是并不是遍历顺序
    - 画图，然后观察prev和curr的关系，从而分类讨论处理节点

- __P3. Post-order treverse__
    - *Order* : root.left -> root.right -> root
    - 使用Stack记录访问顺序 - 但是并不是遍历顺序
    - 画图，然后观察prev和curr的关系，从而分类讨论处理节点

- __P4. Level treverse__
    - *Order* : low level -> high level
    - BFS
