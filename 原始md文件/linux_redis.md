### 1、redis是什么 ###

redis是一种支持Key-Value等多种数据结构的存储系统。可用于缓存，事件发布或订阅，高速队列等场景。该数据库使用ANSI C语言编写，支持网络，提供字符串，哈希，列表，队列，集合结构直接存取，基于内存，可持久化。

### 2、redis的应用场景 ###

1）会话缓存（最常用）  
2）消息队列，比如支付  
3）活动排行榜或计数  
4）发布，订阅消息（消息通知）  
5）商品列表，评论列表等

### 3、redis数据类型 ###

redis一共支持五种数据结构：string（字符串），hash（哈希），list（列表），set（集合）和zset（sorted set有序集合）。

#### 0）redis常用命令 ####
启动redis服务：

	cd /home/rong/redis/bin
	./redis-cli

停止redis服务（或exit）：

	./redis-cli shutdown

检测redis服务是否启动：

	PING

查看键数据结构：

	type key（键）

查看所有队列：
	
	keys *

删除某一键：

	del key（键）

清除所有队列：

	flushall

#### 1）string（字符串） ####

它是redis的最基本的数据类型，一个键对应一个值，需要注意是一个键值最大存储512MB。

    127.0.0.1:6379> set key "hello world"
    OK
    127.0.0.1:6379> get key
    "hello world"
    127.0.0.1:6379> getset key "nihao"
    "hello world"
    127.0.0.1:6379> mset key1 "hi" key2 "nihao" key3 "hello"
    OK
    127.0.0.1:6379> get key1
    "hi"
    127.0.0.1:6379> get key2
    "nihao"
    127.0.0.1:6379> get key3
    "hello"

#### 2）hash（哈希） ####

redis hash是一个键值对的集合，是一个string类型的field和value的映射表，适合用于存储对象

    127.0.0.1:6379> hset redishash 1 "001"
    (integer) 1
    127.0.0.1:6379> hget redishash 1
    "001"
    127.0.0.1:6379> hmset redishash 1 "001" 2 "002"
    OK
    127.0.0.1:6379> hget redishash 1
    "001"
    127.0.0.1:6379> hget redishash 2
    "002"
    127.0.0.1:6379> hmget redishash 1 2
    1) "001"
    2) "002"

#### 3）list（列表） ####

是redis的简单的字符串列表，它按插入顺序排序

    127.0.0.1:6379> lpush word hi
    (integer) 1
    127.0.0.1:6379> lpush word hello
    (integer) 2
    127.0.0.1:6379> rpush word world
    (integer) 3
    127.0.0.1:6379> lrange word 0 2
    1) "hello"
    2) "hi"
    3) "world"
    127.0.0.1:6379> llen word
    (integer) 3

#### 4）set（集合） ####

是字符串类型的无序集合，也不可重复

    127.0.0.1:6379> sadd redis redisset
    (integer) 1
    127.0.0.1:6379> sadd redis redisset1
    (integer) 1
    127.0.0.1:6379> sadd redis redisset2
    (integer) 1
    127.0.0.1:6379> smembers redis
    1) "redisset"
    2) "redisset2"
    3) "redisset1"
    127.0.0.1:6379> sadd redis redisset2
    (integer) 0
    127.0.0.1:6379> smembers redis
    1) "redisset"
    2) "redisset2"
    3) "redisset1"
    127.0.0.1:6379> sadd redis redisset3
    (integer) 1
    127.0.0.1:6379> smembers redis
    1) "redisset3"
    2) "redisset"
    3) "redisset2"
    4) "redisset1"
    127.0.0.1:6379> srem redis redisset
    (integer) 1
    127.0.0.1:6379> smembers redis
    1) "redisset3"
    2) "redisset2"
    3) "redisset1"

#### 5）zset（sorted set有序集合） ####

是string类型的有序集合，也不可重复  
有序集合中的每个元素都需要指定一个分数，根据分数对元素进行升序排序，如果多个元素有相同的分数，则以字典序进行升序排序，sorted set因此非常适合实现排名

    127.0.0.1:6379> zadd nosql 0 001
    (integer) 1
    127.0.0.1:6379> zadd nosql 0 002
    (integer) 1
    127.0.0.1:6379> zadd nosql 0 003
    (integer) 1
    127.0.0.1:6379> zcount nosql 0 0
    (integer) 3
    127.0.0.1:6379> zcount nosql 0 3
    (integer) 3
    127.0.0.1:6379> zrem nosql 002
    (integer) 1
    127.0.0.1:6379> zcount nosql 0 3
    (integer) 2
    127.0.0.1:6379> zscore nosql 003
    "0"
    127.0.0.1:6379> zrangebyscore nosql 0 10
    1) "001"
    2) "003"
    127.0.0.1:6379> zadd nosql 1 003
    (integer) 0
    127.0.0.1:6379> zadd nosql 1 004
    (integer) 1
    127.0.0.1:6379> zrangebyscore nosql 0 10
    1) "001"
    2) "003"
    3) "004"
    127.0.0.1:6379> zadd nosql 3 005
    (integer) 1
    127.0.0.1:6379> zadd nosql 2 006
    (integer) 1
    127.0.0.1:6379> zrangebyscore nosql 0 10
    1) "001"
    2) "003"
    3) "004"
    4) "006"
    5) "005"

### 4、服务相关的命令 ###

    select		＃选择数据库（数据库编号0-15）
    exit		＃退出连接
    info		＃获得服务的信息与统计
    monitor		＃实时监控
    config get	＃获得服务配置
    flushdb		＃删除当前选择的数据库中的key
    flushall	＃删除所有数据库中的键

### 5、redis的发布与订阅 ###

redis的发布与订阅（发布/订阅）是它的一种消息通信模式，一方发送信息，一方接收信息。
下图是三个客户端同时订阅同一个频道

![](https://ediakam.github.io/image/redis_1.png)

下图是有新信息发送给频道1时，就会将消息发送给订阅它的三个客户端

![](https://ediakam.github.io/image/redis_2.png)

### 6、redis的持久化 ###

redis持久有两种方式：快照（快照），仅附加文件（AOF）

**快照（快照）**

1）将存储在内存的数据以快照的方式写入二进制文件中，如默认dump.rdb中  
2）保存900 1  
＃900秒内如果超过1个Key被修改，则启动快照保存  
3）保存300 10  
＃300秒内如果超过10个Key被修改，则启动快照保存  
4）保存60 10000  
＃60秒内如果超过10000个重点被修改，则启动快照保存  

**仅附加文件（AOF）**

1）使用AOF持久时，服务会将每个收到的写命令通过写函数追加到文件中（appendonly.aof）  
2）AOF持久化存储方式参数说明  
appendonly yes   
＃开启AOF持久化存储方式  
appendfsync always  
＃收到写命令后就立即写入磁盘，效率最差，效果最好  
appendfsync everysec  
＃每秒写入磁盘一次，效率与效果居中  
appendfsync no  
＃完全依赖操作系统，效率最佳，效果没法保证  

redis常用数据结构：[https://blog.csdn.net/middleware2018/article/details/80355418](https://blog.csdn.net/middleware2018/article/details/80355418)

redis命令参考：[http://doc.redisfans.com/index.html](http://doc.redisfans.com/index.html)