<extoc></extoc>

# Java String

- `String`
    - `int capacity()`
    - **`char charAt(int index)`**
    - `int indexOf(String str)`
    - `int indexOf(String str, int fromIndex)`
    - `int lastIndexOf(String str)`
    - `int lastIndexOf(String str, int fromIndex)`
    - **`int length()`**
    - `String substring(int start)`
    - **`String substring(int start, int end)`** output = input[start, end)
    - `String toString()`
- `StringBuilder`
- `StringBuffer`
    - same as `String`
    - `StringBuffer append(String s)`
    - `StringBuffer reverse()`
    - `delete(int start, int end)`
    - **`deleteCharAt(int index)`**
    - `insert(int offset, int i)`
    - `replace(int start, int end, String str)`

```java

public class Test{
  public static void main(String args[]){
    StringBuffer sBuffer = new StringBuffer("菜鸟教程官网：");
    sBuffer.append("www");
    sBuffer.append(".runoob");
    sBuffer.append(".com");
    System.out.println(sBuffer);  
  }
}

```

## String to Char Array & Char Array to String

- [startIndex, endIndex)
- [offset, offset + count)

```java
public char[] convert(String input){
    return input.toCharArray();
}

public String substring(String input, int offset, int count){
    return new String(input, offset, count);
}


public String convert(char[] input, int startIndex, int endIndex){
    return input.substring(startIndex, endIndex);
}
```