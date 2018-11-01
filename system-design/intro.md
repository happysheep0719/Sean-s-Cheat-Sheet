****# System Design

System/Solution/Product Design

Eg.
 
- Design a Twitter?
- Design a Uber?
- Design a short URL service.

Product -> functionalities/use cases -> Architecture

## Common patterns

- typical way to dispatch job to multiple workers
  - MapReduce, WebCrawler, etc. Partition
  - Batching - grouping things together
- Hashtable / Distributed Hash Table / Consistent Hashing
  - Consistent hashing is a special kind of hashing such that when a hash table is resized, only K/n keys need to be remapped on average.
    - K is the number of keys
    - n is the number of slots
- Push/Pull model
- Typical ways to handle failures
  - Server Failover - master/slave
  - Data durability - replication
- Cache
  - different ways of cache
    - Write through
      - When writing, data is confirmed written after being written cache and memory
      - large writing latency
      - consistent cache and memory
      - good for writing and re-loading frequently
    - Write around
      - When writing, data is confirmed written after being written only memory
      - good for not re-loading subsequently
      - cache-miss will happen if reading
    - Write back
      - When writing, data is confirmed written after being written only cache
      - low latency
      - data availability risk because the cache could fail 
      - good for best performer
- Database
  - DBMS guarantees the **ACID** (Atomicity, Consistency, Isolation, Durability) of database transactions.
    - **Atomicity**
      - Transactions are often composed of multiple statements. Atomicity guarantees that each transaction is treated as a single "unit", which either succeeds completely, or fails completely: if any of the statements constituting a transaction fails to complete, the entire transaction fails and the database is left unchanged. An atomic system must guarantee atomicity in each and every situation, including power failures, errors and crashes.
    - **Consistency**
      - Consistency ensures that a transaction can only bring the database from one valid state to another, maintaining database invariants: any data written to the database must be valid according to all defined rules, including constraints, cascades, triggers, and any combination thereof. This prevents database corruption by an illegal transaction, but does not guarantee that a transaction is correct.
      - For example, A's money + B's money = 2000
    - **Isolation**
      - Transactions are often executed concurrently (e.g., reading and writing to multiple tables at the same time). Isolation ensures that concurrent execution of transactions leaves the database in the same state that would have been obtained if the transactions were executed sequentially. Isolation is the main goal of concurrency control; depending on the method used, the effects of an incomplete transaction might not even be visible to other transactions.
    - **Durability**
      - Durability guarantees that once a transaction has been committed, it will remain committed even in the case of a system failure (e.g., power outage or crash). This usually means that completed transactions (or their effects) are recorded in non-volatile memory.
  - **CAP theorem**
    - [Reference 1](http://www.hollischuang.com/archives/666)
    - [Reference 2](https://towardsdatascience.com/cap-theorem-and-distributed-database-management-systems-5c2be977950e)
    - [!](http://www.hollischuang.com/wp-content/uploads/2015/12/Teorema-CAP-2.png)
    - CAP Theorem is a concept that a distributed database system can only have 2 of the 3: Consistency, Availability and Partition Tolerance.
    - **Consistency**
      - all nodes see the same data at the same time
    - **Availability**
      - Reads and writes always succeed. / Every request gets a response on success/failure.
      - Achieving availability in a distributed system requires that the system remains operational 100% of the time. Every client gets a response, regardless of the state of any individual node in the system.
      - no timeout
    - **Partition Tolerance**
      - the system continues to operate (run) despite arbitrary message loss or failure of part of the system
      - A system that is partition-tolerant can sustain any amount of network failure that doesn’t result in a failure of the entire network. Data records are sufficiently replicated across combinations of nodes and networks to keep the system up through intermittent outages. 
  - sharding
- Synchronous/Asynchronous call
  - Synchronous call will wait until response come back
  - Asynchronous call will make the call, do something else and handle message when callback happens
 
## Distributed File System
## Design a URL shortened system
## Design a Web Crawler


