Java
------
## Coding Style
[Google Coding Style Java]()
1. Naming - use upperCamelCase for class names and all upper cases for const variable, otherwise lowerCamelCase.


## Primitive types vs. Class types:
int/char/double
5/5.5
Strings are objects.
Arrays are objects.

### Array

int[][] array = new int[2][];
array[0] = new int[1];
array[1] = new int[3];

取subarray，使用arrays工具箱。



## Memory
Stack and heap
stack = call stack

## Static & Final

1. static

class variable vs. instance varible
class method vs. instance method

unlike C++, local static varible is allowed.


2. final

final class: A class that cannot be dereived. 最终类。不能被继承。
final method: A method that cannot be overridden.
final field/var: A varible that once assigned, cannot be assigned again.

define a constant in Java:

```
final int value = 10;
```

## parameter passing

Java parameters are always passed by value.

primitive type: copy of the value itself
objects: copy of the object reference





## Interface
**Queue**
LinkedList
.offer()
.poll()

