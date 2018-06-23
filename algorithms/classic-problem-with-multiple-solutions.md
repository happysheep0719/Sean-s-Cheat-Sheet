<extoc></extoc>

# Classic Problems with Multiple Solutions

## K-Sum
### 2-Sum

- Sorted input
    - use HashMap
        - HashMap<Target - input[i], i>
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
Time = O(n^2) sorted it first

### 4-Sum

Solution 1

```java
for i:
    for j:
        run 2Sum
```
Time = O(n^3)

Solution 2

```java
sum1 = <i1 + j1> => HashSet
sum2 = <i2 + j2>

for i:
    for j:
        current pair <i, j> with sum = input[i] + input[j]
        loop: 
            find pair in the hashSet with value = target - sum
            check duplicatation worst O(n)
```
Time = O(n^3)

Solution 3 - optimized from Solution 2

- We do not want duplication of set of 4 numbers.
    - we only store only one pair in the hashmap.
    - we want to ensure 4 numbers are arranged in order, like i1 < j1 < i2 < j2
    - when we add 2-sum pair into the hashmap, if for each i, we only keep the smallest j
    - for example, we have 1,2,7,9. we only keep pair (1, 2) and pair (7,9). when we have pair (1, 7), it is not add to the hashmap
    
```java
```
## DP && DFS && BFS2

### largest product of length

Given a dictionary containing many words, find the largest product of two words’ lengths, such that the two words do not share any common characters.

[laicode](https://code.laioffer.com/ui/#/app/problem/191)

1. no common characters
2. max product of length

Potential ways to solve max/min problem

- DP
- BFS2(best first search)
    - initial state
    - expansion/generation rule
    - termination condition
- DFS (brute force)
    - generate all the possible conditions and find the max

Time = O(n^2 * (log(n^2) + m))
    