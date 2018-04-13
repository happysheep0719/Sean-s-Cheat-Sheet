<extoc></extoc>

# Java String

- `String`
    - `int capacity()`
    - `char charAt(int index)`
    - `int indexOf(String str)`
    - `int indexOf(String str, int fromIndex)`
    - `int lastIndexOf(String str)`
    - `int lastIndexOf(String str, int fromIndex)`
    - `int length()`
    - `String substring(int start)`
    - `String substring(int start, int end)`
    - `String toString()`
- `StringBuilder`
- `StringBuffer`
    - same as `String`
    - `StringBuffer append(String s)`
    - `StringBuffer reverse()`
    - `delete(int start, int end)`
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