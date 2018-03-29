``` flow
st=>start: Start|past:>http://www.google.com[blank]
e=>end: End:>http://www.google.com
op1=>operation: My Operation|past
op2=>operation: Stuff|current
sub1=>subroutine: My Subroutine|invalid
cond=>condition: Yes
or No?|approved:>http://www.google.com
c2=>condition: Good idea|rejected
io=>inputoutput: catch something...|request

st->op1(right)->cond
cond(yes, right)->c2
cond(no)->sub1(left)->op1
c2(yes)->io->e
c2(no)->op2->e
```


$$\int_{-\infty}^\infty g(x) dx$$


$$
\int_{-\infty}^\infty g(x) dx
$$

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
