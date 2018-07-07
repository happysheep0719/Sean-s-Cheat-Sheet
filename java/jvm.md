<extoc></extoc>

# Java Virtual Machine JVM

**JRE** - Java Runtime Environment

- JRE is the JVM program.

**JDK** - Java Development Kit

- JDK contains the tools for developing Java programs running on JRE.
    - for example, it provides the compiler 'javac'
    
    

## Garbage Collection


- What is GC?
    - GC is the mechanism to automatically detect/delete the unused objects.
- Why do we need it?
    - More efficiently manage dynamic memory allocation.
- How does it work?

**stack vs. heap**

**Stack** - local varible, tracking method call flow, return address etc. - one per thread
**Heap** - dynamic memory allocation - only one per JVM


