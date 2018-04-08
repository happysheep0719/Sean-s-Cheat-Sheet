<extoc></extoc>

# Data Storage
## Array


### Basic Problems

- Sorting Problems
    - See **Sorting Algorithms**.
- Sorted Array & Binary Search
    - See **Binary Search**.
- Partition Problems
    - See **Two Pointers**.
- String Problems
    - String Problems can be seen as char array problems.
    - See **String**

## Linked List
_Reference: Laioffer Class 4 & Practice4_

**Note:**

- Never lose the control of the **head** pointer of the Linked List.
- When dereferencing a ListNode, ensure that pointer is not `NULL`.
- When changing the links of the nodes, be very careful and do not lose the **reference**.


**Coding Tricks**

- __1. Dummy head__

	- _Situation 1._ When the head of the returning linked list could be changed, we should use dummy head.

- __2. Fast and Slow pointers__

	- _Situation 1._ to find the **middle** node of the linked list
	
	- _Situation 2._ to find if there exists a **circle** in the linked list

	- Q: Why do we use fast and slow pointers instead of treverse two times?

		A: Online algorithm vs. Offline algorithm: We can stop in the middle of the program and record the two nodes without losing information.


### Basic Problems

- __P1. Reverse a linked list__
    - Space Complexity: $O(1)$
    - 改变link方向时，需要使用`next`或者`prev`去记录因为改变link可能丢失的节点。

- __P2. Find middle node of a linked list__
    - 快慢指针
    - 尽量去找middle左边的节点，方便后续调用。

- __P3. determine if there exists a circle in a linked list__
    - 快慢指针

- __P3 Follow-up. 寻找环的开始__

    - 快慢指针相遇后，在head节点新放一只慢速指针，最终会和slow相遇。

- __P4. insert a node in a sorted linked list__

    - corner case - node插入在head之前，tail之后。
    - 使用dummy head，因为node可能需要插在head之前。

- __P5. merge two linked list__

    - 使用dummy head


### Composed Problems

- __P5 Follow-up. change N1->N2->...->Nn->null into N1->Nn->N2->Nn-1->...__
    
    - Step 1 - find the middle node
    - Step 2 - reverse the second hal
    - Step 3 - merge two halves into one solution

- __P6. Partition List__

    - 把节点小于target放在左边，大于等于的放在右边。
    - Step 1 - 使用两个dummy head
    - Step 2 - 分配节点
    - Step 3 - 合并两个linked lists
    - 易错点 - 合并需要两个步骤，循环+剩余节点链接。

- __P7. Merge Sort__
    
    - Step 1 - Find the middle
    - Step 2 - Split the list into two halves
    - Step 3 - Recurse: sort each half
    - Step 4 - Merge two halves

- __P8. Add Two Numbers__
    
    - Step 1 - Reverse two linked lists
    - Step 2 - Add the number and create one new linked list
    - Step 3 - Reverse the new linked list

- __P9. Check if a linked list is palindrome__

    - Step 1 - findMiddle
    - Step 2 - Reverse
    - Step 3 - Compare

## Array vs. Linked List Comparison

- Memory Layout
    - Array: consecutive allocated, no **overhead**
    - Linked List: non-consecutive, **overhead** of multiple objects with the `next` reference
- Random access time
    - Array: $O(1)$
    - Linked List: worst case $O(n)$
- Search time in unsorted list
    - Array, Linked List: $O(n)$
- Search time in sorted list
    - Array: $O(logn)$
    - Linked List: $O(n)$


