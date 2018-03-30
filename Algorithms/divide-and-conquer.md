# Binary Search

__适用的问题__
1. 不能死循环，每次循环会减少解空间。
2. 不能在循环中，把正确答案排除掉。

__Coding Tips__
1. 循环进入条件

start + 1 < end
start < end
start <= end

2. 调试方法

使用base case, Eg. [0], [0, 1], [0, 1, 2]

# Binary Search
**Binary Search Template**
Source: [jiuzhang](http://www.jiuzhang.com/solutions/binary-search/)

```java
class Solution {
/**
* @param nums: The integer array.
* @param target: Target to find.
* @return: The first position of target. Position starts from 0.
*/
public int binarySearch(int[] nums, int target) {
# First consider the case that the input is null or empty array.
if (nums == null || nums.length == 0) {
return -1;
}
# initial condition. The end is included in the range of the num,
# because the end is initialized to the length of nums minus one
int start = 0, end = nums.length - 1;
# Here, the condition should be start+1<end.
# because when start=0 and end=1, then mid=0
# and the start may not be updated.
while (start + 1 < end) { # Note: use start+1<end as the condition to continue
int mid = start + (end - start) / 2;
if (nums[mid] == target) {
end = mid;
} else if (nums[mid] < target) {
start = mid;
// or start = mid + 1
} else {
end = mid;
// or end = mid - 1
}
}
# When the loop is end, decide where the first postion of target is.
if (nums[start] == target) {
return start;
}
if (nums[end] == target) {
return end;
}
return -1;
}
}
```
Note:
1. The loop control condition should be