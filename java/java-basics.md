<extoc></extoc>

# Java

## Difference Between Java & C++

Java: Platform compatible, write once, compile once, run everywhere on JVM.

C++: write once, compile everywhere


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

- `boolean`/`byte`/`char`/`short`/`int`/`long`/`float`/`double`
    - `char` ranges from `0``\u0000` to `\uffff``65535` (16-bit unicode)
- `5`/`5.5` are objects.
- Strings are objects.
- Arrays are objects.

### Autoboxing and Unboxing

- Wrapper class
    - allow null
    - immutable internal values
- **Autoboxing & unboxing are done only when it is necessary.**
    - Mannual: `Integer a = Integer.valueOf(4);`
- `==` vs. `equals`
    - `Integer a == Integer b` can be wrong
    - `(Integer)a.equals((Integer)b)` or `Integer.compare(o1, o2)` should be used!
- `int[]` vs. `Integer[]`
    - there is no auto conversion directly between them.
- Unboxing null throws NPE (Null pointer exception).

### Compare Integer

```java
Integer i1;
Integer i2;
i1 == i2 // wrong!
i1.equals(i2) // right
```

### Converting Number to/from Strings

- factory method

```java
int i = 0;
String si = i + "";
si = String.valueOf(i); // factory
si = Integer.toString(i);

Integer w = null;
si = w.toString(); // "null"
si = String.valueOf(w); // factory

Integer.valueOf(si); // factory
Integer.parseInt(si);
```

- from string to integer

```java
public int parsePosInt(String str) {
    int res = 0;
    for (char c: str.toCharArray()) {
        res = res * 10 + (c - '0');
    }
    return res;
}
```

## Array

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

class extends class
class implements interface
interface extends interface

- **Override** vs. **Overload**
    - Override is to redefine a method that has been defined in a parent class
    - Overload is when you define two methods with the same name distinguished by their different signatures.
        - Overload has nothing to do with polymorphism
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

- When do we use abstract class vs. interface?
    - abstract class provides a common base case implementation to derived classes
    - if we want to declare non-public members
    - if we need to add methods in the future

### Polymorphism and Overriding

Polymorphism 多态 : 调用override的function

java会根据实际的object而决定调用的行为。

### Design

残疾人是一个有残疾状态的人，不应该是子类。因为残疾可能会变好。


## Top Level Class

- One Java file have only one public class.
- One Java file can have more than one classes.
- A helper class is at most package access level but a static nested can be public.

## Nested Class

- **Static nested class** - can access class varibles and methods
    - It is a way of logically grouping classes that are only used in one place.
    - It increases encapsulation. Consider we hide B into A. We can set members in A to be private and B can access them and be hidden from outside A.
- **Nonstatic nested class** / **Inner class** - can access varibles and methods
    - **Inner class cannot be created without an instance of outer class while nested class can.**
    - `return Outerclass.this;`
- **Anonymous class**
    - Comparators, lambda

## Iterator


### Iterator

- `next()`
- `hasNext()`
- `remove()` (optional)

```java
for (Iterator<Apple> iter = list.iterator(); iter.hasNext();) {
    Apple apple = iter.next();
    System.out.prinln(apple)
}
```

为什么使用Map的View时候删除会报错Concurrent Modification Exception。

### ListIterator

- `previous()`
- `previousIndex()`
- `hasPrevious()`
- `nextIndex()`


## Generics

- Types are parameters
- A type or method to operate on objects of various types while providing **compile-time** type safety (vs. runtime safetyl too late, exceptions).
- E T K V U
- 原理：类型擦除保留原始类型

```java
List list = new ArrayList();
Apple apple = (Apple) list.get(0);
```

```java
// read time, fever codes
List<Apple> list = new ArrayList<>();
Apple apple = list.get(0);

// write time, safety check
list.add(new Orange()); //wrong
list.add(new Fruit()); // wrong

// Itertor gets better (no need to cast)
for (Iterator<Apple> iter = list.itertor(); iter.hasNext();) {
    Apple apple = iter.next();
}

// for each
for (Apple apple : list) {
    apple.printOut();
}
```

- Static methods(needs to declare generic type again)

```java
public static <T> T getFirst(List<T> list) {
    return list.get(0);
}
```

- Subclass and Superclass in Generics

```java
Apple apple = new Apple();
Fruit fruit = apple; // ok

Fruit fruit = new Fruit();
Apple apple = fruit; // wrong, need cast
Apple apple = (Apple) fruit; // ok at compile time, but may have java.lang.ClassCastException at runtime
```

- List of T cast

```java
List<Apple> a = new ArrayList<>();
List<Fruit> b = a; // not allowed.
// b can add new Orange(). a cannot add new Orange(). a and b refer to the same object.

List<Fruit> a = new ArrayList<>();
List<Apple> b = a; // not allowed either.
```

- Generics check the type during the compile-time while **Array does not**.

```java
Apple[] apples = new Apple[3];
Fruit[] fruits = apples; // ok at compile time
fruits[0] = new Apple(); // ok
fruits[1] = new Fruit(); // ArrayStoreException
fruits[2] = new Orange(); // ArrayStoreException
```

- `? extends T` and `? super T`
    - give read-time flexibility

```java
List<? extends Fruit> fruits = apples;
```

```java
public static <E extends Comparable<E>> E getMin(E[] arr) {
    ...
}
```

## Enum

```java
class RainbowColor {
    public static final int RED = 0;
    public static final int BLUE = 1;
}
```

```java
enum RainbowColor {RED, ORANGE, YELLOW}

switch(today) {
    case Mon: do(something); break;
    case Tue: do(something); break;
}
```

- `enum.values()`
- `constant.valueOf()`
- `constant.ordinal()` returns the order

```java
enum Weekday {
    Mon, Tue, Wed, Thu, Fri, Sat, Sun
}

Weekday[] l = Weekday.values();
for (Weekday wd : l) {
    System.out.println(wd + " " + wd.ordinal());
}


Weekday wd = Weekday.valueOf("Mon");
Weekday wd = Weekday.valueOf("Monday");
```

- Extends Enum

```java
final class MyDay extends Enum {
    public static MyDay[] values() {return (MyDay[])$VALUES.clone();}
    private MyDay(String s, int i) {
        super(s, i);
    }
    
    public static final MyDay MONDAY;
    public static final MyDay TUESDAY;
    public static final MyDay $VALUES[];
    
    static {
        MONDAY = new MyDay("MONDAY", 0);
        TUESDAY = new MyDay("TUESDAY", 1);
        
        $VALUES = (new MyDay[] {MONDAY, TUESDAY});
    }
}
```

- Enum classes and anonymous class

```java

```
