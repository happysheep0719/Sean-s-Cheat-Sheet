<extoc></extoc>

# Dynamic Programming

- 把大问题分解为很多个小问题，思考如何用小问题的solution构建大问题的solution (Divide and Conquer)
- 记录Sub-solutions (Memorization)

常见：最大最小值

## What is DP? DP vs. Recursion

- recursion：从大到小解决问题，不记录任何sub-solution
    - base case
    - recursive rule
- DP：从小到大解决问题，记录sub-solution（数学归纳法）
    - size(<n) subsolution -> size(n) subsolution
    - base case
    - induction rule
- 满足一定条件的recursion可以用dp
- 空间复杂度可能可以通过只记录M[n-1]从$$O(n)$$优化到$$O(1)$$

## When do we use DP?

- **linear scan + look back **
- 大号问题应该可以通过小号问题的解答推导出来
    - 求largest/smallest（变体，在某一段范围求largest/smallest）
    - 分割类问题
    - 最长连续类问题
    - largest rectangle不行，因为需要找leftest/rightest hi < h，需要用前面所有的解，此时用单调栈会更简单一些。

## One Dimension DP

1. 左大段 + 右小段
2. 左大段 + 右大段

最小不可分的问题是similar和identical的。
->是->linear scan回帖都看
->否->右大段有可能有不同的pattern （cut postion类型问题）

### P1. Longest Ascending Subarray

- Array vs. Sequence
    - sub-Array: phsical contiguous elements in an array
    - sub-Sequence: not necessarily contiguous
- M[i] represents in String[0, i] the max length of the ascending subarrays. The substring must include i-th element. **(以i结尾的最长的substring)**
- $$M[i] = M[i - 1] + 1, if input[i] > input[i - 1]$$
- $$M[i] = 1, otherwise$$

### Follow-up. Longest Ascending Subsequence

### P2. Cut ropes

Note: 之所以说DP是从小到大解决问题，是因为我们只解决每个子问题一遍，而且严格地按照从规模小到规模大的问题的顺序解决。使用Recursion比较不容易控制解决问题的顺序。

### P3. Maximum subarray sum

- $$M[i]$$ represents the subarray with the largest sum among all subarrays that ends with i.
- $$M[i] = M[i - 1] + input[i], if M[i - 1] > 0$$
- $$M[i] = input[i], otherwise$$

### P4. Dictionary Concat

## Two Dimension DP

### P1. Edit Distance

### P2. Maximum Square of 1's in a binary matrix

__P3. __