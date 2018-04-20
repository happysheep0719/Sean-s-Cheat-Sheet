<extoc></extoc>

# Bit Representation

## Binary

Decimal -> Binary

One's Complement / **Two's Complement**

- 为什么这么设计？
    CPU处理时不用考虑符号

use 32bits for each number

```
 1 == 0000 0000 0000 0000 0000 0000 0000 0001
                       
      1111 1111 1111 1111 1111 1111 1111 1110
-1 == 1111 1111 1111 1111 1111 1111 1111 1111  plus 1
```

## Hexadecimal

32-bit signed integer max value = 0x7FFFFFFF

# Bit Operation

- & and
- | or
- ~ not
- ^ xor
- << left shift
    - add 0 to the right of positive number
- >> right shift
    - add 0 to the left of positive number
    - add 1 to the left of negative number
    - `3 >> 1 = 3 / 2 = 1`
    - `-3 >> 1 = -2` 负数除法不建议用位运算做

## bit check

```java
x & (1 << k)

(x >> k) & 1
```

## bit set

```java
x = x | (1 << k)
```