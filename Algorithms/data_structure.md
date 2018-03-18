# Queue Vs. Stack
Stack.push()

**Queue**
```
Queue.offer(element);  // add one element. return false when full.
Queue.add(element);    // add one element. throw an exception when full.

Queue.poll();   // remove the first element. return null when empty.
Queue.remove(); // remove the first element. throw an exception when empty.

Queue.peek();      // see the first element. return null when empty.
Queue.element();   // see the first element. throw an exception when empty.
```

**Stack**
```
Stack.
```

# Deque
左右都可以进出的队列

# Hashmap 实现
存储方式：array+linkedlist（用来避免碰撞）
存储分配：hashcode函数。Java1.8的hashmap的hashcode：(h = k.hashCode()) ^ (h >>> 16)
扩容问题：容量、负载因子。用capacity*load factor作为新容量。然后rehash
工作方式：通过hash方法，通过put和get存储和获取对象。通过K/V对决定存储的位置。
The time complexity of a get() call in a hash map is in O(1). X（Usually O(1), worst case: walking through all the entries in the same bucket O(n)）

# 什么是平衡二叉树
【平衡二叉树 Self-balancing binary search tree AVL tree】左右子树高度差不为1的二叉树。
【二叉搜索树 Binary Search Tree】左子树上的所有节点都小于根节点。右子树上的所有节点均大于根节点。所有节点的值都不相同。