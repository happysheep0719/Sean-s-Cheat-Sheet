<extoc></extoc>

# Objected-Oriented Design

## Books Recommendation
 
for beginners: *head first java*

for intermediates: 

- *effective java*
- Java source code (e.g. ArrayList, LinkedList, HashMap, PriorityQueue...)

Book on Computer Systems: *A programmer's perspective CSAPP*

*Design Pattern*
*Java tutorial*
*The Pragmatic Programmer: from Journeyman to Master*

## Introduction

**3 advices to answering design questions**

1. 文（design）无第一，武（coding）无第二
    - 很有可能最优design不存在的，换一个场景可能就换了个解法
    - coding则会有好坏之分
2. 尽信书则不如无书，过程比结果更重要
3. 冰冻三尺非一日之寒

no silver bullet - 真正的银弹并不存在；所谓的没有银弹是指没有任何一项技术或方法可使软件工程的生产力在十年内提高十倍。

__What is good code/design?__

- Complete functionality
- __Easy to use (by others)__
    - clear, elegant, easy to understand, no ambiguity
    - prevent users from making mistakes
- __Easy to evolve__

__Motivation of OOD__

- Structured programming : code + data 代码和数据的合理组织
    - Each object is defined by two kinds of information: state/behavior.
        - state: field - what things it maintains;
        - behavior: method - what it can do.
- Limitedly exposed interfaces/API

**Object-Oriented Design vs. Procedure-Oriented Design**

-|面向对象|面向过程
----|----|----
解决问题的模块|函数（怎么做）|对象（谁来做）
角度|先具体逻辑细节，后抽象问题整体|先抽象问题整体，后具体逻辑细节
封装特性支持|继承、多态|重载、覆盖

Note:

**重载**：使用同名函数，但是形参不同，可以是个数，也可以是类型，顺序。


## Three ways of OOD

- **Encapsulation** **封装**
    - encapsulate data and methods in class
    - Data Abstraction and Access Lebels
- **Inheritance** **继承**
    - base class and derived class
    - In Java, Interface and Abstract class
- **Polymorphism** **多态**
    - Overriding 
    - In Java, `List.get()` has different implementations. It is different for each call of different class implementation.

### Encapsulation

__Data Encapsulation: Data Abstrction and Access Levels__

- Providing only essential information to the outside world and hiding their background details
- Separate interface and implementation
- Access Labels: public, private, protected, default

Access | public | protected | private
----|----|----|----
Same class | yes | yes | yes
Derived class | yes | yes | no
Outside class | yes | no | no

In Java, add one access level - **no modifier**(**default**) and one kind of class - **package**

- no modifier is accessible to classes in the same package but not to a subclass

Note:

- 存在嵌套关系的package并不属于同一个package，import的时候也只会import父亲，而不会import子孙。


__How to select appropriate access labels?__

As strict as possible.

- API: public
- Internal Implementation: private
- Class inheritance: do we need to use protected for methods/attributes
    - Protected methods: sometimes useful when we want to override an implementation in subclasses
    - Protected attributes: be careful, try to use private first
- default in java(package-private)

## General steps for OOD

1. Understand/Analyze the **use case**
    - 换位思考
    - use cases -> API, what is input/output?
    - from top level to bottom level
2. Classes and their relationships
    - Single-responsibility Pricinple - A class should have only one job
    - **Class relationships**
        - **Association** 
            - eg. Vehicle - Parking Spot
        - **Aggregation/Compostion/has-a** 
            - eg. Parking Lot - Level - Parking Spot
        - **Inheritance/is-a** 
            - eg. Car, Truck
3. For complicated designs, first focus on public methods (APIs). Discuss the implementation details later!
    - Basic functionality: use case
    - Possible extensions (Product Road Map): provide available spot locations, ...



4. Complete implementation Details

```java
public class ParkingLot{
    private Level[] levels;
    
    public boolean hasSpot(Vehicle v){
    // TODO
    }
    
    class Level{
        // boolean hasSpot(Vehicle)
    }
    
    class ParkingSpot{
        // boolean fit(Vehicle): check size and availability
    }
    
    class abstract class Vehicle{
        // getSize()
    }
    
    class car, bus, ... extends Vehicle
}
```

- 用enum常对象给VehicleSize的项目赋予size的属性。

```java
public enum VehicleSize{
    Compact, Large
}
```

- use unmodifiable class

```java
Colltions.unmodifiableList(list);
```

- **Do not include the mapping from Vehicle to ParkingSpot in the field of the Vehicle class.**
    - Reasons：逻辑不清楚，从属不清楚。实现容易出错，最好不要让对象相互环形持有对方。

```java
HashMap<Vehicle, ParkingSpot>
```

## Steps

1. Understand / Analyze the **functionality** and its **use case**
    
    What is the problem and its use case?

    Details: Describe the parking lot building? Vehicle monitoring? What kind of parking lot?
    
    **use cases** -> **functionalities** -> **APIs**
    
    **functionalities**
    
    - the main functionality
    - input/output of the main functionality
        - **Request** -> **Schedule & move elevator** -> Load onto elevator -> schedule and move elevator -> unload

    
    **Modeling**
    
    - Visble
        - Elevators
        - Users
        - Floors
    - Invisble
        - Requests
        - Controller
        - Simulation program itself

2. Classes and their relationships
    
    Data - Classes and their member fields
    Action - Methods
    
    Single-responsibility Principle: A class should have only one job.
    
    **Abstraction** & **Decouple**: to sperate logics. 

---------
**Example 1.** **Parking Lot**


**Example 2.** In card games like **BlackJack**, the data are to describe the states of cards and game. 

- Data - 公共道具（牌堆）
- Action - 流程规则


The actions are the rules and the game process.

1. What **data** are used.
2. What manipulation are done on the data.

**Example 3. Elevators**

Elevator

- State
    - id
    - maximum capacity
    - current laod size
    - current location
    - loaded requests
    - next destination
    - moving direction
- Behavior
    - load(weight)
    - unload(weight)
    - move design
        - X--moveTo(floor)--
        - moveUp()/moveDown() (stateless design)
        - move()/stop()/Change moving direction (stateful design)

    
Note:这里的目的是为了把电梯的行为拆分，分析的关键在于把调度的功能和移动的功能解耦。调度功能放在simulator里面。


Users

- State
    - current location
    - request
- Behavior
    - send request
    - enter elevator
    - leave elevator

Requests

Simulator


