---
title: Redis（缓存）
date: 2022-05-20 21:58:10
tags:
    Redis,缓存
categories:
    Redis
---

# Redis（缓存）

## Redis认知

**REmote DIctionary Server** 远程字典服务器  ——  C语言写的

- 字典 —— 基于内存存储，速度快
- 服务器 —— 开放网络，支持增删改查
- 远程 —— 分布式的特征
- 同时涉及多种数据结构， 满足不同的应用场景
- 同时单线程模型的设计（非6.x），原子性操作，线程安全



## 开始Redis

下载地址：https://www.redis.com.cn/

Redis 是Linux下的开源软件 —— 目前最新版本6.2.x —— 不推荐windows使用，但是微软有推出 最高版本 3.2



**Redis - Sever** —— SQL Server

**Redis - CLI** —— 命令行工具

**Command** —— SQL语句

**RedisDesktiopManager** —— SQL Server ManagerStudio



## .NET6对接Redis

1. **ServiceStack.Redis**：收费的 （可破解）（limit 3600 request per hour）
2. **StackExchange.Redis**：免费的-ASP.NET Core 默认的分布式Session用的就是这个
3. **CSRedisCore**：社区很喜欢的

都是些简单封装：链接管理，命令翻译



## Redis原子性操作

**如：**Append  GetAndSetValue  Lncr  Decr

都是Redis命令，不是类库故意封装的

**原子性操作，为了线程安全**

**如：**Append的效果是直接给某个Key的值加长一断，返回加长后的结果——这个是线程安全；等同于限度出来，然后拼接值，然后写入——这个是线程不安全的；

因为Redis是单线程—任何命令都是原子性的（一次性完成）—— 所以Append是一定会成功，拼接然后返回结果，读取和拼接之间是**不会**有其他操作，因为**Redis只有一个线程**

程序先Get，在拼接，再Set，这个时间差里面，可能 有别的客户端把值给修改了，然后这里Set就覆盖了其他客户端的操作——Redis只有一个线程，但是**能响应多个客户端**



## Redis防超卖

### **Redis—String特性：**

- **快速存取；**
- **支持原子性操作；**
- **自增自减；**



**举例：**

**数据库：**

十个商品，5000个人并发抢，先查找——加锁——检测库存——有——创建订单——减库存——释放锁——5000线程；数据库崩溃超时；

解决方案：用Redis来做库存管理——负责做检测和减库存——线程安全

对应项目：Redis1

## Redis数据结构

**五大结构**？八大结构？九大结构

1. **String**
2. **List**
3. **Hash**
4. **Set**
5. **ZSet(Sorted Seet)**
6. Bitmap
7. GEOhash
8. Hyperloglog
9. Streams

![image-20220926112511856](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220926112511856.png)

### **String如何存储**

Redis——RemoteDictionary Server—— Redis本身其实就是个Map（字典）

String是最简单的存储单个value即可，其实就是个SDS动态字符串



C#里面，String字符串是不变的，不变性

Redis里面，Redis新类型**SDS动态字符串**——动态变长



#### SDS动态字符串

```c#
//数据结构  
struct sdshdr {
	//记录bug数组中已使用字符的数量，等于SDS保存字符串的长度
	int len;
	//记录bug数组中未使用的字符数量
	int free;
	//字符数组，用于保存字符串
	char buf[]
}
Redis string 将字符串存储到字符类型的bug[]中，并使用len、free对buf[]数组的长度和未使用的字符数进行描述
//默认分配是512byte——为了后面能扩容
```

![image-20220926105401378](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220926105401378.png)



#### 字符串扩容策略

1. **默认**分配是521Byte
2. 当字符串所占空间小于1MB时，Redis对字符串存储空间的扩容是以**成倍**的方式增加的
3. 而当所占空间**超过1MB**时，每次扩容只增加1MB
4. Redis字符串允许**最大值**字节数是512MB



#### 对象存取需求

String类型是最常见最容易理解的类型，很多快速存取的需求都可以完成。

**Redis保存一个用户对象信息，如何快速实现**：

1. **序列化成Json保存：**读取很方便，但是制度一个属性就比较麻烦-->读取+反序列化 ———— 修改一个属性的值-读取-反序列化+修改+序列化保存
2.  **按属性来存String：**读取一个属性方便 --- 修改单个属性方便 --- 缺陷就是key多，整体读取麻烦



两全其美的方式 --- **String不行** 只有这两种方式



### **Hash散列类型**

**Hash**散列类型是更好的保存方式，是Rides常用数据结构；

1. 能快速获取单个属性值：key--field
2. 能快速更新单个属性值：key--field
3. 也能快速获取全部属性：全部的key 全部的value 全部的key--value

通常：String存单个字符串  Hash存对象

**相比较而言：**

String更适合

Hash更适合

#### Hash底层结构

Hash 类型是Redis 常用数据类型之一1，其底层存储结构油两种实现方式：

1. 当存储的数量较少时，Hash 采用ziplist 作为底层存储结构，此时要求符合一下两个条件（ziplist是个双向链表，紧密拜访-压缩的-很节约空间）
   - 哈希对象保存的所有键值对（键和值）的字符串长度总和小于64个字节。
   - 哈希对象保存的键值对数量要小于512个。
2. 当无法满足上述条件时，Hash 就会采用第二种方式来存储，也就是 dict（字典结构）底层是数组和链表相结合的方式存储数据。查找性能非常高效，其时间复杂度未O(1)。

![image-20220926163655531](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220926163655531.png)

#### Hash命令

| 命令                                                         | 说明                                              |
| ------------------------------------------------------------ | ------------------------------------------------- |
| HDEL  key  Field [field ...]                                 | 用于删除一个或多个哈希表字段                      |
| HEXISTS  key field                                           | 用于确认哈希表字段是否存在                        |
| HGET  key  field                                             | 获取key关联的哈希字段的值                         |
| HGETALL  key                                                 | 获取key关联的所有哈希字段值                       |
| HINCRBY  key  field  increment                               | 给key关联的哈希字段做整数增量运算                 |
| HINCRBYFLOAT  key  field  increment                          | 给key关联的哈希字段做浮点数增量运算               |
| HKEYS  key                                                   | 获取key关联的所有字段和值                         |
| HLEN  key                                                    | 获取key中的哈希表的字段数量                       |
| HMSET  key  field  value  [filed value ...]                  | 再哈希表中同时设置多个 field-value （字段-值）    |
| HMGET  key  field1  [field2]                                 | 用于同时获取多个给哈希字段（field）对应的值       |
| HSET  key field value                                        | 用于重置指定key的哈希表字段和值（field/value）    |
| HSETNX  key  field  value                                    | 仅当字段field不存在时，设置哈希表字段的值         |
| HVALS  key                                                   | 用于获取哈希表中的所有值                          |
| HSCAN  key  cursor                                           | 迭代哈希表中的所有键值对，cursor标识游标，默认为0 |
| ![image-20220926115326269](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220926115326269.png) |                                                   |

对应项目：Redis2



### **Set结构**

**Set**是一个**无序**的、**自动去重**的**集合**数据类型，Set底层用两种数据结构存储，一个是hashtable，一个是inset。

满足两个条件，就用**Inset**（就是个数组）：

1. 元素个数不少于默认值521
2. 元素可以用整形表示（值必须是整形）

一般使用的**Hashtable**如图：

![image-20220926164732830](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220926164732830.png)

#### Set命令

| 命令                                           | 说明                                                   |
| ---------------------------------------------- | ------------------------------------------------------ |
| SADD key member [member ...]                   | 向集合中添加一个或多个元素，并且自动去重。             |
| SCARD key                                      | 返回集合中元素的个数                                   |
| SDIFF key [key ...]                            | 求两个或多个集合的差集                                 |
| SDIFFSTORE destination key [key ...]           | 求两个集合或多个集合的差集，并将结果保存到指定的集合中 |
| SINTER key [key]                               | 求两个或多个集合的交集。                               |
| SINTERSTORE destination key [key ...]          | 求两个或多个集合的交集,并将结果保存到指定的集合中。    |
| SISMEMBER key member                           | 查看指定元素是否存在于集合中。                         |
| SMEMBERS key                                   | 查看集合中所有元素。                                   |
| SMOVE source destination member                | 将集合中的元素移动到指定的集合中。                     |
| SPOP key                                       | 弹出指定数量的元素。                                   |
| SRANDMEMBER key [count]                        | 随机从集合中返回指定数量的元素，默认返回1个。          |
| SREM key member [member ...]                   | 删除一个或者多个元素，若元素不存在则自动忽略。         |
| SUNION key [key ...]                           | 求两个或者多个集合的并集。                             |
| SUNIONSTORE destination key [key ...]          | 求两个或者多个集合的并集,并将结果保存到指定的集合中。  |
| SSCAN key cursor [MATCH pattern] [COUNT count] | 该命令用来迭代的集合中的元素。                         |
|                                                |                                                        |

通过命令操作，写入读取删除和其他操作就是个数据容器具备了无序去重



#### Set特点

- Set是无序的 --- 可以随便放入任意数据，然后数据读取时没有顺序
  1. 抽奖 --- 随机
  2. 听课 --- 随机播放
- Set去重 ---- 集合里面写入数据不会出现重复的
  1. 朋友圈点赞 --- 不能点两次
  2. PV --- PageeView    UV --- UnitView    IP --- IPAddress



### **ZSet**

ZSet为有序（有限score排序，score相同则元素字典序），自动去重的集合数据类型，其底层实现为字典（dict）+ 跳表（skiplist），当数据比较少的时候用ziplist编码结构存储。也叫Sorted-Set

满足一下两个条件采用ziplist存储：

1. 有序结合保存的元素数量小于默认值128个
2. 有序集合保存的所有元素的长度小于默认值64字节



#### ZSet复杂结构

当有序结合不满足使用压缩列表的条件时，就会使用skipList结构来存储数据、。

跳跃列表（skipList）又称"跳表"是一种基于链表实现的随机化数据结构，其插入、删除、查找的时间复杂度均为O(logN)

![image-20220927104804824](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220927104804824.png)

![image-20220927105246008](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220927105246008.png)



#### ZSet命令

ZSet  key --- field --- Score分数，比Set多了个Score

![image-20220927111903486](https://gitee.com/be_lieve_oneself/demo1/raw/master/image-20220927111903486.png)