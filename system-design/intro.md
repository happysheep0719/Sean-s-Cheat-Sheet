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
- Hashtable DHT Consistent Hashing
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

    - Write back
 
## Distributed File System
## Design a URL shortened system