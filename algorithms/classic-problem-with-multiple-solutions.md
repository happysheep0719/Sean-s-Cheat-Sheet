<extoc></extoc>

# Classic Problems with Multiple Solutions

## K-Sum
### 2-Sum

- Sorted input
    - two pointers, time O(n) space O(1)
    - 证明：循环证明。有点绕，大概意思就是所有被排出的数都可以被之前被排除的数的结论推导得到。
    - assume we have Xi0 + Yj0 < t
    - then we got: for all Xi < Xi0, Xi + Yj0 < t
    - all Xi < Xi0 are excluded with Yj >= Yj0 under only one situation that Xi + Yj < t
        - that is, for all Xi < Xi0, exists Yj1 >= Yj0 that Xi + Yj1 < t
    - for Yj > Yj1, it is excluded with Xi1 <= Xi0 under only one situation that Xi1 + Yj1 < t
        - that is, for all Yj > Yj1, exists Xi2 <= Xi1 that Xi2 + Yj > t
    - conclusion: for all Xi < Xi0, we have Yj >= Yj0, Xi + Yj != t
- Unsorted input
    - sort first, then use methods for sorted input
        - quick sort, Space average O(logn) worst O(n)
        - merge sort, Space O(logn)
        - selection sort (recursively select the max/min and swap it with the number in the right place), Space O(1), Time O(n^2)
            - optimized space
            
- What if the data cannot fit in the memory? (sorted input)
    - use two pointers
    - use cache

### 3-Sum

```java
for (int i = 0; i < input.length; i++) {
    run2Sum(input, i + 1, input.length - 1, target - input[i]);
}
```
