##  一、NoSQL简介

### 1.1、为什么要使用NoSQL？

> ==1、单机Mysql时代==

![image-20211120214317631](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211120214325.png)

90年代,一个网站的访问量一般不会太大，单个数据库完全够用。随着用户增多，网站出现以下问题

1. 数据量增加到一定程度，单机数据库就放不下了
2. 数据的索引（B+ Tree）,一个机器内存也存放不下
3. 访问量变大后（读写混合），一台服务器承受不住。

> ==2、Memcached（缓存）+ Mysql + 垂直拆分（读写分离）==

网站80%的情况都是在读，每次都要去查询数据库的话就十分的麻烦！所以说我们希望减轻数据库的压力，我们可以使用缓存来保证效率！

![image-20211120214528890](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211120214529.png)

优化过程经历了以下几个过程：

1. 优化数据库的数据结构和索引(难度大)
2. 文件缓存，通过IO流获取比每次都访问数据库效率略高，但是流量爆炸式增长时候，IO流也承受不了
3. MemCache,当时最热门的技术，通过在数据库和数据库访问层之间加上一层缓存，第一次访问时查询数据库，将结果保存到缓存，后续的查询先检查缓存，若有直接拿去使用，效率显著提升

> ==3、分库分表 + 水平拆分 + Mysql集群==

 ![image-20211120214748163](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211120214748.png)

> ==4、如今最近的年代==

 如今信息量井喷式增长，各种各样的数据出现（用户定位数据，图片数据等），大数据的背景下关系型数据库（RDBMS）无法满足大量数据要求。Nosql数据库就能轻松解决这些问题。

> ==目前一个基本的互联网项目==

 ![image-20211120214954423](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211120214954.png)

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

 ![image-20211122204054985](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211122204055.png)

存储的是关系

- 不是用来存放图形的，是用来存储关系的，朋友圈社交，广告推荐
- **Neo4j**，InfoGrid



 ![image-20211122203926489](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211122203933.png)

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

   ![image-20211122224833290](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211122224833.png)

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

   ![image-20211122225232578](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211122225232.png)

- 关闭redis

  ```bash
  shutdown
  exit
  ```

   ![image-20211122225522299](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211122225522.png)


### 2.3、Redis的压力测试

菜鸟教程：https://www.runoob.com/redis/redis-benchmarks.html

 ![image-20211123164703942](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211123164711.png)

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
GET key value

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
127.0.0.1:6379> mset user:1:name fafa user:1:age 21
OK
127.0.0.1:6379> mget user:1:name
1) "fafa"
127.0.0.1:6379> mget user:1:name user:1:age
1) "fafa"
2) "21"
127.0.0.1:6379> 
```

 ![image-20211126160422768](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211126160432.png)

> ==小结==

String类似的使用场景：value除了是我们的**字符串**还可是**数字**

-  计数器
-  统计多单位的数量 uid :id:follow:number
-  粉丝数
-  对象存储



### 3.3、List

基本的数据类型，列表

 ![image-20211129173456369](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211129173503.png)

在redis里面，我们可以把redis玩成，栈，队列，阻塞队列！

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
微博，B站，全民（共同关注）

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

































































