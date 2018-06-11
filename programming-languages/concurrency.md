<extoc></extoc>

# Concurrency

## Concurrency vs. Parallel

**Concurrency** - multiple tasks run simultaneoutly (Semantic Concept)

**Parallel** - multiple tasks **physically** run simultaneouly (Implementation level)

- Eg. multilane highway, multicore machines, Hadoop clusters

Explanations:

- Two definitions have nothing to do with the order of different tasks
- On a single core machine, we still have concurrency and parallel. (pretend to do so)
- 冯诺依曼体系：（每个核）一个时刻只能执行同一条**指令**。但是和上面概念不矛盾。

**Ways to perform parallel programming** (to physically launch multiple executors)

- Multiprocess
- multi-thread
- I/O multiplexing

## Process vs. Thread

Ways | memory space | call stack | heap | os resource
----|----|----|----|----
**Process** | independent | independent | independent | independent
**Thread** | shared | independent | shared | shared

- Independent memory space is realized using **virtual memory** techniques in OS.
- Java concurrency is focusing on multithread cases in real life.
- 创建线程开销相对更小

**Problems in multi-thread**
- Communication overhead
- Resource isolation (fault tolerance)
- Creation/destroy overhead

### Java Thread

**Steps:**

- create the thread objects
    - each Java thread is mapped to one System thread (managed and scheduled by OS kernel rather than in user space)
- tell the threads what you want them to do
- start the thread

**Ways of creating threads and make them running:**

1) extends Thread

```java
Thread t = new Thread() {
    @Override
    public void run(){
        System.out.println("Hello");
    }
};
t.start(); // schedule the created thread and make ready to go
//
// concurrency here
System.out.println("Main Thread"); // main thread
//
t.join(); // make sure the thread finished after this line
```

2) implements Runnable (for the purpose of being not conflict with single inheritence rule)

```java
interface Runnable {
    void run();
}

class HelloRunnable extends Client implements Runnable {
    @Override
    public void run(){
        //..
    }
}

Thread newThread = new Thread(new HelloRunnable());
newThread.start();
newThread.interrupt();
```

**When the JVM will exit?**

- **no alive non-daemon threads**
    - default thread is non-daemon
    - create daemon thread using `Thread.setDaemon()` method

**Thread Operations**

- `.start()`
- `.run()`
- `.join()`
- `.sleep()`
- `.yield()` - 让出CPU资源。通常不需要手动使用。
- `.interrupt()`

**How do we determine which line is run at each time?**

- Scheduler + Queues: threads/processes are waited in queues, and there is a scheduler controls which thread/process is going to be run at the current time
- Each thread accepts a sequence of executed instructions

![threadLifeCycle](https://www.tutorialspoint.com/java/images/Thread_Life_Cycle.jpg)
![](http://www.runoob.com/wp-content/uploads/2014/01/java-thread.jpg)

- Ways to block a thread
    - `.sleep()` / `.suspend()`
    - `.wait()`
    - wait for synchronized lock
    - `.join()`
    - other blocks

## Synchronous procedure call Vs. Asynchronous procedure call

[Thread or process synchronization](https://en.wikipedia.org/wiki/Synchronization_(computer_science)#Thread_or_process_synchronization)

> Thread synchronization is defined as a mechanism which ensures that two or more concurrent processes or threads do not simultaneously execute some particular program segment known as critical section. 

[Asynchrony](https://en.wikipedia.org/wiki/Asynchrony_(computer_programming))


**异步调用**的三种方式

1. 单向调用：客户端发出请求之后不再关心服务端的情况
2. 延迟响应：在第一次发出调用请求的时候，服务端需要返回一个称为票据（Ticket）的对象。客户端通过后续的调用查询请求结果。票据对象会作为第二次发出检索结果请求时的一个参数。（有些地方称为同步非阻塞，因为通过轮询方式不断地查询本身就是同步的）
3. 请求回调：客户端发出调用请求，服务端立刻返回。服务端得到请求的结果之后，通过回调方式通知客户端触发响应。

**关于Tornado**

>Tornado is a Python web framework and **asynchronous networking library**, originally developed at FriendFeed. **By using non-blocking network I/O**, Tornado **can scale** to tens of thousands of open connections, making it ideal for long polling, WebSockets, and other applications that require a long-lived connection to each user.

- Tornado provides asynchronous functions (in its library) to call
- Tornado ioloop is condition synchronization by epolling for non-blocking
- By using non-blocking I/O, we can increase our programme's performance

## Synchronization & race

**Synchronization** - the **coordination** of events to operate a system in unison.

Impose orders on (previously) concurrent events. 我们人为提供时间执行的顺序。

How? Locks (synchronized), concurrent data structures, wait/notify (condition synchronization), volatile, ...

**Data races** - if two "conflicting operations" are in different threads and are not properly synchronized (concurrent), they will introduce data races.

冲突可能发生在CPU指令层次，最后会导致读操作对写操作产生影响。所以一定要同时对读操作和写操作采用合适的同步操作。

**3 factors can form a data race**

- More than one operations work on the same memory location
- At least one oepration is a `write`
- At least two of those opreations are concurrent

## Mutual exclusion, critical section, and lock

The most typical way to get rid of data races: **locks**

Or, on the semantic side: **mutual exculsion**

lock锁的是代码不是资源

No two concurrent processes are in their critical section at the same time. And a **critical section** can be defined as:

A part of a multi-process program that may not be concureently executed by more than one of the program's processes/threads.

**How to create a critical section?**

- A general lock has two operations: lock and unlock.
- Lock: wait no one is there and go into the critical section
- Unlock: Leave the critical section and mark no one is here

**Our goals in parallel programming**

1. Data race freedom
2. determinism

Lock **Granularity** 粒度:

- coarse grained lock (CGL) 粗粒度锁
- fine grained lock (FGL) 细粒度锁
- critical section
    - avoid super slow opeartions in a **critical section**, such as IO

### Mutual exclusion in Java

1. synchronized keyword

```java
private int value;
public void increase() {
    synchronized(this) {
        value++;
    }
}

public synchronized void decrease(){
    value--;
}
```

- synchronized on non-static method == synchronized(this)
- synchronized on static method == synchronized(Counter.class) != synchronized(all instances)

2. `synchronizedMap` is a wrapper of `Map`

3. `concurrentHashMap` separates HashMap into segements and perform sync operations on each one of them separately (sharding, federation).

### Locks in Java

```java
Lock L = ...;
l.lock();
try {
    // access the resource protected by this lock
} finally {
    l.unlock();
}
```

[ReentrantLock](https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/locks/ReentrantLock.html)

### Dead Lock

- **Defintion**
    - P1: holding Lock 1, trying to acquire Lock 2
    - P2: holding Lock 2, trying to acquired Lock 1
- **Conditions to form a deadlock**
    - **Mutual Exclusion**
        - Cannot avoid. We want mutual exclusion for synchronization
    - **Hold and Wait** or **Resource Holding**
        - Can avoid by using one lock at a time
    - **No Preemption** (抢占)
        - Cannot avoid. We do not have this kind of mechanism sometimes
    - **Circular Wait**
        - Can avoid by arranging the order of locks
        
### Live Lock

live lock will happen if each side is actively resolving the problem (backoff and retry)

**Solutions**

- priority
- randomize

## Atomicity

**volatile**

- guarantees **visibility** (semantically, happens-before), much like acquiring and releasing a lock.
    - **为单个变量提供独占性，避免data race**
- does not guarantee **atomicity**
    - only guarantees single read/write operation is atomic. But in a read-then-update case (or more complicated), we want to gurantee `value++` is atomic.
    - use `synchronized` or `AtomicInteger` instead
    - use [double checked locking](https://en.wikipedia.org/wiki/Double-checked_locking) in Singleton case
- **Common use case**
    - flag to stop (read/write only for each thread)

```java
public volatile boolean flag = false;
```

## Condition synchronization

Think this in real life: wait for some important mail. I can:

- keep waiting there (very low efficiency)
- periodic check and go (better efficiency, but may delay, how long shall I wait?)
- use tracking service and notification it will send you messages when it comes! (high efficiency, almost no delay)

Here we can do similar things: instead of busy waiting or periodic checking, we need a mechanism to:

- allow threads to wait on a condition
- (Hopefully) Allow a thread satisfies the condition to notify all waiting threads

### Producer consumer problem

Build a **blocking queue**, such that:

- when the queue is empty, consumer will wait until produce provide one element
- when the queue is full, producer will wait until consumer release one element

Both operations happens in a mutual exclusive fashion so that all operations are ordered.

- Mutual exclusive -> use locks
- Wait -> condition synchronization

What is **Monitor**?

- There are two queues controlling the access to enter the room.
- lock queue, there is only one thread at a time from the queue can enter
- wait queue, there is a queue for the condition provided, all the thread wait(), is in the queue, and wait for the notify() call to remove from the condition queue.

**BlockingQueue Realization Using Wait NotifyAll**

```java
class Q {
    private Queue<Integer> q;
    private final int limit;
    public Q(int limit) {
        this.q = new LinkedList<>();
        this.limit = limit;
    }
    
    public synchronized void put(Integer ele) {
        while (q.size() == limit) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        if (q.size() == 0) { // Comsumer wait under only on circumstance that the queue is empty.
            notifyAll();
        }
        q.offer(ele);
    }
    
    public synchronized Integer take() {
        while (q.size() == 0) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrack();
            }
        }
        if (q.size() == limit) {
            notifyAll();
        }
        return q.poll();
    }
}

```

