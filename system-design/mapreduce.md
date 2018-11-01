<extoc></extoc>

# MapReduce

Computation:

1. Batch processing
    - log analysis, web page analysis
    - processing all stored data, which may be of large scale
    - new information arriving in the meantime is not processed
2. Stream processing
    - continuously receives data that is under constant change
    - real-time monitoring: capture and analyze data issued by various sources such as sensors, news feeds, click on Web pages, etc

A classic Batch Processing model: **MapReduce**

MapReduce is a programming model and an associated implementation for processing and generating large data sets with a parallel, distributed algorithm on a cluster

## Example 1: Word Count

text file, words separated by space

- 数据量不大的情况：
    - HashMap or sorting
- Input非常大, Eg., Terabytes？
    - 可能出现的单词有范围？
    - 如果单词没有范围（不一定是正确的英文单词）Eg. aaa, 111, 12ab

- **Map**
    - Multiple machines, counting in parallel
    - M1: Apple-1, Mango-1
    - M2: Plum-1, Orange-1
    - M3: Apple-2, Plum-1
    - Map tasks scheduled so HDFS/GFS input block replica are on same machine or same rack
- **Shuffle**
    - shuffle intermediate results
    - move Map outputs to the reducers
    - shuffle rule for word count: hash
    - A different subset of the intermediate key space is assigned to each reduce node
- **Reduce**


## Example 2: Terasort

How to quickly sort 1TB data?

Solution 1

- 把原有的数据分布到多个节点上分别排序，最后Merge Sort
- Bottle Neck: 归并排序，最后单独一个reducer需要处理所有数据

Solution 2

- 把数据分成R个数据块，根据首字母划分
    - 只要保证第i块所有数据都比第i+1块所有数据要小
- 各个mapper分别排序
- Shuffle based on partitions
- 最终R个reducer分别聚合

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

