# Hashmap 实现
存储方式：array+linkedlist（用来避免碰撞）
存储分配：hashcode函数。Java1.8的hashmap的hashcode：(h = k.hashCode()) ^ (h >>> 16)
扩容问题：容量、负载因子。用capacity*load factor作为新容量。然后rehash
工作方式：通过hash方法，通过put和get存储和获取对象。通过K/V对决定存储的位置。