<extoc></extoc>

# Java

## Coding Style
[Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)

1. Naming - use upperCamelCase for class names and all upper cases for const variable, otherwise lowerCamelCase.

2. Separate reversed words and bracelets. 
reversed words - 保留字

- Eg. ```for ()```
- Eg. ```a && b```

3. Add spaces on both sides of binary or ternary operators.

- Eg. ```a + b```


## Primitive types vs. Class types

__Primitive types:__

- `boolean`/`byte`/`char`/`short`/`int`/`long`/`float`/`double`
- `5`/`5.5` are objects.
- Strings are objects.
- Arrays are objects.

### Array

```java
int[][] array = new int[2][];
array[0] = new int[1];
array[1] = new int[3];
```

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

## Parameter Passing

**Java parameters are always passed by value.**

- **primitive type**: copy of the value itself
- **objects**: copy of the object reference

## Inheritance, Interface, Abstract Class

__Inheritance（继承）__ - Base class（父类）, Derived Class（子类）

C++: Abstract class
Java: Interface and Abstract Class

### Java Interfaces & Abstract Classes

**Interface** helps you (or enforces you) to focus on the API signature definition.
**Abstract Class** provides a common base class implementation to derived classes. Use abstract class (or even concrete class) for base class if the derived classes share common implementation

- 为什么要用List作为Interface？

    ```java
    List<Integer> myList = new LinkedList<>();
    ```

    把接口和实现分开实现。因为这里我们仅仅需要List的语义，我们要的不是一个特定的List。实现可能会变化。
    
    Eg.
     
    ```java
    List<Integer> myList = creatListFromConfig(conf);
    ```
    
- 父类List有的功能，子类LinkedList一定有。


__Abstract class vs. interfaces__

[Java docs](https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html)

Abstract class | Interface
----|----
using **extends** | **implements**
methods can be declared without implementation | same
cannot instantiate | same
can give implementation | cannot
doesn't support multiple inheritance | support
... | ...


```java
interface A {
    public Integer get(int index);
}

interface B {
    public void put(int index, E e);
}

A myDict = new A(); // wrong

class myList implements A, B {
    @override
    public Integer get(int index) {
    }
    @override
    public void put(int index, E e) {
    }    
}
```

### Polymorphism and Overriding

Polymorphism 多态 : 函数参数不同是不同的函数。

Override: a 

## Nested Class

- Static nested class - can access class varibles and methods
- Nonstatic nested class / Inner class - can access instance varibles and methods
把class定义在另一个class里面