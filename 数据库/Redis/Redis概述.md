
# Redis概述

- 基于内存，速度快
- key-value模型，因为通常用作缓存，数据不完整难以形成关系型
- worker单线程，io操作多线程
- 连接多(连接池)，NIO多路复用，epoll
- value五种数据类型-->本地方法：计算向数据移动，IO优化(相比Memcached优化)
- 串行化/原子


## 数据类型

### String

- 字符串操作
    - APPEND，STRLEN 字节长度
    - 场景：session，kv缓存，数值计算计数器，小文件
- 数值计算
- 二进制位
    - bitmap
    - 场景：统计用户登录次数，统计活跃用户人数


### List

- 双向链表
- key指向头和尾
- 同向操作 lpush lpop --> 栈<br>
  异向操作 --> 队列<br>
  index() --> 数组
- 场景：评论列表，消息队列，替代java容器 

### Hash

- value是一个hashmap
- 场景：聚集数据，详情页，用户详情

### Set

- 集合：无序，不重复
- 场景：一个集合：抽奖，验证码，扑克牌游戏；两个集合交并集：共同好友，好友推荐

### Sorted set (zset)

- 有序集合，带score
- 场景：排行榜


## 线程模型

- worker单线程


## 使用场景

