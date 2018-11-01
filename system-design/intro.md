# System Design

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
  - **ACID** (Atomicity, Consistency, Isolation, Durability)
    - Atomicity
    - Consistency
    - Isolation
    - Durability
  - **CAP theorem**
    - CAP Theorem is a concept that a distributed database system can only have 2 of the 3: Consistency, Availability and Partition Tolerance.
    - Consistency
    - Availability
    - Partition Tolerance
      - tolerance for failures
  - sharding
- Synchronous/Asynchronous call
  - Synchronous call will wait until response come back
  - Asynchronous call will make the call, do something else and handle message when callback happens
 
## Distributed File System
## Design a URL shortened system
## Design a Web Crawler


