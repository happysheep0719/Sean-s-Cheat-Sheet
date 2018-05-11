<extoc></extoc>

# Database

**Sharding and Replication**

**Consistency and Availability**

## SQL vs. NoSQL

So, here comes the first main difference between traditional SQL and NoSQL: do you want to maintain **consistency** between all nodes, or you want to make response quickly to your client, or you want to achieve both.

- For traditional SQL(MySQL), it chooses **consistency** over availability.
- For NoSQL(MongoDB), it chooses **availability** over consistency.

**CAP Theorem** - it is impossible for a distributed data store to simultaneously provide more than two out of the following three guarantees
- **Consistency**
    - Every read receives the most recent write or an error
- **Availability**
    - Every request receives a (non-error) response – without guarantee that it contains the most recent write
- **Partition tolerance**
    - The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes


## MySQL

## MongoDB
