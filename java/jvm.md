<extoc></extoc>

# Java Virtual Machine JVM

[Java tutorial](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html)

**JRE** - Java Runtime Environment

- JRE is the JVM program.

**JDK** - Java Development Kit

- JDK contains the tools for developing Java programs running on JRE.
    - for example, it provides the compiler 'javac'
    
[!HotSpot JVM: Architecture](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/images/gcslides/Slide1.png)

## Garbage Collection


- What is GC?
    - GC is the mechanism to automatically detect/delete the unused objects.
- Why do we need it?
    - More efficiently manage dynamic memory allocation.
- How does it work?

**stack vs. heap**

**Stack** - local varible, tracking method call flow, return address etc. - one per thread
**Heap** - dynamic memory allocation - only one per JVM


### Step 1 Marking

The first step in the process is called marking. This is where the garbage collector identifies which pieces of memory are in use and which are not.

[!marking](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/images/gcslides/Slide3.png)

### Step 2 Normal Deletion

[!normal deletion](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/images/gcslides/Slide1b.png)