<extoc></extoc>

# Dynamic Programming

- 把大问题分解为很多个小问题，思考如何用小问题的solution构建大问题的solution (Recursion)
- 记录Sub-solutions (Memorization)

常见：最大最小值

## DP vs. Recursion

- recursion：从大到小解决问题，不记录任何sub-solution
    - base case
    - recursive rule
- DP：从小到大解决问题，记录sub-solution
    - size(<n) subsolution -> size(n) subsolution
    - base case
    - induction rule
- 满足一定条件的recursion可以用dp


__P1. Longest Ascending Subarray__

Array vs. Sequence

sub-Array: phsical contiguous elements in an array
sub-Sequence: not necessarily contiguous

__P2. Cut ropes__

Note: 之所以说DP是从小到大解决问题，是因为我们只解决每个子问题一遍，而且严格地按照从规模小到规模大的问题的顺序解决。使用Recursion比较不容易控制解决问题的顺序。


