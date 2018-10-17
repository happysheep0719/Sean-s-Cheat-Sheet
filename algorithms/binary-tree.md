<extoc></extoc>

# Binary Tree

_Reference: Laioffer Class 5, Practice Class 7, 8_

__Definition__

- **Binary Tree**
    - _Structure_ - For each node, there are at most two children nodes.

- **Balanced Binary Tree**
    - _Structure_ - **For every node**, the depth of the left and right subtrees differ by 1 or less. 对于每个节点，左右子树高度差都小于等于 1。
    - Height = O(log2(N))

- **Complete Binary Tree**
    - _Structure_ - 除了最后一层的节点可以为null，其他都不为null。并且最后一层的节点都挤在左边。

- **Full / Perfect Binary Tree**
    - _Structure_ 

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

- **What do you expect from lchild, rchild?**
- What do you want to tell to your lchild, rchild?
- How do you want to divide the problems into subproblems?
- **What do you want to do in the current layer?**
- **What do you want to report to your parent?**

__几种类型__

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
    //      1.1: root.left == one or two || root.right == one or two (may not be answer if answer is not gurantee)
    //            =>  return root
    //      1.2: root.left != one either two && root.right != one either two (may not be answer if answer is not gurantee)
    //            =>  return root
    // ----> root is one or two  =>  return root
    // case 2: root is not one or two
    //      2.1: one of root.left and root.right found one or two
    //            =>  return lres || rres
    //      2.2: both of root.left and root.right found one or two
    //            =>  return root
    //      2.3: return null

- __Follup-up. LCA (with parent node)__

    - Solution 1 - go to the parent recursively and get the number of level
    - Solution 2 - go to the parent from one of the node, and record the path of going up.

- __Follow-up. LCA (one or two is not guranteed in the tree)__

    - check if children return two if root == one 
    - check if children return one if root == two

- __P7. Maximum Leaf-to-Leaf Path__

    - What do we expect from left child / right child? / What do we want to report to the parent node?
        - max single path in the left / right subtree
    - What do we want to do in the current layer?
        - update global_max
    
- __Follow-up. max Node-to-Node path sum__

- **Insert in BST**
    - *Problem* : return the new root after the change.
    - corner case: if the root is null, return the new node.

- **Delete in BST**
    - *Problem* : return the new root of the BST.
    - **Step 1**: find the node to be deleted
        - By transforming the problem into ONE sub problem that delete the key in one of the sub tree.
    - **Step 2**: delete the node
        - **case 1** - the node has no children.
        - **case 2** - the node has no left child.
        - **case 3** - the node has no right child.
        - **case 4** - the node has both left and right children.
            - The problem is transformed into three parts
            - **part 1**: find the largest node in the left subtree or the smallest node in the right subtree and record the replacement
            - **part 2**: delete the replacement in the tree - can be realized using recursive call. It must only hit one of case 1, case 2 and case 3.
            - **part 3**: set the children of the replacement



3. 人字形

- __P1. Maximum Path Sum Binary Tree II__

    - update maximum的逻辑和recursion传递逻辑有区别
        - update maximum在每个节点，不仅要考虑人字形，也要考虑单臂型
        - recursion传递逻辑只考虑传递其中一条单臂信息
        
4. Path Problem in Binary Tree

- 问法可以和一维数组问题结合，比如Maximum Subarray sum，比如2 Sum

-----
## Binary Search Tree Problems

- 为什么BST里面没有重复数据？
    - 工业界中，BST是用来查找的。

__Time Complexity in BST__

- `search` - worst case $$O(n)$$, average $$O(logn)$$
- `insert` - worst case $$O(n)$$, average $$O(logn)$$
- `remove` - worst case $$O(n)$$, average $$O(logn)$$

- Worst case happen if the binary tree is structured like a linked list.
- In **Balanced Binary Search Tree**, `search`, `insert` and `remove` operations are guaranteed to be $$O(logn)$$. For example, **AVL Tree**, **Red-Black Tree** are balanced BST.

__优化__

- 怎么样让BST效率更高？ - 更加Balanced
- **balanced binary search tree**
    - Eg. AVL tree, Red-black tree, etc 但是面试不会考定义，可能会借这个定义考基本能力。
    - Red-Black tree Implementations
        - in Java: TreeMap/TreeSet
        - in C++: map/set


-----
## Treverse & Tree (Serialization) Problems

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
   
----- 
## Deserialization Problems

每一层需要得到左右子树各自的输入（比如是in-order和post-order），左右子树分别返回构造好的tree的root。

### P1. Reconstruct a BST with post-order traverse

### P2. Reconstruct a tree with level-order and in-order traverses

### P3. Reconstruct a tree with pre-order and in-order traverses
