<extoc></extoc>

# Exceptions

**Error** indicates serious problems that a reasonable application should not try to catch.

- `StackOverflowError`

**Exception** indicates conditions that a reasonable application might want to catch.

`Error` and `Exception` extend from `Throwable`

`Error` and all exceptions in `Runtime Exception` can be not caught in the compiling.

`Exception`是`Throwable`的子类，包含一些有用的函数。

## Catch an exception

```java
try {
    return;
} catch (IOException e) {
    return;
} catch (Exception e) {
    return;
} finally {
    return;
}
```

## Define an exception

`Exception`是`Throwable`的子类，包含一些有用的函数。

```java
public class MyException extends Exception {
    public MyException(){
        super();
    }
    public MyException(String msg){
        super(msg);
    }
}
```

## New feature in Java 7

```java
try (BufferedReader br = new new BufferedReader(new FileReader(path))) {
    return br.readline();
}
```

```java
BufferedReader br = new BufferedReader(new FileReader(path));
try {
    return br.readline();
} finally {
    if (br != null) br.close();
}
```
