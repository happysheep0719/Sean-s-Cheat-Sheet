<extoc></extoc>

# Java

## Coding Style
[Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)

1. Naming - use upperCamelCase for class names and all upper cases for const variable, otherwise lowerCamelCase.

2. Separate reversed words and bracelets. 
reversed words - 保留字
Eg 1. ```for ()```
Eg 2. ```a && b```

3. Add spaces on both sides of binary or ternary operators.
Eg.
```a + b```


## Primitive types vs. Class types

__Primitive types:__
- boolean/byte/char/short/int/long/float/double
- 5/5.5 are objects.
- Strings are objects.
- Arrays are objects.

### Array

int[][] array = new int[2][];
array[0] = new int[1];
array[1] = new int[3];

取subarray，使用arrays工具箱。


## Static & Final

__1. static__

- class variable vs. instance varible
- class method vs. instance method
- unlike C++, local static varible is not allowed.

__2. final__

- final class: A class that cannot be dereived. 最终类。不能被继承。
- final method: A method that cannot be overridden.
- final field/var: A varible that once assigned, cannot be assigned again.

define a **constant var** in Java:

```
// Cannot change the value
final int value = 10;
```

define a **constant reference** in Java:

```
// Cannot change the reference value
final Boy b1 = new Boy(10);

// Can change the object field varibles
b1.girlFriend = new Girl("Lady gaga");
```

## parameter passing

**Java parameters are always passed by value.**

- **primitive type**: copy of the value itself
- **objects**: copy of the object reference

## Abstract class and Interfaces

Both can have methods declared without implementation (abstract methods).

```
interface Dictionary {
    public Integer get(int index);
}

Dictionary myDict = new Dictionary(); // Wrong !

class DictionaryImp1 implements Dictionary {
    @Override
    public Integer get(int index) {
    
    }
}
```
Cannot instantiate an object by abstract class or interfaces


## Java Interfaces & Classes

__Abstract class and interfaces__

```
interface Dictionary {
    public Integer get(int index);
}

Dictionary myDict = new Dictionary();

```


| Operations | List | ArrayList | LinkedList |
|----|----|----|----|
|length|.length()|.length()|.length()|
|get| .get(i) | .get(i)| .get(i) |


List Interface in Java

- Random Access:
    set(int index, E e)
    get(int index)
    add(int index, E e), add(E e)
    remove(int index)

- Search
- Iterator
- Range-View
- isEmpty();
- size();
