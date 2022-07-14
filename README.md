---
description: 注意
---

# notice

### 禁用

* KEYS
* FLUSHALL
* FLUSHDB

### 慎用

慎用全量操作命令，比如Hash类型的HGETALL、Set类型的SMEMBERS等，这些操作会对Hash和Set的底层数据结构进行全量扫描，如果数据量较多的话，会阻塞Redis主线程。

* HGETALL
* SMEMBERS
* MONITOR

### 缓存技巧

* key的命名要尽量易读，即见名知意，在易读的前提下长度要尽可能的小，以减少资源的占用，对于value来说可以用int就尽量不要用string，对于小于N的value，redis内部有shared\_object缓存。
* 在redis使用hash的情况下进行key的拆分，同一个hash key会落到同一个redis节点，hash过大的情况下会导致内存以及请求分布的不均匀，考虑对hash进行拆分为小的hash，使得节点内存均匀避免单节点请求热点。
* 为了避免不存在的数据请求，导致每次请求都缓存miss直接打到数据库中，进行空缓存的设置。
* 缓存中需要存对象的时候，序列化尽量使用protobuf，尽可能减少数据大小。
* 新增数据的时候要保证缓存务必存在的情况下再去操作新增，使用Expire来判断缓存是否存在。
* 对于存储每日登录场景的需求，可以使用BITSET，为了避免单个BITSET过大或者热点，可以进行sharding。
* 使用sorted set的时候，避免使用zrange或者zrevrange返回过大的集合，复杂度较高。
* 在进行缓存操作的时候尽量使用PIPELINE，但也要注意避免集合过大。
* 避免超大的value。
* 缓存尽量要设置过期时间。
