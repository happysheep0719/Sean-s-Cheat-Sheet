<extoc></extoc>


# Distributed File System (HDFS)

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

- Files are divided into fixed-size **blocks**, like 128MB.
    - Why Is a Block in HDFS So Large?

> HDFS blocks are large compared to disk blocks, and the reason is to minimize the cost of seeks. By making a block large enough, the time to transfer the data from the disk can be significantly longer than the time to seek to the start of the block. Thus the time to transfer a large file made of multiple blocks operates at the disk transfer rate.

> A quick calculation shows that if the seek time is around 10 ms and the transfer rate is 100 MB/s, to make the seek time 1% of the transfer time, we need to make the block size around 100 MB. The default is actually 64 MB, although many HDFS installations use 128 MB blocks. This figure will continue to be revised upward as transfer speeds grow with new generations of disk drives.

>This argument shouldn’t be taken too far, however. Map tasks in MapReduce normally operate on one block at a time, so if you have too few tasks (fewer than nodes in the cluster), your jobs will run slower than they could otherwise.

- Blocks are replicated.

![FileBlock](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/images/hdfsdatanodes.png)

**How to locate these blocks?**

- NN stores the mapping of blocks to datanodes.
- NN tracks the location of new blocks
- NN monitors the health of datanodes (by sending **heartbeat** from datanodes to namenodes)


Eg. Read one random file

- get block address (which datanode) -> read from different datanodes
- block-datanodes mapping: file -> tree mapping(filepath to blocks) -> mapping(blocks to datanodes) -> datanodes

### Data durability

Disk, DataNode or Network could fail.

- 3 replicas by default
    - 1st replica on local node, local rack or random node
    - 2nd, 3rd replicas are on the same rack but different data nodes.
    - reliability - tolerate 2 failures
    - good data locality
    - fast block recovery
    
- failure handling
    - detect failure
        - ACK (data receive acknowledgement)
        - Checksum
    - replica consistency
        - maintained using version number

### thoughput vs. latency

吞吐量 vs. 延迟

