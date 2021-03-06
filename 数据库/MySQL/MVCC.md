# MVCC

**Multiple Version Concurrent Control 多版本并发控制**

针对并发事务过程中存在的问题，即脏读、不可重复读、幻读等，需要数据库提供事务隔离机制来避免。实现隔离机制的方式主要有两种：

1. 加读写锁
2. 一致性快照读，即 MVCC

但基于提升并发性能的考虑，通常使用 MVCC 较多。

MVCC 本质上是行级锁的一个变种，但是它在大多数情况下避免了加锁操作，因此开销更低。

MVCC 是通过保存数据在某个时间点的快照来实现，也就是说不管需要执行多长时间，每个事务看到的数据都是一致的。根据事务开始时间的不同，每个事务对同一张表，同一时刻看到的数据可能是不一样的。

不同存储引擎的MVCC实现不同，典型的有乐观并发控制和悲观并发控制。



## InnoDB 的MVCC

InnoDB的MVCC，通过在每行记录后面保存两个隐藏的列来实现，分别是 DATA_TRX_ID 和 DATA_ROLL_PTR

DATA_TRX_ID：

- 记录最近更新这条行记录的事务 ID，大小为 6 个字节

DATA_ROLL_PTR：

- 表示指向该行回滚段（rollback segment）的指针，大小为 7 个字节，InnoDB 便是通过这个指针找到之前版本的数据。该行记录上所有旧版本，在 undo 中都通过链表的形式组织。

