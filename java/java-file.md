<extoc></extoc>

# Java File

**Stream**

- Byte Stream
    - 8-bit byte
    - `FileInputStream`
    - `FileOutputStream`
- Character Stream
    - 16-bit unicode
    - `FileReader`
    - `FileWriter`
- Standard Stream
    - standard input
    - standard output
    - standard error

Common Java Read/Write Operations

- stream handle input/output byte by byte
- we want to do it line by line
    - `BufferedReader`
        - `.readLine()`