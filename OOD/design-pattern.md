<extoc></extoc>

# Design Pattern

## Builder Pattern

**Motivation**

- reduce the number of constructors
- control the exposure of limited data while having multiple options to initialize an instance
- ensure when an instance is completedly initialized semantically

```java
public class User {
    private final String firstName; // required
    private final String lastName; // required
    private int age;
    private String phone;
    private String address;
}

private User(UserBuilder builder){
    this.firstName = builder.firstName;
    this.lastName = builder.lastName;
    this.age = builder.age;
    this.phone = builder.phone;
    this.address = builder.address;
}

public static class UserBuilder {
    private final String firstName; // required
    private final String lastName; // required
    private int age = 0;
    private String phone = "";
    private String address = null;
    public UserBuilder(String firstName, String lastName){
        this.firstName = firstName;
        this.lastName = lastName;
    }
    
    public UserBuilder age(int age){
        this.age = age;
        return this;
    }
    public UserBuilder phone(String phone){
        this.phone = phone;
        return this;
    }
    public UserBuilder address(String address){
        this.address = address;
        return this;
    }
    public User build(){
        return new User(this);
    }
}

public static void main(String[] args){
    User user = new User.UserBuilder("San", "Zhang")
    .age(25)
    .phone("1234567890")
    .address("Fake Address")
    .build()
}

```


## Factory Pattern

**Motivation**

- Create objects **without specifying the exact class** of object that will be created. Separate instance/object creation logic from its usage
    - eg. We want lots of `Shape`s. Some of them can be `Rectangle`s. Some of them can be `Circle`s. We want to create those from its `Name`s.

## Abstract Factory

**Motivation**

- Provides a way to encapsulate a group of individual factories that have a common theme without specifying the concrete classes.

## Singleton

**Motivation**

- Ensure a class has only one instance and provide a global access point to that instance.

```java
public class Singleton {
    private _static_ final Singleton INSTANCE = new Singleton();
    _private_ Singleton() {}
    
    _public static_ Singleton getInstance(){
        return INSTANCE;
    }
}
```