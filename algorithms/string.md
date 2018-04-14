<extoc></extoc>

# String

__Popular Represenatation of Characters__

- ASCII
    - A == 65, a == 97
- Unicode

## Basic Problems

__Idea__

- 把string当成char array来思考，最好使用**in-place**写法
- 循环中间改变（删除）string，会影响for循环次数
    - Solution: `i--` / `i++`
- 避免频繁调用`deleteCharAt(i)`，因为花费$$O(n)$$时间。
    - 常使用**Two Pointers**的两个隔板把字符串分成三个部分：已经检查的 | 已经删去的 | 未检查的 

__P1. Char Removal__

- `solution -> soltio`
- 字符串只减小不增大
- Solution: 使用**Two Pointers**的同向的两个`pivot`把字符串分成三个部分：已经检查的 | 已经删去的 | 未检查的 

__P2. De-dupliaction__

- `aaaabbbbcc -> abc`
- 字符串只减小不增大
- Solution: 使用**Two Pointers**的同向的两个`pivot`把字符串分成三个部分：已经检查的 | 已经删去的 | 未检查的

__P3. Sub-string Finding (strstr)__

- regular method
- Robin-Carp (hash based string matching)
    - use Hash Function to get the hashcodes of all substrings, which has the same length as the pattern does.
- KMP (Knuth-Morris-Pratt)

__P4. String Reversal (swap)__

- `I love yahoo -> yahoo love I`
- Step 1: swap the whole sentence
- Step 2: swap every single word (two pointers)

__P5. String Replacement__

- Eg. replace empty space " " with "20%"
- Case 1: pattern.length >= replacement.length
    - use **Two Pointers**
- Case 2: pattern.length < replacement.length
    - Step 1: count how many times show up in the original string and extend the string to new string with empty space in the right.
    - Step 2: use **Two Pointers** 同向双指针，**从右往左**扫描。未扫描区域 | 待复制区域 | 已处理区域


## Advanced Problems

__P1. String Shuffling__

- `ABCD1234 -> A1B2C3D4`
- Merge sort with custom comparator
- Reverse of Merge Sort - Space $$O(n)$$
- swap the 2nd and the 3rd part - Space $$O(1)$$

- follow-up: sorted array 被push到deque里面（任意方向），然后又被pop出来（任意方向），如何用$$O(n)$$的时间恢复sorted array?

__P2. String Permutation__

- CANNOT have duplicate string in the result
- DFS
- Situation 1: no duplicate letters in the input string
- Situation 2: exists duplicate letters in the input string

__P3. String Decoding/Encoding__

- `aaaabcc -> a4b1c2`
- 可能越界
    - 这个时候如果只出现一次，那么不使用数字
    - 先拓展string

__P4. Sliding Window in a string__

- Longest substring that contains only unique chars
- use a sliding window
- use a hash table to record the existence of characters

__P4 follow-up. Sliding Window in a string__

- find all anagrams （同构异形体） of a substring S2 in a long string S1
- anagrams: reorder of the original string, bcaa -> acab
- Solution 1
    - use a hash table to record the counts of all charcters
    - compare the hash table of each sliding window to that of the original pattern
    - if the two hash tables are the same, return
- Solution 2
    - use a hash table to record the difference of the appearances of each character.
    - use a counter to count the zeros in the hash table
    - if the counter equals 0, return

__P4 follow-up. Sliding Window in a string__

- given a 0-1 array, you can flip at most k '0's to '1's. Please find the longest subarray that consists of all '1's.
- use a sliding window
- use a counter to record the number of '0's and '1's.

__P5. Matching (*, ?)__


