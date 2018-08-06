<extoc></extoc>

# System Design

System/Solution/Product Design

Eg.
 
- Design a Twitter?
- Design a Uber?
- Design a short URL service.

Product -> functionalities/use cases -> Architecture

## Distributed File System (HDFS)

- Data Center
    - Cluster
        - (Rack)
            - Node/Server

Communication inside Rack is cheap, compared to that between nodes in different racks.


Example: [Hadoop Distributed File System](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html)

Basic use case: **Commodity hardware**

- **Metadata** are put in the same machine, that is, **Namenode / Master Node**
    - The size of total metadata is not very large.
- **Data** are stored in **Data Nodes / Slave Nodes**

[!HDFS Architecture](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/images/hdfsarchitecture.png)

**How a file is stored?**

- Files are divided into fixed-size blocks, like 128MB.
- Block are replicated.

![FileBlock](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/images/hdfsdatanodes.png)

**How to locate these blocks?**

- NN stores the mapping of blocks to datanodes.
- NN tracks the location of new blocks
- NN monitors the health of datanodes (by sending **heartbeat** from datanodes to namenodes)


Eg. Read one random file

- get block address (which datanode) -> read from different datanodes
- block-datanodes mapping: file -> tree mapping(filepath to blocks) -> mapping(blocks to datanodes) -> datanodes

### Data durability

- 3 replicas
    - 1st replica on local node, local rack or random node
    - 2nd, 3rd replicas are on the same remote rack

- replica consistency
    - maintained using version number

### thoughput vs. latency

吞吐量 vs. 延迟

## Distrbuted Computing

- Batch Processing
    - Eg. log analysis, web page analysis
- Stream Processing
    - Eg. real-time monitoring

### MapReduce - a classic batch processing model

Map -> Shuffle -> Reduce

#### Eg1. Word count

In reduce stage, reduce the count of each word.

**How to partition the words in shuffle stage?
**
- Hash Partition

Data locality: move computation to data

#### Eg2. Terasort (String)

**Merge sort**

How to determine the range of each map task data?

- Sampling
- use sampled data to sort in advance, then use the sorted result to derive the ranges
- use the ranges to construct a trie tree

How to determine the bucket id of each word?

- use trie tree (prefix tree)

#### Eg3. Two-Sum

**Solution** - use hash

assume A + B = target

if A <= target / 2: hashcode = A
else if A > target / 2: hashcode = target - A

The shuffle stage can move solution pairs to same reducers.


#### Eg4. Inverted Index

We have a bunch of sentences and we want to get the indexes of sentences in which the words appear.

#### Eg5. Group Anagrams

Sorted words first
->
shuffle to same reducer

## 