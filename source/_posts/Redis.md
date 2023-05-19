---
title: Redis
date: 2022-05-20 21:58:10
tags:
    Redis
categories:
    Redis
---

# Redis

- REmote Dictionary Server  远程字典服务
  1. 方便扩展
  2. 大数据量高性能
  3. 数据类型的多样性
  4. 分布式存储



## Redis多种数据类型

1. **String  字符串**
2. **Hash  哈希**
3. **List  集合**
4. **Set  去重集合**
5. **Zset  有序的去重集合**
6. BitMaps
7. HyperLogLoss
8. Streams



## 本地缓存与分布式缓存的区别

**本地缓存：**

- 本地缓存是应用和缓存在同一个进程内部

- **优点：**请求缓存比较快速，没有过多的网络开销

- **缺点：**

  与应用耦合度非常高，多个应用程序无法共享缓存，各个节点需要维护各自的缓存，比较浪费缓存；

  数据随应用进程的重启而丢失；

  集群的数据更新问题；

- **适用场景**
  所以本地缓存一般适合于缓存只读数据，如统计类数据。或者每个部署节点独立的数据，如长连接服务中，每个部署节点由于都是维护了不同的连接，每个连接的数据都是独立的，并且随着连接的断开而删除。如果数据在集群的不同部署节点需要共享和保持一致，则需要使用分布式缓存来统一存储，实现应用集群的所有应用进程都在该统一的分布式缓存中进行数据存取即可

**分布式缓存：**

- 分布式缓存是要给独立的应用，与本地应用隔离

- **优点：**

  支持大数据量存储，不受应用进程重启影响；

  数据集中存储，保证数据一致性；

  数据读写分离，高性能，高可用；

  

- **缺点：**

  数据跨网络传输，性能低于本地缓存



## 分布式缓存对比

|  分布式缓存  |                            Redis                             |                Memcache                |
| :----------: | :----------------------------------------------------------: | :------------------------------------: |
|   数据结构   |  String、Hash、List、Set、ZsetString、Hash、List、set、Zset  |               Key/value                |
|    持久化    |                           RDB、AOF                           | 无持久化，需要依赖第三方组件MemcacheDB |
|   线程模型   |                  单线程，Redis6.0以后多线程                  |                 多线程                 |
|   存储结构   |  简单动态字符串、双向链表、压缩列表、哈希表、跳表、整数数组  |                  Slab                  |
|    高可用    |                 主从复制、Sentinel、Cluster                  |           第三方组件Memagent           |
|   队列支持   |                             支持                             |       不支持，使用MemcacheQ实现        |
| 数据淘汰策略 | maxmemory、maxmemory-policy、volatile-lru、alkeys-lru、volatile-random、allkeys-random、volatile-ttl、noeviction(trturn error) |                  LRU                   |
|              |                                                              |                                        |



## Redis数据结构类型以及使用场景

![image-20220921105600406](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220921105600406.png)



![image-20220921105934474](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220921105934474.png)

![image-20220920112025484](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220920112025484.png)





## Redis与数据库双写一致性问题

- 先更新缓存，在更新数据库
- 先更新数据库，在更新缓存
- 先删除缓存，在更新数据库

![image-20220922101341063](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220922101341063.png)

- 先更新数据库，在删除缓存（最常用）

![image-20220922101412171](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220922101412171.png)



## Redis的过期策略

- 定时删除是集中处理
- 惰性删除是零散处理

#### 贪心策略

- 从过期的字典中随机20个key
- 删除这20个key中已经过期的key
- 如果过期的key比率超过4/1（循环这个过程）

![image-20220922103022795](D:\lei.zhang\AppData\Roaming\Typora\typora-user-images\image-20220922103022795.png)



## 如何解决缓存的三大问题

### 缓存穿透

![image-20220922103341845](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220922103341845.png)

### 缓存击穿

- 大量请求同时查询一个Key，而这个Key刚好失效，导致大量请求到数据库中



### 缓存雪崩

- 后端系统压力太大造成数据库后端故障成为服务器雪崩



## Redis集群概述

![image-20220922104505067](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220922104505067.png)

#### 什么是集群

- 集群是一组机器，也就是若干台机器，这些机器共同完成一件事情



#### 集群的特点

- 可扩展性：集群的性能不限制于u单一的服务实体，新的服务实体可以动态的添加到集群，从而增强集群的性能。
- 高可用性：当集群中某一个节点发生故障时集群节点上面所运行的应用程序将在另一台节点呗自动接管，消除单点故障对于增强数据可用性、可达性和可靠性是非常重要的



## 集群与分布式的区别

![image-20220922105538212](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220922105538212.png)

分布式干的活不一样

![image-20220922105602565](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220922105602565.png)

集群干的活一样





## Redis集群搭建

### Redis—Cluster

