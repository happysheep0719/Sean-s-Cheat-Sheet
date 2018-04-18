# Dynamic Programming

- 把大问题分解为很多个小问题，思考如何用小问题的solution构建大问题的solution。
- 记录Sub-solutions

## DP vs. Recursion
- recursion：从大到小解决问题，不记录任何sub-solution
    - base case
    - recursive rule
- dp：从小到大解决问题，记录sub-solution
    - size(<n) subsolution -> size(n) subsolution
    - base case
    - induction rule
- 满足一定条件的recursion可以用dp


## Longest Ascending Subarray

Array vs. Sequence

sub-Array: phsical contiguous elements in an array
sub-Sequence: not necessarily contiguous