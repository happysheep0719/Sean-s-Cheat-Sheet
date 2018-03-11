# Hashmap 实现
存储方式：array+linkedlist（用来避免碰撞）
存储分配：hashcode函数
扩容问题：容量、负载因子。用capacity*load factor作为新容量。然后rehash
