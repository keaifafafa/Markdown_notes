##  一、NoSQL简介

### 1.1、为什么要使用NoSQL？

> ==1、单机Mysql时代==

![image-20211120214317631](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211120214325.png)

90年代,一个网站的访问量一般不会太大，单个数据库完全够用。随着用户增多，网站出现以下问题

1. 数据量增加到一定程度，单机数据库就放不下了
2. 数据的索引（B+ Tree）,一个机器内存也存放不下
3. 访问量变大后（读写混合），一台服务器承受不住。

> ==2、Memcached（缓存）+ Mysql + 垂直拆分（读写分离）==

网站80%的情况都是在读，每次都要去查询数据库的话就十分的麻烦！所以说我们希望减轻数据库的压力，我们可以使用缓存来保证效率！

![image-20211120214528890](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211120214529.png)

优化过程经历了以下几个过程：

1. 优化数据库的数据结构和索引(难度大)
2. 文件缓存，通过IO流获取比每次都访问数据库效率略高，但是流量爆炸式增长时候，IO流也承受不了
3. MemCache,当时最热门的技术，通过在数据库和数据库访问层之间加上一层缓存，第一次访问时查询数据库，将结果保存到缓存，后续的查询先检查缓存，若有直接拿去使用，效率显著提升

> ==3、分库分表 + 水平拆分 + Mysql集群==

 ![image-20211120214748163](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211120214748.png)

> ==4、如今最近的年代==

 如今信息量井喷式增长，各种各样的数据出现（用户定位数据，图片数据等），大数据的背景下关系型数据库（RDBMS）无法满足大量数据要求。Nosql数据库就能轻松解决这些问题。

> ==目前一个基本的互联网项目==

 ![image-20211120214954423](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211120214954.png)

> ==为什么要使用NoSQL==

用户的个人信息，社交网络，地理位置。用户自己产生的数据，用户日志等爆发式增长！

这时候我们就需要使用NoSQL数据库，NoSQL可以很好地处理以上的情况

### 1.2、什么是NoSQL？

==NoSQL = Not Only SQL（不仅仅是SQL）==

Not Only Structured Query Language（不仅仅是结构化查询语言）

关系型数据库（如MySql，Oracle等）：表格，行+列，同一个表下数据的结构是一样的。

非关系数据库：数据存储没有固定的格式，并且可以进行横向的扩展。

NoSQL泛指非关系型数据库，随着web2.0互联网的诞生，传统的关系型数据库很难应付web2.0时代！尤其是大规模的高并发的社区，暴露出来很多难以克服的问题，NoSQL在当今大数据环境下发展十分的迅速，Redis是发展最快的。

### 1.3、NoSQL特点？

1. 方便扩展（数据之间没有关系，很好扩展！）

2. 大数据量高性能！（Redis一秒可以写8W次，读11W次，NoSQL的缓存记录级，是一种细颗粒度的缓存，性能会比较高！）

3. 数据类型是多样型的！（不需要实现设计好数据库，随取随用！）

4. 传统的RDBMS 和 NoSQL

   ```bash
   # 传统的 RDBMS(关系数据库)
   - 机构化组织
   - SQL
   - 数据和关系都存在单独的表中 row col
   - 严格的一致性
   - 基础的事务（ACID）
   - ...
   ```

   ```bash
   # NoSQL
   - 不仅仅是数据库
   - 没有固定的查询语言
   - 键值对存储、列存储、文档存储、图形数据库（社交关系）
   - 最终一致性
   - CAP定理 和 BASE
   - 高可用、高性能、高扩展
   - ...
   ```

   > ==了解：3V + 3高==

   大数据时代的3V ：主要是**描述问题**的

   1. 海量Velume
   2. 多样Variety
   3. 实时Velocity

   大数据时代的3高 ： 主要是**对程序的要求**

   1. 高并发

   2. 高可扩

   3. 高性能

      

   **真正在公司中的实践：NoSQL + RDBMS 一起使用才是最强的。**

### 1.4、NoSQL的四大分类

> ==KV键值对==

- 新浪：**Redis**
- 美团：**Redis** + Tair
- 阿里、百度：**Redis** + memecache

> ==文档型数据库（Bosn格式和Json格式）==

- **MongoDB**
  - MongoDB是一个基于分布式文件存储的数据库，C++编写，用来处理大量的文档
  - MongoDB是一个介于关系型数据库和非关系型中间的产品，非关系型数据库中功能最丰富的，最像关系型数据库的
- ConthDB

> ==列存储数据库==

- **HBase**(大数据会用到)
- 分布式文件系统

> ==图形关系数据库==

 ![image-20211122204054985](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211122204055.png)

存储的是关系

- 不是用来存放图形的，是用来存储关系的，朋友圈社交，广告推荐
- **Neo4j**，InfoGrid



 ![image-20211122203926489](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211122203933.png)

## 二、Redis入门

### 2.1、Redis概述

> ==Redis是什么？==

Redis （Remote Dictionary Server），远程字典服务

开源、使用C语言编写，支持网络、基于内存可持久化的日志型，Key-Value数据库，提供多种语言的API，可以用多种语言调用 ，NoSQL技术之一，也被称之为结构化数据库之一

读的速度是11w，写的速度是8w

> ==Redis能干什么？==

- 内存存储，持久化，内存是断电即失的，持久化很重要， 持久化有两种机制（RBD，AOF）
- 效率高，可以用于高速缓存
- 发布订阅系统
- 地图信息分析
- 计数器，（浏览量）
- 。。。

> ==特性==

- 多样的数据类型
- 持久化
- 集群
- 事务
- 。。

> ==常用网站==

- Redis官网 [https://redis.io](https://redis.io/)
- Redis中文网[https://www.redis.net.cn](https://www.redis.net.cn/)

### 2.2、安装Redis（Linux环境下）

>  ==**常用的命令**==

```bash
netstat -lnpt ｜grep 6379
//查看6379=端口占用情况，netstat CentOS不自带，需要另外安装
yum install -y net-tools

kill -9 [PID]
//结束对应PID进程

ln -s /usr/local/redis/bin/redis-cli /usr/bin/redis
//创建链接，使之可以直接使用/bin之中的命令，这创建应该回到～目录进行创建，称为命令软链接

cp /usr/local/redis-5.0.3/redis.conf /usr/local/redis/bin/
//复制操作

make install PREFIX=/usr/local/redis
//安装到指定目录

tar -zxvf redis-5.0.3.tar.gz
//解压

wget http://download.redis.io/releases/redis-5.0.3.tar.gz
//通过链接下载

```

我是直接在宝塔里面安装的

- 首先去应用商店安装

- 去redis安装目录下执行

  ```bash
  cd /www/server/redis/src
  make install
  ```

   ![image-20211122224833290](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211122224833.png)

- 然后启动服务端

  redis-server "配置文件地址"

  ```bash
  redis-server /www/server/redis/src
  ```

- 开启客户端

  ```bash
  redis-cli -p 6379
  ```

- 然后查看redis的进程

  ```bash
  ps -ef|grep redis
  ```

   ![image-20211122225232578](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211122225232.png)

- 关闭redis

  ```bash
  shutdown
  exit
  ```

   ![image-20211122225522299](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211122225522.png)


### 2.3、Redis的压力测试

菜鸟教程：https://www.runoob.com/redis/redis-benchmarks.html

 ![image-20211123164703942](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211123164711.png)

```bash
# 测试 100个并发，100000请求
redis-benchmark -h localhost -p 6379 -c 100 -n 100000
```

### 2.4、基础知识

Redis是单线程的，Redis是基于内存操作的，CPU不是Redis的瓶颈，根据机器的内存和网络带宽的，可以用单线程实现

每秒10w+的QPS，完全不比使用key-value的Memcache差

> ==单线程Redis==

- 误区1，高性能服务器一定是多线程

- 误区2，多线程一定比单线程效率高
  - 多线程要涉及CPU的上下文切换
- 核心：Redis是将所有数据全部放到内存中去操作，效率就是高，CPU上下文切换是耗时的操作，对于系统来说没有上下文切换，系统效率就是最高的，多次读写都是在一个cpu上的，在内存情况下效率就是最高的

## 三、Redis五大基本类型

### 3.1、简介

> ==那五大类型？==

- String
- List
- Set
- Hash
- Zset

>==Redis官方简介==

- Redis是内存中的数据结构存储系统，可以作用数据库、缓存、消息中间MQ
- 支持多种数据类型
- String字符串
- hash散列
- list列表
- set 集合
- sorted sets有序集合
- bimemaps
- hyperloglog
- geospatial
- Redis内置了主从复制replication、LUAscripting脚本，LRU 驱动事件，transactions事务，和不同级别的磁盘持久化persistence
- 通过Redis哨兵Sentinel，和自动分区Cluster，提供高可用性high availability

> ==常用命令==

```bash
keys * # 查询全部key

select 3 # 切换数据库3

dbsize 变量名 # 查看数据库大小

flushdb #  清空当前库

flushall #  清空所有数据

exists 变量名 # 判断某个key是否存在

move 变量名 index # 移动key

expire 变量名 time（seconds） # 设置过期时间，可以用作单点登录

ttl 变量名 # 查看过期时间

type 变量名 # 查看key的类型

config set requirepass XXX # 设置密码

config set requirepass "" # 取消密码

auth xxx # 登录
```

### 3.2、String

> ==常用命令==

```bash
# 设置指定的key值
SET key value

# 获取指定的key值
GET key

# 返回 key 中字符串值的子字符
GETRANGE key start end # 当end = -1时截取到最后，这里左右都是闭区间

# 将给定 key 的值设为 value ，并返回 key 的旧值(old value)。
GETSET key value

# 对 key 所储存的字符串值，获取指定偏移量上的位(bit)。
GETBIT key offset

# 获取所有(一个或多个)给定 key 的值。
MGET key1 [key2..]

# 将值 value 关联到 key ，并将 key 的过期时间设为 seconds (以秒为单位)。
SETEX key seconds value

# 只有在 key 不存在时设置 key 的值。
SETNX key value

# 同时设置一个或多个 key-value 对。
MSET key value [key value ...]

# 同时设置一个或多个 key-value 对，当且仅当所有给定 key 都不存在。
MSETNX key value [key value ...]   # 这里遵循原子性，只有有一个失败，就全失败

# 将 key 中储存的数字值增一。
INCR key

# 将 key 所储存的值加上给定的增量值（increment） 。
INCRBY key increment

# 将 key 所储存的值加上给定的浮点增量值（increment） 。
INCRBYFLOAT key increment

# 将 key 中储存的数字值减一。
DECR key

# key 所储存的值减去给定的减量值（decrement） 。
DECRBY key decrement

# 如果 key 已经存在并且是一个字符串， APPEND 命令将指定的 value 追加到该 key 原来值（value）的末尾。
APPEND key value

# 这个命令和 SETEX 命令相似，但它以毫秒为单位设置 key 的生存时间，而不是像 SETEX 命令那样，以秒为单位。
PSETEX key milliseconds value
```

> ==存储对象==

**格式:  user:{id}:{field}**

设置一个对象，值为json字符串来保存一个对象

```bash
127.0.0.1:6379> mset user:1:name fafa user:1:age 21OK127.0.0.1:6379> mget user:1:name1) "fafa"127.0.0.1:6379> mget user:1:name user:1:age1) "fafa"2) "21"127.0.0.1:6379> 
```

 ![image-20211126160422768](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211126160432.png)

> ==小结==

String类似的使用场景：value除了是我们的**字符串**还可是**数字**

-  计数器
-  统计多单位的数量 uid :id:follow:number
-  粉丝数
-  对象存储



### 3.3、List

基本的数据类型，列表

 ![image-20211129173456369](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211129173503.png)

在redis里面，我们可以把redis玩成 栈，队列，阻塞队列！

所有的 list 命令 **大部分** 都是用 **L** 开头的

```bash
#####################################################################################
127.0.0.1:6379> LPUSH list one  # 将一个值或者多个值，插入到列表头部（左）
(integer) 1
127.0.0.1:6379> LPUSH list two
(integer) 2
127.0.0.1:6379> LPUSH list three
(integer) 3
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "two"
3) "one"
#####################################################################################
127.0.0.1:6379> RPUSH list origin  # 将一个值或者多个值，插入到列表尾部（右）
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "two"
3) "one"
4) "origin"
#####################################################################################
LPOP（左）
RPOP（右）
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "two"
3) "one"
4) "origin"
127.0.0.1:6379> LPOP list  # 移除list的第一个元素
"three"
127.0.0.1:6379> RPOP list  # 移除list的最后一个元素
"origin"
127.0.0.1:6379> LRANGE list 0 -1
1) "two"
2) "one"
#####################################################################################
LINDEX
127.0.0.1:6379> LRANGE list 0 -1
1) "two"
2) "one"
127.0.0.1:6379> LINDEX list 0 # 通过下标获得 list 中的某一个值（下标从0开始）
"two"
127.0.0.1:6379> LINDEX list 1 # 通过下标获得 list 中的某一个值（下标从0开始）
"one"
#####################################################################################
LLEN
127.0.0.1:6379> LPUSH list one
(integer) 3
127.0.0.1:6379> LPUSH list two
(integer) 4
127.0.0.1:6379> LPUSH list three
(integer) 5
127.0.0.1:6379> LLEN list # 获得list的长度
(integer) 5
#####################################################################################
LREM # 移除元素·
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "two"
3) "one"
4) "two"
5) "one"
127.0.0.1:6379> LREM list 2 one # 移除list中 两个 元素"one"
(integer) 2
127.0.0.1:6379> LREM list 0 -1 # 移除list中 0个 元素 "-1"
(integer) 0
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "two"
3) "two"
#####################################################################################
LTRIM
127.0.0.1:6379> RPUSH mylist "hello"
(integer) 1
127.0.0.1:6379> RPUSH mylist "hello2"
(integer) 2
127.0.0.1:6379> RPUSH mylist "hello3"
(integer) 3
127.0.0.1:6379> RPUSH mylist "hello4"
(integer) 4
127.0.0.1:6379> RPUSH mylist "hello5"
(integer) 5
127.0.0.1:6379> LTRIM mylist 1 3  # 通过下标截取指定的长度，这个list已经改变了，截断了只剩下截取的元素！
OK
127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello2"
2) "hello3"
3) "hello4"
#####################################################################################
RPOPLPUSH # 移除列表的最后一个元素，将他移动到新的列表中！
127.0.0.1:6379> RPUSH mylist "hello"
(integer) 1
127.0.0.1:6379> RPUSH mylist "hello1"
(integer) 2
127.0.0.1:6379> RPUSH mylist "hello2"
(integer) 3
127.0.0.1:6379> RPOPLPUSH mylist myotherlist # 移除列表的最后一个元素，然后将他移动到新的列表中
"hello2"
127.0.0.1:6379> LRANGE mylist 0 -1 # 查看原来的列表
1) "hello"
2) "hello1"
127.0.0.1:6379> LRANGE myotherlist 0 -1 # 查看目标列表中，确实存在改动值！
1) "hello2"
#####################################################################################
LSET # 更新或者添加操作（将列表中指定下标的值替换为另一个）
127.0.0.1:6379> EXISTS list # 先判断是否存在
(integer) 0
127.0.0.1:6379> LSET list 0 item # 如不存在就会报错
(error) ERR no such key
127.0.0.1:6379> LPUSH list demo01
(integer) 1
127.0.0.1:6379> LRANGE list 0 -1
1) "demo01"
127.0.0.1:6379> LSET list 0 item # 如果存在就会进行更新
OK
127.0.0.1:6379> LRANGE list 0 -1
1) "item"
127.0.0.1:6379> LSET list 1 other # 不存在这个
(error) ERR index out of range
#####################################################################################
LINSERT # 将某个具体的value插入到类表中某个元素的前面或者后面
127.0.0.1:6379> RPUSH mylist hello
(integer) 1
127.0.0.1:6379> RPUSH mylist world
(integer) 2
127.0.0.1:6379> LINSERT mylist before world other
(integer) 3
127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello"
2) "other"
3) "world"
127.0.0.1:6379> LINSERT mylist after world new
(integer) 4
127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello"
2) "other"
3) "world"
4) "new"

```

> ==小结==

- 实际上是一个**链表**，before Node after，left，right都可以插入值
- 如果key不存在，创建新的链表
- 如果key存在，新增内容
- 如果移除了所有值，空链表，也代表不存在！
- 在两边插入或者改动值，效率最高！中间元素，相对来说效率会低一些~

消息排队！ 消息队列（Lpush Rpop），栈（Lpush Lpop）

### 3.4、Set(集合)

和java里的set一样，是无序不重复的集合

| 序号 | 命令及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [SADD key member1 [member2\]](https://www.runoob.com/redis/sets-sadd.html) 向集合添加一个或多个成员 |
| 2    | [SCARD key](https://www.runoob.com/redis/sets-scard.html) 获取集合的成员数 |
| 3    | [SDIFF key1 [key2\]](https://www.runoob.com/redis/sets-sdiff.html) 返回第一个集合与其他集合之间的差异。 |
| 4    | [SDIFFSTORE destination key1 [key2\]](https://www.runoob.com/redis/sets-sdiffstore.html) 返回给定所有集合的差集并存储在 destination 中 |
| 5    | [SINTER key1 [key2\]](https://www.runoob.com/redis/sets-sinter.html) 返回给定所有集合的交集 |
| 6    | [SINTERSTORE destination key1 [key2\]](https://www.runoob.com/redis/sets-sinterstore.html) 返回给定所有集合的交集并存储在 destination 中 |
| 7    | [SISMEMBER key member](https://www.runoob.com/redis/sets-sismember.html) 判断 member 元素是否是集合 key 的成员 |
| 8    | [SMEMBERS key](https://www.runoob.com/redis/sets-smembers.html) 返回集合中的所有成员 |
| 9    | [SMOVE source destination member](https://www.runoob.com/redis/sets-smove.html) 将 member 元素从 source 集合移动到 destination 集合 |
| 10   | [SPOP key](https://www.runoob.com/redis/sets-spop.html) 移除并返回集合中的一个随机元素 |
| 11   | [SRANDMEMBER key [count\]](https://www.runoob.com/redis/sets-srandmember.html) 返回集合中一个或多个随机数 |
| 12   | [SREM key member1 [member2\]](https://www.runoob.com/redis/sets-srem.html) 移除集合中一个或多个成员 |
| 13   | [SUNION key1 [key2\]](https://www.runoob.com/redis/sets-sunion.html) 返回所有给定集合的并集 |
| 14   | [SUNIONSTORE destination key1 [key2\]](https://www.runoob.com/redis/sets-sunionstore.html) 所有给定集合的并集存储在 destination 集合中 |
| 15   | [SSCAN key cursor [MATCH pattern\] [COUNT count]](https://www.runoob.com/redis/sets-sscan.html) 迭代集合中的元素 |

```bash
#####################################################################################
127.0.0.1:6379> SADD myset hello
(integer) 1
127.0.0.1:6379> SADD myset fafa
(integer) 1
127.0.0.1:6379> SADD myset lovelyfa
(integer) 1
127.0.0.1:6379> SMEMBERS myset # 查看指定的set的所有值
1) "lovelyfa"
2) "fafa"
3) "hello"
127.0.0.1:6379> SISMEMBER myset fafa # 判断一个元素是不是在set集合中
(integer) 1
127.0.0.1:6379> SISMEMBER myset world
(integer) 0
#####################################################################################
127.0.0.1:6379> SCARD myset # 获取set集合中的内容元素个数
(integer) 3
#####################################################################################
SREM # 删除元素
127.0.0.1:6379> SREM myset hello # 移除set集合中的指定元素
(integer) 1
127.0.0.1:6379> SCARD myset
(integer) 2
127.0.0.1:6379> SMEMBERS myset
1) "lovelyfa"
2) "fafa"
#####################################################################################
127.0.0.1:6379> SADD myset alne
(integer) 1
127.0.0.1:6379> SADD myset bob
(integer) 1
127.0.0.1:6379> SADD myset cici
(integer) 1
127.0.0.1:6379> SADD myset ac
(integer) 1
127.0.0.1:6379> SRANDMEMBER myset # 随机获得集合中的元素（默认为1个，后面可以自己添加·）
"bob"
127.0.0.1:6379> SRANDMEMBER myset
"fafa"
127.0.0.1:6379> SRANDMEMBER myset
"lovelyfa"
127.0.0.1:6379> SRANDMEMBER myset 2
1) "cici"
2) "ac"
127.0.0.1:6379> SRANDMEMBER myset 4
1) "ac"
2) "alne"
3) "fafa"
4) "cici"
#####################################################################################
# 将指定的值移动到另一个集合中·
127.0.0.1:6379> SADD myset hello
(integer) 1
127.0.0.1:6379> SADD myset world
(integer) 1
127.0.0.1:6379> SADD myset fafa
(integer) 1
127.0.0.1:6379> SADD myset2 set2
(integer) 1
127.0.0.1:6379> SMOVE myset myset2 fafa # 将指定的值移动到另一个集合中·
(integer) 1
127.0.0.1:6379> SMEMBERS myset2
1) "fafa"
2) "set2"
#####################################################################################
# 微博，B站，全民（共同关注）
127.0.0.1:6379> SADD key1 a
(integer) 1
127.0.0.1:6379> SADD key1 b
(integer) 1
127.0.0.1:6379> SADD key1 c
(integer) 1
127.0.0.1:6379> SADD key2 c
(integer) 1
127.0.0.1:6379> SADD key2 d
(integer) 1
127.0.0.1:6379> SADD key2 e
(integer) 1
127.0.0.1:6379> 
127.0.0.1:6379> SDIFF key1 key2 # 差集
1) "b"
2) "a"
127.0.0.1:6379> SINTER  key1 key2 # 交集
1) "c"
127.0.0.1:6379> SUNION  key1 key2 # 并集
1) "c"
2) "a"
3) "b"
4) "d"
5) "e"
```

微博，将A用户所有的关注都放在一个集合，将他的粉丝放在另一个集合中！

共同关注，共同友，二度好友，推荐好友!（六度分割理论）

### 3.5、Hash(哈希)

Hash和String很相似，只不过多了一个·**field**

```bash
#####################################################################################
# 添加元素
127.0.0.1:6379> HSET myhash field1 fafa
(integer) 1
127.0.0.1:6379> HSET myhash field2 world # 设置单个元素
(integer) 1
127.0.0.1:6379> HGET myhash field1 # 获取单个元素
"fafa"
127.0.0.1:6379> HMSET myhash field1 hello field2 World # 设置多个元素
OK
127.0.0.1:6379> HMGET myhash field1 field2  # 获取多个元素
1) "hello"
2) "World"
127.0.0.1:6379> HGETALL myhash # 或全部元素（key + value）
1) "field1"
2) "hello"
3) "field2"
4) "World"
127.0.0.1:6379> HLEN myhash # 获取集合的长度
(integer) 2
127.0.0.1:6379> HDEL myhash field1 # 删除元素
(integer) 1
#####################################################################################
127.0.0.1:6379> HEXISTS myhash field2 # 判断指定元素是否存在
(integer) 1
#####################################################################################
127.0.0.1:6379> HKEYS myhash # 获得所有的key
1) "field2"
127.0.0.1:6379> HVALS myhash # 获得所有的value
1) "World"
#####################################################################################
HINCRBY  # 增加
HDECRBY # 减少
127.0.0.1:6379> HSET myhash field1 5
(integer) 1
127.0.0.1:6379> HINCRBY myhash field1 1
(integer) 6
127.0.0.1:6379> HINCRBY myhash field1 -1
(integer) 5
#####################################################################################
# 存储对象（推荐）
127.0.0.1:6379> HSET myhash:1 name fafa age 21 # 设置对象
(integer) 2
127.0.0.1:6379> HMGET myhash:1 name age # 获取对象
1) "fafa"
2) "21"
```

Hash变更数据user name age,尤其是用户信息之类的，经常变动的信息！

Hash更适合对象的存储，String更适合字符串的存储！！！

### 3.6、Zset(有序的set集合)



```bash
#####################################################################################127.0.0.1:6379> ZADD salary 2500 xiaohong(integer) 1127.0.0.1:6379> ZADD salary 5000 zhangsan(integer) 1127.0.0.1:6379> ZADD salary 500 fafa(integer) 1127.0.0.1:6379> ZRANGEBYSCORE salary -inf +inf # inf 代表无穷的意思，从低到高排序·1) "fafa"2) "xiaohong"3) "zhangsan"127.0.0.1:6379> ZRANGE salary 0 -1  # 获取全部元素1) "fafa"2) "xiaohong"3) "zhangsan"127.0.0.1:6379> ZRANGEBYSCORE salary -inf +inf withscores # 附带scores1) "fafa"2) "500"3) "xiaohong"4) "2500"5) "zhangsan"6) "5000"###################################################################################### 删除元素 ZREM127.0.0.1:6379> ZREM salary xiaohong(integer) 1127.0.0.1:6379> ZCARD salary # 获取有序集合中的个数(integer) 2127.0.0.1:6379> ZCOUNT salary 0 +inf # 统计区间内的元素个数(integer) 2
```

- 其余的一些API，通过我们的学习吗，你们剩下的如果工作中有需要，这个时候你可以去查查	

  ​	

- 看官方文档!案例思路: set 排序存储班级成绩表，工资表排序!
  		

- 普通消息，1，重要消息2，带权重进行判断!
  		

- 排行榜应用实现，取Top N测试!



## 四、三大特殊类型

### 4.1、Geospatial（地图）

> ==GEOADD==

将指定的地理空间位置（纬度、经度、名称）添加到指定的`key`中。这些数据将会存储到`sorted set`这样的目的是为了方便使用[GEORADIUS](http://www.redis.cn/commands/georadius.html)或者[GEORADIUSBYMEMBER](http://www.redis.cn/commands/georadiusbymember.html)命令对数据进行半径查询等操作。

```bash
# 有效的经度从-180度到180度。# 有效的纬度从-85.05112878度到85.05112878度。127.0.0.1:6379> GEOADD china:city 116.40 39.90 beijing(integer) 1127.0.0.1:6379> GEOADD china:city 121.47 31.23 shanghai(integer) 1127.0.0.1:6379> GEOADD china:city 106.50 29.53 chongqing(integer) 1127.0.0.1:6379> GEOADD china:city 114.05 22.52 shenzhen(integer) 1127.0.0.1:6379> GEOADD china:city 120.16 30.24 hangzhou(integer) 1127.0.0.1:6379> GEOADD china:city 106.96 34.26 xian(integer) 1
```

> ==GEOPOS==

获取指定城市的经纬度

```bash
127.0.0.1:6379> GEOPOS china:city beijing1) 1) "116.39999896287918091"   2) "39.90000009167092543"127.0.0.1:6379> GEOPOS china:city chongqing1) 1) "106.49999767541885376"   2) "29.52999957900659211"
```

> ==GEODIST==

返回两个给定位置之间的距离。

如果两个位置之间的其中一个不存在， 那么命令返回空值。

指定单位的参数 unit 必须是以下单位的其中一个：

- **m** 表示单位为米。
- **km** 表示单位为千米。
- **mi** 表示单位为英里。
- **ft** 表示单位为英尺。

```bash
127.0.0.1:6379> GEODIST china:city beijing chongqing # 查看北京到重庆的距离"1464070.8051"127.0.0.1:6379> GEODIST china:city beijing chongqing km  # 结果转换为km"1464.0708"127.0.0.1:6379> GEODIST china:city beijing shanghai km"1067.3788"
```

> ==GEORADIUS==

附近的人？（获得所有附近的人的地址，定位！）通过半径来查询

```bash
127.0.0.1:6379> GEORADIUS china:city 100 30 1000 km # 显示在经100，纬30，方圆100km以内的城市1) "chongqing"2) "xian"127.0.0.1:6379> GEORADIUS china:city 100 30 1000 km withdist # 显示纬度1) 1) "chongqing"2) "629.6756"2) 1) "xian"2) "808.5178"127.0.0.1:6379> GEORADIUS china:city 100 30 1000 km withcoord # 显示经度1) 1) "chongqing"2) 1) "106.49999767541885376"2) "29.52999957900659211"2) 1) "xian"2) 1) "106.96000188589096069"2) "34.25999964418929977"127.0.0.1:6379> GEORADIUS china:city 100 30 1000 km withcoord count 1 # 可以限定查询的结果数1) 1) "chongqing"2) 1) "106.49999767541885376"2) "29.52999957900659211"
```

> ==GEORADIUSBYMEMBER==

```bash
# 找出位于指定元素的位置内容127.0.0.1:6379> GEORADIUSBYMEMBER china:city xian 1000 km1) "xian"2) "chongqing"127.0.0.1:6379> GEORADIUSBYMEMBER china:city shanghai 1000 km1) "hangzhou"2) "shanghai"
```

> ==GEOHASH==

该命令将返回11个字符的GEOHASH字符串！

```bash
# 将二维的经纬度，转为一维的字符串127.0.0.1:6379> GEOHASH china:city chongqing shanghai1) "wm5xzrybty0"2) "wtw3sj5zbj0"
```

> ==底层原理==

其实底层运用的就是**ZSET**，所**ZSET**命令在此处依然是合法的

```bash
127.0.0.1:6379> ZRANGE china:city 0 -11) "chongqing"2) "xian"3) "shenzhen"4) "hangzhou"5) "shanghai"6) "beijing"127.0.0.1:6379> ZREM china:city beijing(integer) 1
```

### 4.2、Hyperloglog

> ==简介==

Redis Hyperloglog 基数统计的算法！

优点：占用的内存是固定的，2^64不同的元素的基数，只需要12kb的内存！如果要从内存的角度比较的话，Hyperloglog是首选！

**网页的UV（一个人访问一个网站多次，但还是算作一个人！）**

传统的方式，set保存用户的id，然后就可以统计set中的元素数量作为标准判断！

但是这个方式如果保存大量的用户id，就会比较麻烦！我们的目的是为了计数，而不是保护用户id；

0.81%错误率！统计UV任务！可以忽略不计的！

> ==测试使用==

```bash
127.0.0.1:6379> PFADD mykey a bc d e f g h i g k l # 创建第一组元素(integer) 1127.0.0.1:6379> PFCOUNT mykey # 统计元素中的 基数 数量(integer) 10127.0.0.1:6379> PFADD mykey2 i j k l o p g n f a(integer) 1127.0.0.1:6379> PFCOUNT mykey2(integer) 10127.0.0.1:6379> PFMERGE mykey3 mykey mykey2 # 合并两组 基数（不能重复的）OK127.0.0.1:6379> PFCOUNT mykey3
```

如果允许容错，那么一定可以使用 Hyperloglog ！

若果不允许容错，就是用set或者自己的数据类型即可5



### 4.3、Bitmap

> ==位存储==

统计用户信息，活跃，不活跃！登录、未登录！打卡，365天打卡！

像这种两个状态的，都可以使用Bitmaps

365天 = 365bit 1字节 = 8bit  46个字节左右



周一到周日的打卡

周一：1   周二：0……

```bash
127.0.0.1:6379> SETBIT sign 0 1  # 周一(integer) 0127.0.0.1:6379> SETBIT sign 1 0  # 周二(integer) 0127.0.0.1:6379> SETBIT sign 2 1  # 周三(integer) 0127.0.0.1:6379> SETBIT sign 3 1(integer) 0127.0.0.1:6379> SETBIT sign 4 0(integer) 0127.0.0.1:6379> SETBIT sign 5 1(integer) 0127.0.0.1:6379> SETBIT sign 6 1(integer) 0
```

查看 某一天是否打卡

```bash
127.0.0.1:6379> GETBIT sign 4(integer) 0127.0.0.1:6379> GETBIT sign 3(integer) 1127.0.0.1:6379> GETBIT sign 6(integer) 1
```

统计打卡天数

```bash
127.0.0.1:6379> BITCOUNT sign # 统计这周的打卡记录 ，可以作为考勤(integer) 5
```



## 五、事务

Redis事务本质：一组命令的集合！一个事务中的所有命令都会被序列化，在事务执行过程中，会按照顺序执行！

一次性，顺序性，排他性！执行一些列的命令！

```bash
-----队列 set set set 执行-------
```

==Redis事务没有隔离级别的概念==

所有的命令在事务中，并没有直接被执行！只有发起执行命令的时候才会执行 Exectue

==Redis 单条命令保存原子性的，但是事务不保证原子性（要么都成功，要么都失败）！==

Redsi事务：

- 开启事务（MULTI ）
- 命令入队（SET ）
- 执行事务（EXEC ）

锁：乐观锁

> ==正常执行事务==

```bash
127.0.0.1:6379> MULTI # 开启事务
OK
127.0.0.1:6379(TX)> set k1 v1 # 命令入队
QUEUED
127.0.0.1:6379(TX)> set k2 v2
QUEUED
127.0.0.1:6379(TX)> set k3 v3
QUEUED
127.0.0.1:6379(TX)> get k2
QUEUED
127.0.0.1:6379(TX)> EXEC # 执行事务
1) OK
2) OK
3) OK
4) "v2"
```



> ==放弃事务！==

```bash
127.0.0.1:6379> clear127.0.0.1:6379> MULTIOK127.0.0.1:6379(TX)> SET k1 v1QUEUED127.0.0.1:6379(TX)> SET k2 v2QUEUED127.0.0.1:6379(TX)> SET k3 v3QUEUED127.0.0.1:6379(TX)> SET k4 v4QUEUED127.0.0.1:6379(TX)> GET k2QUEUED127.0.0.1:6379(TX)> DISCARD  # 取消事务（回滚）OK127.0.0.1:6379> GET k3 # 事务队列中命令不会被执行！(nil)127.0.0.1:6379> GET k4(nil)
```

> ==编译型异常（代码有问题！命令有错！），事务中所有的命令都不会被执行！==

```bash
127.0.0.1:6379> MULTIOK127.0.0.1:6379(TX)> SET k1 v1QUEUED127.0.0.1:6379(TX)> SET k2 v2QUEUED127.0.0.1:6379(TX)> SET k3 v3QUEUED127.0.0.1:6379(TX)> GETSET k3(error) ERR wrong number of arguments for 'getset' command127.0.0.1:6379(TX)> SET k4 v4QUEUED127.0.0.1:6379(TX)> SET k5 v5QUEUED127.0.0.1:6379(TX)> EXEC  # 执行事务就报错了，所有命令都不会被执行(error) EXECABORT Transaction discarded because of previous errors.
```

> ==运行型异常（1 / 0）==

如果事务队列中存在语法性，那么执行命令的时候，其他命令是可以正常执行的，错误命令抛出异常！

```bash
127.0.0.1:6379(TX)> SET k1 "v1"QUEUED127.0.0.1:6379(TX)> INCR k1  # 字符串不能进行加减运算QUEUED127.0.0.1:6379(TX)> SET k2 v2QUEUED127.0.0.1:6379(TX)> SET k3 v3QUEUED127.0.0.1:6379(TX)> SET k4 v4QUEUED127.0.0.1:6379(TX)> EXEC  # 整体事务保证原子性，所以其他语句都执行成功了！1) (integer) 12) OK3) (error) ERR value is not an integer or out of range4) OK5) OK6) OK127.0.0.1:6379> GEt K2(nil)127.0.0.1:6379> GEt k2"v2"
```



## 六、**监控（Watch）**【重点】

> ==悲观锁==

很谨慎（很悲观），认为什么时候都会出问题，无论做什么都要加锁！！！（效率极其低下，比如**Synchronized**）

> ==乐观锁==

很乐观，认为什么时候都不会出现问题，所以不会上锁！更新数据的时候去判断一下，是否有人修改过这个数据，==version==(在mysql使用这个)！

> ==Redis监视测试==

单线程操作！

```bash
127.0.0.1:6379> SET money 100OK127.0.0.1:6379> SET out 0OK127.0.0.1:6379> WATCH money  # 监视 money 对象OK127.0.0.1:6379> MULTI  OK127.0.0.1:6379(TX)> DECRBY money 20QUEUED127.0.0.1:6379(TX)> INCRBY out 20QUEUED127.0.0.1:6379(TX)> EXEC  # 事务正常结束，数据期间没有变动，这个时候就正常执行成功！1) (integer) 802) (integer) 20
```

> ==多线程下的==

测试多线程修改值，使用watch 可以当做redis的乐观锁操作！

```bash
127.0.0.1:6379> WATCH money # 监视 moneyOK127.0.0.1:6379> MULTI  # 开启事务OK127.0.0.1:6379(TX)> DECRBY money 10QUEUED127.0.0.1:6379(TX)> INCRBY out 10QUEUED127.0.0.1:6379(TX)> EXEC  # 执行之前，另一个线程，修改了money的值，这时候我们在执行就会报错!(nil)
```

如何解决？

- 先解锁，再上锁（相当于一个更新！！！）
- 然后再重新进行事务操作！！！

```bash
127.0.0.1:6379> UNWATCH  # 先解锁OK127.0.0.1:6379> WATCH money # 再上锁OK127.0.0.1:6379> DECRBY money 10(integer) 990127.0.0.1:6379> UNWATCHOK127.0.0.1:6379> clear127.0.0.1:6379> WATCH moneyOK127.0.0.1:6379> MULTIOK127.0.0.1:6379(TX)> DECRBY money 10QUEUED127.0.0.1:6379(TX)> INCRBY money 10QUEUED127.0.0.1:6379(TX)> EXEC1) (integer) 9802) (integer) 990
```

## 七、Jedis

我们要使用java来操作 Redis

> ==什么是Jedis ？ 它是Redis官方推荐的java连接开发工具！ 使用java操作Redis中间件！如果你使用java操作redis，那么一定要对Jedis十分的熟悉！！！==

知其然不知其所以然！授人以渔！学习不能急躁！慢慢来就会了！

> ==导入Jedis==

```xml
<!-- https://mvnrepository.com/artifact/redis.clients/jedis --><dependency>    <groupId>redis.clients</groupId>    <artifactId>jedis</artifactId>    <version>3.2.0</version></dependency><!--fastjson--><dependency>    <groupId>com.alibaba</groupId>    <artifactId>fastjson</artifactId>    <version>1.2.62</version></dependency>
```

ping一下，运行结果

```java
public class TestPing {    public static void main(String[] args) {        // 1、 new Jedis 对象即可        Jedis jedis = new Jedis();        // Jedis 所有的命令就是我们之前学的所有的命令        System.out.println(jedis.ping());    }}
```

![image-20211202223205742](C:\Users\Sire\AppData\Roaming\Typora\typora-user-images\image-20211202223205742.png)

> ==回顾事务==

```java
public class TestTx {    public static void main(String[] args) {        Jedis jedis = new Jedis("127.0.0.1",6379);        // 开启事务        JSONObject jsonObject = new JSONObject();        jsonObject.put("hello","world");        jsonObject.put("name","fafa");        Transaction multi = jedis.multi();        String s = jsonObject.toJSONString();        try {            multi.set("user1",s);            multi.set("user2",s);            // 执行事务！            multi.exec();        } catch (Exception e) {            // 取消事务(回滚)！            multi.discard();            e.printStackTrace();        } finally {            System.out.println(jedis.get("user1"));            System.out.println(jedis.get("user2"));            // 关闭连接            jedis.close();        }    }}
```

 ![image-20211202231334025](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211202231335.png)

 ![image-20211202231551037](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211202231551.png)



## 八、SpringBoot整合

SpringBoot操作数据：是封装在Spring-data中的，jpa、jdbc、mongodb、redis

在SpringBoot2.x以后与原来使用的jedis被替换成来看lettuce，底层已经不使用jedis了

- jedis：采用的直连，多个线程操作的话，不安全，要提高安全性要使用jedis pool连接池
- lettuce：采用netty，高性能网络框架，异步请求，实例在多线程中可以共享，不存在线程不安全的情况，dubbo底层也是用netty，可以减少线程数量，更像NIO

```xml
<dependency>    <groupId>org.springframework.boot</groupId>    <artifactId>spring-boot-starter-data-redis</artifactId></dependency>
```

### 8.1、原理

- SpringBoot所有配置类，都会有一个自动配置类

  ![image-20211203214611015](C:\Users\Sire\AppData\Roaming\Typora\typora-user-images\image-20211203214611015.png)

- 自动配置类都会绑定一个properties配置文件

- RedisAutoConfiguation

  ![image-20211203214653218](C:\Users\Sire\AppData\Roaming\Typora\typora-user-images\image-20211203214653218.png)

  

- 启动配置类中有一个RedisProperties配置类

  ![image-20211203214721634](C:\Users\Sire\AppData\Roaming\Typora\typora-user-images\image-20211203214721634.png)

- 里面有很多以前缀spring.redis开头的配置，可以在application中配置

  

- 如host、password、配置

- RedisAutoConfiguation中封装了两个Bean

  - RedisTemplate

    ```java
    @Bean@ConditionalOnMissingBean(name = "redisTemplate")public RedisTemplate<Object, Object> redisTemplate(RedisConnectionFactory redisConnectionFactory)    throws UnknownHostException {    RedisTemplate<Object, Object> template = new RedisTemplate<>();    template.setConnectionFactory(redisConnectionFactory);    return template;}
    ```

    - 没有过多的设置，Redis的对象都是需要序列化的
    - 两个泛型都是object，后面使用需要强制转换
    - 靠自己重写config来替换这个template

  - StringRedisTamplate

    - 大部分情况下String类型是最常用的，就会多一个StringRedisTemplate

  - ```java
    @ConditionalOnMissingBean(name = "redisTemplate")
    //重写一个redisTemplate就能替换掉这个bean
    ```

### 8.2、整合实现

- 导入依赖
- 配置连接
- 测试

> ==实现==

- 依赖

  ```xml
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-data-redis</artifactId>
  </dependency>
  ```

- 根据在properties中看到的配置参数，以spring.redis为prefix的配置

- 但是建议使用lettuce

- 在redisTemplate的parameter中需要给入一个RedisConnectionFactory

  ![image-20211203221552974](C:\Users\Sire\AppData\Roaming\Typora\typora-user-images\image-20211203221552974.png)

- 有两个方法实现了这个接口

- 在Jedis中有多个爆红，没下载完整

- lettuce中下载完整，为了避免不必要的错误，建议使用lettuce，默认生效

- 测试

  Redis02SpringbootApplicationTests.java

  ```java
  package com.fafa;
  
  import com.fafa.pojo.User;
  import com.fasterxml.jackson.core.JsonProcessingException;
  import com.fasterxml.jackson.databind.ObjectMapper;
  import org.junit.jupiter.api.Test;
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.beans.factory.annotation.Qualifier;
  import org.springframework.boot.test.context.SpringBootTest;
  import org.springframework.data.redis.core.RedisTemplate;
  
  @SpringBootTest
  class Redis02SpringbootApplicationTests {
      @Autowired
      @Qualifier(value = "redisTemplate")
      private RedisTemplate redisTemplate;
  
      @Test
      void contextLoads() {
  
      }
  
      @Test
      void test() throws JsonProcessingException {
          User user = new User("可爱发", 18);
          // 这里需要序列化，可以直接让实体类实现 Serializable 接口，也可以使用下面的ObjectMapper
          String jsonUser = new ObjectMapper().writeValueAsString(user);
          redisTemplate.opsForValue().set("user",jsonUser);
          System.out.println(redisTemplate.opsForValue().get("user"));
      }
  
  }
  
  ```

- Redis的对象都需要序列化serialization

- 默认的序列化是JDK序列化，可能要使用JSON来序列化

- 需要自己来定义配置类

- 创建对象时需要序列化、implement Serializable

  **RedisConfig.java**

  ```java
  package com.fafa.config;
  
  import com.fasterxml.jackson.annotation.JsonAutoDetect;
  import com.fasterxml.jackson.annotation.PropertyAccessor;
  import com.fasterxml.jackson.databind.ObjectMapper;
  import org.springframework.context.annotation.Bean;
  import org.springframework.context.annotation.Configuration;
  import org.springframework.data.redis.connection.RedisConnectionFactory;
  import org.springframework.data.redis.core.RedisTemplate;
  import org.springframework.data.redis.serializer.Jackson2JsonRedisSerializer;
  import org.springframework.data.redis.serializer.StringRedisSerializer;
  
  /**
   * @author Sire
   * @version 1.0
   * @date 2021-11-17 23:42
   */
  @Configuration
  public class RedisConfig {
      // 编写我们自己的 redisTemplate
      @Bean
      @SuppressWarnings("all")
      public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory redisConnectionFactory) {
          RedisTemplate<String, Object> template = new RedisTemplate<>();
          // 连接
          template.setConnectionFactory(redisConnectionFactory);
          Jackson2JsonRedisSerializer jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer(Object.class);
          ObjectMapper om = new ObjectMapper();
          om.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
          om.enableDefaultTyping(ObjectMapper.DefaultTyping.NON_FINAL);
          jackson2JsonRedisSerializer.setObjectMapper(om);
          StringRedisSerializer stringRedisSerializer = new StringRedisSerializer();
  
          /**
           * 配置具体的序列化方式
           * **/
          // key采用String的序列化方式
          template.setKeySerializer(stringRedisSerializer);
          // hash的key也采用String的序列化方式
          template.setHashKeySerializer(stringRedisSerializer);
          // value序列化方式采用jackson
          template.setValueSerializer(jackson2JsonRedisSerializer);
          // hash的value序列化方式采用jackson
          template.setHashValueSerializer(jackson2JsonRedisSerializer);
          template.afterPropertiesSet();
          return template;
      }
  }
  ```

## 九、Redis高级技能

### 9.1、配置文件分析

```bash
bind 127.0.0.1
#绑定的ip
protected-mode yes
#保护模式
port 6379
#端口
#这些配置之后可能会经常使用

daemonize yes 
#以守护线程的方式开启

#日志
debug、verbose、notice、warning
#设置日志等级
loglevel notice

logfile
#设置日志文件位置

database 16
#16个数据库

always-show-logo yes 
#永远显示logo

snapshotting#快照
三个方法，在规定时间内，执行了多少次操作，则会持久化到文件  .rdb  .aof
redis是内存数据库，没有持久化，数据就会丢失
save 900 1  #900秒内，至少有一个key进行了修改，就进行持久化操作
save 300 10  #。。。。。
save 60 10000  #同理

stop-writes-on-bgseve-error yes
#持久化错误之后是否要继续工作，默认开启

rdbcompression yes
#是否压缩rdb文件，需要消耗cpu资源

rdbchecksum yes
#保存rdb文件是否要进行错误检查校验

dir 	./
#rdb文件保存的目录

replication #主从复制，需要搭建多个redis


Security #安全设置
requirepass foobared
#默认没有密码
#通过命令config set requirepass 可以设置密码
#auth password   进行登录

########################################################################
127.0.0.1:6379> config get requirepass
1) "requirepass"
2) ""
127.0.0.1:6379> config set requirepass 123
OK
127.0.0.1:6379> ping 
PONG
127.0.0.1:6379> quit
haoyun@HAOYUN ~ % redis-cli         #设置密码操作
127.0.0.1:6379> ping
(error) NOAUTH Authentication required.
127.0.0.1:6379> auth 123
OK
127.0.0.1:6379> ping
PONG
127.0.0.1:6379> 
########################################################################


maxlients 10000 
#设置能连接上redis的最大客户端数量
maxmemory <bytes>
#redis配置最大的内存数
maxmemory-policy noeviction
#内存到达上限之后的处理策略
#移除一些过期的key
#报错、、、
#六种机制
volatile-lru：设置了过期时间的key进行lru移除
allkeys-lru：删除
volatile-random：删除即将过期的key
allkeys-random：随机删除
volatile-ttl：删除即将过期的
noeviction：永远不过期，直接报错



Append only模式  aof模式
#持久化的两种方式之一RDB、AOF
appendonly no
#默认是不开启的，默认使用RDB持久化，大部分情况下RDB完全够用

appendfilename "appendonly.aof"
#aof持计划文件名

appendfsync always 
#每次修改都会synch 消耗性能
appendfsync everysec 
#每秒执行一次 synch，可能会丢失那1s的数据
appendfsync no
#不执行sync 这时候操作系统自己同步数据，速度是最快的，一般也不用

```

### 9.2、Redis持久化

持久化RDB、AOF，重点

Redis是内存数据库，断电即失去，只要是内存数据库就一定会有持久化操作

#### 1、RDB(Redis DataBase)

在指定的时间 间隔内将内存中的数据集快照写入到磁盘中，Snapshot快照，恢复时将快照文件直接读到内存中

 ![image-20211204185600768](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211222125351.png)

- 单独创建一个子进程，fork分支
- 将内存内容写入临时RDB文件
- 再用临时文件替换上次持久化完成的文件

整个过程主进程不进行任何io操作，保证了性能，如果进行大规模数据恢复，RDB和AOP都可以进行数据恢复，RDB数据恢复完整性不敏感，RDB更加高效，缺点是最后一次持久化后的数据可能丢失，默认使用的就是RDB，一般情况不需要修改这个配置

RDB保存的文件是dump.rdb

AOF保存的文件是appendonly.aof

配置快照在snapshots配置区域下

rdb保存的文件都是dump.rdb  都是在我们的配置文件中进行配置的！！！

 ![image-20211204184151051](C:\Users\Sire\AppData\Roaming\Typora\typora-user-images\image-20211204184151051.png)

可以通过如下命令获取  dump.rdb 位置

```bash
127.0.0.1:6379> CONFIG GET dir
1) "dir"
2) "/usr/local/bin"
```

 ![image-20211204232500582](C:\Users\Sire\AppData\Roaming\Typora\typora-user-images\image-20211204232500582.png)

- 触发机制

  - save规则触发
  - 执行flushall命令
  - 关闭redis

- 备份会自动生成dump.rdb文件

- #### 如何恢复备份文件

  只要将rdb文件放在redis规定的目录，redis启动时会自动检查dump.rdb文件恢复数据

  查看位置，config get dir

  在生产环境中最好对dump.rdb文件进行备份

- #### RDB优缺点

  **优点：**

  - 父进程正常处理用户请求，fork分支一个子进程进行备份
  - 适合大规模的数据恢复，如果服务器宕机了，不要删除rdb文件，重启自然在目录下，自动会读取

  **缺点：**

  - 需要一定的时间间隔，可以自行修改设置
  - 如果redis意外宕机，最后一次的修改数据会丢失
  - fork进程的时候，会占用一定的内存空间



#### 2、AOF(Append Only File)

将所执行的所有命令都记录下来，处读操作以外，恢复时重新执行一次，如果是大数据就需要写很久

aof默认是文件无限追加，大小会不断扩张

在主从复制中，rdb是备用的，在从机上使用，aof一般不使用

 ![image-20211204232947836](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211222125413.png)

1. fork分支出子进程
2. 根据内存中的数据子进程创建临时aof文件
3. 父进程执行的命令存放在缓存中，并且写入原aof文件
4. 子进程完成新aof文件通知父进程
5. 父进程将缓存中的命令写入临时文件
6. 父进程用临时文件替换旧aof文件并重命名
7. 后面的命令都追加到新的aof文件中

- ### 开启AOF

  ![image-20211204215527176](C:\Users\Sire\AppData\Roaming\Typora\typora-user-images\image-20211204215527176.png)

  配置文件Append Only Modo区块中设置

  ```bash
  appendonly no
  #默认关闭appendonly 手动设置yes开启
  
  appendfilename "appendonly.aof"
  #默认名字
  
  # appendfsync always
  appendfsync everysec
  # appendfsync no
  #每次都进行修改
  #每秒钟都进行修改
  #不进行修改
  
  no-appendfsync-on-rewrite no
  #是否进行重写
  
  auto-aof-rewrite-percentage 100
  auto-aof-rewrite-min-size 64mb
  #percentage重写百分比
  #重写时文件最小的体积
  
  
  #一般保持默认，一般只需要开启
  
  ```

  **这些配置也能在连接redis后在redis中通过config set 进行更改**

![image-20211204235834311](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211222125419.png)

与RDB类似的触发机制，也能生成配置文件

![image-20211204235900341](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211222125425.png)

进行了一些操作，如list在同一个key上覆盖值操作，aof是一同操作的，把之前的值进行了覆盖，但是保存的并不是最新的值，而是把全部进行的操作保存了下来，lpush lpop，当从aof文件中恢复数据时，不管最新的值是什么都重新的进行一遍操作，这样在时间上和效率上并不是最优的，但是能保证在每次的操作能进行备份，保证数据不丢失，如果出于绝对的安全考虑可以开启aof

 ![image-20211205000045192](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211222125429.png)

- ### aof文件损坏情况

  - 人为测试aof文件损坏，aof文件是根据文件的大小进行比对，判断文件是否损坏，使用

  - ```bash
    redis-check-aof --fix /usr/local/var/db/redis/appendonly.aof 
    AOF analyzed: size=23, ok_up_to=23, diff=0
    AOF is valid
    ```

  - 损坏的aof会导致redis无法打开

  - 这个修复真垃圾，给我数据删没了，删除规律数据不好修复，但是加入明显没有逻辑的错误，还是能修复

  - redis-check-rdb 能修复rdb文件

- ### 优缺点

  **优点：**

  - 可设置文件修改每次都同步备份，文件完整性更好，但是消耗性能
  - 设置每秒同步一次可能会丢失一秒的数据
  - 从不同步效率最高

  **缺点**

  - 对于数据文件，aof远远大于rdb，修复速度也比rdb慢
  - aof是io操作，所以默认是aof
  - aof文件会无限扩大

### 9.3、Redis发布订阅

Redis 发布订阅 (pub/sub) 是一种消息通信模式：发送者 (pub) 发送消息，订阅者 (sub) 接收消息。

Redis 客户端可以订阅任意数量的频道。

下图展示了频道 channel1 ， 以及订阅这个频道的三个客户端 —— client2 、 client5 和 client1 之间的关系：

 ![image-20211205160920694](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211205160920.png)

当有新消息通过 PUBLISH 命令发送给频道 channel1 时， 这个消息就会被发送给订阅它的三个客户端：

 ![image-20211205160939629](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211205160939.png)

 ![image-20211205160953429](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211205160953.png)

> ==测试==

订阅端:

```bash
127.0.0.1:6379> SUBSCRIBE keaifa # 订阅一个频道 keaifa
Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "keaifa"
3) (integer) 1
# 等待读取推送的信息
1) "message" # 消息
2) "keaifa"  # 频道 channel
3) "001"     # 消息的具体内容 
1) "message"
2) "keaifa"
3) "hello"
```

发送端：

```bash
127.0.0.1:6379> PUBLISH keaifa 001 # 发布者发送消息到频道！
(integer) 1
127.0.0.1:6379> PUBLISH keaifa hello # 发布者发送消息到频道！
(integer) 1
```

 ![image-20211205160244682](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211205160251.png)

**使用场景：**

- 实时消息系统
- 实时聊天系统（频道当做聊天室）
- 订阅，关注系统都是可以的

稍微复杂的就需要使用消息中间件（MQ等）来实现！

### 9.4、Redis主从复制（重点）

一个Master有多个slave，将一台redis服务器数据，复制到其他的redis服务器，前者称为主节点（master、leader），后者称为从节点（slave、follower），数据是单向的，只能从主节点到从节点，Master以写为主，Slave以读为主

#### 1、环境配置

只配置从库，不配置主库！

```bash
127.0.0.1:6379> info replication # 查看当前库的信息
# Replication
role:master # 角色
connected_slaves:0 # 从机
master_failover_state:no-failover
master_replid:6c8092ab314dfa23c6f02a957e61662cdb7a0bd9
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0

```

复制三个配置文件，然后修改对应的信息

1. 端口

2. pid 名字

3. log 文件名字

4. dump.rdb 名字

   修改完毕后，启动三个集群服务（单机多服务）

    ![image-20211205171450486](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211205171450.png)

#### 2、一主二从

   ==默认情况下，每台Redis服务器都是主节点==

我们一般情况下只用配置从机即可！

认老大！一主（79） 二从（80/81）

```bash
127.0.0.1:6380> SLAVEOF 127.0.0.1 6379  # SLAVEOF host 6379 找老大
OK
127.0.0.1:6380> info replication
# Replication
role:slave   # 当前角色  从机
master_host:127.0.0.1
master_port:6379
master_link_status:up
master_last_io_seconds_ago:4
master_sync_in_progress:0
slave_read_repl_offset:0
slave_repl_offset:0
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:2ccb16adcafdfbefff6ceb3fbf104173a1536bb0
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:0

#  在主机中查看
127.0.0.1:6379> info replication
# Replication
role:master
connected_slaves:1  # 从机的信息
slave0:ip=127.0.0.1,port=6380,state=online,offset=14,lag=1
master_failover_state:no-failover
master_replid:2ccb16adcafdfbefff6ceb3fbf104173a1536bb0
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:14
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:14

```

如果两个都配置完的话，就会有两个从机的

真实的从机配置是在配置文件中进行的（永久的），命令行是暂时的的

> ==细节了解==

主机可以写（主要，也可以读的），从机只能读（不能写）！主机中所有的信息与数据，都会被从机复制与保存！

> ==测试==

主机断开操作，主机依旧连接到主机的，但是没有写操作了，

如果是使用命令行配置的，主从配置，这个时候如果重启了，就会变成主机，只要变为从机，立刻就可以获取主机的内容！

> ==主从复制原理==

- slave启动成功连接到master后会发送一个sync同步命令

- master接到命令，启动后台的存盘进程，同时收集所接收到的用于修改数据集命令，后台执行完毕之后，master将传送整个数据文件到slave，并完成一次同步，成为增量复制
  专有名词

  - 全量复制

    slave服务在接受到数据库文件数据后，将其存盘并加载到内存中

  - 增量复制

    master继续将新的所有收集到的修改命令依次传给slave，完成同步

- 只要重新连接master，一次完全同步（全量复制）将被自动执行，数据一定能在从机中看到

  ​	

> ==层层链路==

上一个M连接下一个S

 ![image-20211205181130068](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211205181130.png)

  这时候我们也可以完成我们的主从复制！

如果没有老大了，我们可以手动选择一个出来

==谋朝篡位==

如果主机断开了连接，我们就可以使用 SLAVEOF no one 让自己变为主机！其他的节点就可以手动连接到这个新的主节点（手动！），这时候老大就算修复了，那就得重新连接才行

#### 3、哨兵模式

（自动选择老大）

 ![image-20211205184928113](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211205184928.png)





> ==测试==

一主二从！

1. 配置哨兵配置文件 sentinel.conf

   ```bash
   # sentinel monitor 被监控的名称 host port 1
   sentinel monitor myredis 127.0.0.1 6379 1
   ```

   最后的数字 1 ， 代表主机挂了，slave投票看让谁接替成为主机，票数最多的，就会成为主机！

2. 启动哨兵！

   ```bash
   # 启动！
   redis-sentinel myredisconfig/sentinel.conf
   
   [root@VM-24-7-centos /]# redis-sentinel myredisconfig/sentinel.conf 
   570:X 05 Dec 2021 19:03:33.939 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
   570:X 05 Dec 2021 19:03:33.939 # Redis version=6.2.6, bits=64, commit=00000000, modified=0, pid=570, just started
   570:X 05 Dec 2021 19:03:33.939 # Configuration loaded
   570:X 05 Dec 2021 19:03:33.940 * monotonic clock: POSIX clock_gettime
                   _._                                                  
              _.-``__ ''-._                                             
         _.-``    `.  `_.  ''-._           Redis 6.2.6 (00000000/0) 64 bit
     .-`` .-```.  ```\/    _.,_ ''-._                                  
    (    '      ,       .-`  | `,    )     Running in sentinel mode
    |`-._`-...-` __...-.``-._|'` _.-'|     Port: 26379
    |    `-._   `._    /     _.-'    |     PID: 570
     `-._    `-._  `-./  _.-'    _.-'                                   
    |`-._`-._    `-.__.-'    _.-'_.-'|                                  
    |    `-._`-._        _.-'_.-'    |           https://redis.io       
     `-._    `-._`-.__.-'_.-'    _.-'                                   
    |`-._`-._    `-.__.-'    _.-'_.-'|                                  
    |    `-._`-._        _.-'_.-'    |                                  
     `-._    `-._`-.__.-'_.-'    _.-'                                   
         `-._    `-.__.-'    _.-'                                       
             `-._        _.-'                                           
                 `-.__.-'                                               
   
   ```

   如果主节点（Master）宕机，这时候会有一个随机投票算法（选出新的主节点）！

    

   **哨兵日志**

   

   ![image-20211205190807228](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211205190807.png)

   此时如果主机回来了，只能归并到新的主机下，当做从机，这就是哨兵模式的规则！

3. 优点：

   - 哨兵集群，基于主从复制模式，所有的主从配置优点，他全有！
   - 主从可以切换，故障可以转移，系统的可用性就会更好
   - 哨兵模式就是主从复制的升级版，手动到自动！

4. 缺点：

   - Redis 不好在线扩容！集群容量一旦到达上限，在线扩容就十分的麻烦！
   - 实现哨兵模式的配置其实是很麻烦的，里面有很多的选择！

### 9.5、Redis缓存穿透和雪崩（面试高频，工作常用！）

都是服务的三高问题

- 高并发
- 高可用
- 高性能

面试高频，工作常用

redis缓存的使用极大的提升了应用程序的性能和效率，特别是数据查询方面，但同时，它也带来了一些问题，数据一致性问题，严格意义上来讲，问题无解，对一致性要求极高，不推荐使用缓存

布隆过滤器、缓存空对象

> ==缓存穿透==

用户查询一个数据，redis数据库中没有，也就是缓存没命中，于是向持久层数据库查询，发现也没有，于是查询失败，用户很多的时候，缓存都没有命中，都请求持久层数据库，给持久层数据库造成巨大压力，称为缓存穿透

在直达持久层的路径上加上过滤器、或者缓存中专门增加一个为空的请求

> ==布隆过滤器==

- 布隆过滤器是一种数据结构，对所有可能的查询参数以hash形式存储，在控制层进行校验，不符合则丢弃，从而避免了对底层存储系统查询压力

 ![image-20201130145545450](https://img-blog.csdnimg.cn/img_convert/82edbb68c3a5528567a440c653dcefc1.png)

> ==缓存空对象==

- 当持久化层不命中后，将返回的空对象存储起来，同时设置一个过期时间，之后再访问这个数据就从缓存中获取，保护持久层数据源

 ![image-20211205213404235](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211205213404.png)

- 需要面临的问题
  - 存储空的key也需要空间
  - 对空值设置了过期时间，还会存在缓存层和存储层的数据有一段时间窗口不一致，对于需要保持一致性的业务会有影响

> ==缓存击穿==

例子微博服务器热搜，巨大访问量访问同一个key

一个key非常热点，不停扛着大并发，集中对一个点进行访问，当个key失效的瞬间，持续大并发导致穿破缓存，直接请求数据库

某个key在过期的瞬间，大量的访问会同时访问数据库来查询最新的数据，并且回写缓存，导致数据库瞬间压力过大

> ==解决方案==

- 设置热点数据不过期
  - 一直缓存也会浪费空间
- 加互斥锁
  - 分布式锁：使用分布式锁，保证对于每个key同时只有一个线程查询后端服务，其他线程没有获得分布式锁的权限，只需要等待即可，这种方式将高并发的压力转移到了分布式锁，因此对分布式锁的考验很大

> ==缓存雪崩==

在某一个时间段，缓存集中过期失效，redis宕机

产生雪崩的原因之一，设置缓存的存活时间较短，大并发访问时刚好都过期，直接访问了数据库，对数据库而言，会产生周期性压力波峰，暴增时数据库可能会宕机

双十一时会停掉一些服务，保证主要的一些服务可用，springcloud中说明过

 ![image-20211205213536064](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211205213536.png)

> ==解决方案==

- 增加集群中服务器数量
  - 异地多活
- 限流降级
  - 缓存失效后，通过加锁或者队列来控制读数据库写缓存的线程数量，对某个key只允许一个线程查询数据和写缓存，其他线程等待
- 数据预热
  - 正式部署之前，把可能的数据提前访问一遍，可能大量访问的数据就会加载到缓存中，加载不同的key，设置不同的过期时间，让缓存时间尽量均匀
