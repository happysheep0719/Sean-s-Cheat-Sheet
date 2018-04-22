<extoc></extoc>

# Dynamic Programming

- 把大问题分解为很多个小问题，思考如何用小问题的solution构建大问题的solution (Divide and Conquer)
- 记录Sub-solutions (Memorization)

常见：最大最小值

## DP vs. Recursion

- recursion：从大到小解决问题，不记录任何sub-solution
    - base case
    - recursive rule
- DP：从小到大解决问题，记录sub-solution（数学归纳法）
    - size(<n) subsolution -> size(n) subsolution
    - base case
    - induction rule
- 满足一定条件的recursion可以用dp
- 空间复杂度可能可以通过只记录M[n-1]从$$O(n)$$优化到$$O(1)$$

__One Dimension DP__

__P1. Longest Ascending Subarray__

- Array vs. Sequence
    - sub-Array: phsical contiguous elements in an array
    - sub-Sequence: not necessarily contiguous
- M[i] represents in String[0, i] the max length of the ascending subarrays. The substring must include i-th element.**(以i结尾的最长的substring)**
- $$M[i] = M[i - 1] + 1, input[i] > input[i - 1]$$
- $$M[i] = 1, otherwise$$

__P2. Cut ropes__

Note: 之所以说DP是从小到大解决问题，是因为我们只解决每个子问题一遍，而且严格地按照从规模小到规模大的问题的顺序解决。使用Recursion比较不容易控制解决问题的顺序。

__P3. Larget Sum of a Subarrays__

- $$M[i]$$ represents among all subarrays that ends with i, the one with the largest sum.

__P4. Dictionary Concat__

__Two Dimension DP__

__P1. Edit Distance__

__P2. Maximum Square of 1's in a binary matrix__