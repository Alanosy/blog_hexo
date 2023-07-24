## NoSQL数据库简介





![截屏2023-07-16 11.31.57](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-16 11.31.57.png)

![截屏2023-07-16 11.29.31](/Users/alan/Desktop/截屏2023-07-16 11.29.31.png)



![截屏2023-07-16 11.32.24](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-16 11.32.24.png)、



**NoSQL数据库概述**

nosql不仅仅是sql，泛指**非关系性数据库**

noSQL不依赖业务逻辑方式存储，而是简单的key-value模式存储，增加了数据库扩展能力

* 不遵循sql标准

* 不支持ACID（事物四特性）

* 远超于SQL的性能

**NoSQL适用场景**

* 对数据高并发的读写

* 海量数据的读写

* 对数据高可扩展性的

不适用场景

* 需要事物支出
* 基于sql的结构化查询存储，处理复杂的关系，需要即席查询
* 用不着sql的和用了sql也不行的情况，就需要考虑NoSql



Memcache

Redis

MongoDb

![截屏2023-07-16 11.39.44](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-16 11.39.44.png)

![截屏2023-07-16 11.40.31](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-16 11.40.31.png)

行式数据库

![截屏2023-07-16 11.42.40](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-16 11.42.40.png)

列式数据库

![截屏2023-07-16 11.42.25](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-16 11.42.25.png)



图关系数据库



## Redis6概述和安装

c语言环境

make

make install

![截屏2023-07-16 11.45.46](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-16 11.51.56.png)





**前台启动**

Redis-server

**后台启动**

![截屏2023-07-16 11.54.52](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-16 11.54.52.png)





Redis-server /etc/redis.conf

**关闭**

* shutdown
* 杀进程



**相关知识**

默认端口号6379

默认提供16个数据库，下标从0开始，默认使用0号库

使用select <dbid>来切换数据库

统一密码管理，所有库同样密码

dbsize查看当前数据库的key的数量

flushdb清空当前数据库

flushall通杀全部库

单线程+多路IO复用（redis）

串行vs多线程+锁（memcached）vs单线程+多路IO复用（redis）



## 常用五大数据类型

#### String字符串

| 命令                      | 功能                                |
| ------------------------- | ----------------------------------- |
| keys *                    | 查看当前库所有key                   |
| Exists key                | 判断某个key是否操作                 |
| Type key                  | 查看key类型                         |
| Del key                   | 删除指定的key的数据                 |
| unlink key                | 根据value选择非阻赛删除（异步删除） |
| Expire key 10             | 为key设置过期时间                   |
| ttl key查看还有多少秒过期 | -1表示永不过期，-2表示已过期        |
| select                    | 切换数据库                          |
| dbsize                    | 查看当前数据库的key数量             |
| flushdb                   | 清空当前数据库                      |
| flushall                  | 清空所有数据库                      |

String字符串

String类型是二进制安全的。意味着redis的string可以包含任何数据，比如图片或者序列化的对象

String类型是redis最基本的数据类型，一个redis中字符串value最多可以是512M

常用命令

Set <key><value>添加键值对

*NX:当前数据库key不存在时，可将key-value添加数据库

*XX:当数据库中key存在时，可以将key-value添加数据库，与NX参数互斥

*EX:key的超市秒数

*PX:key的超时好描述，与EX互斥



Get <key>查询对应的值

Append <key> <value>将给定的<value>追加到原值的末尾

stglen <key>获得 值的长度

Setnx <key><value>只有key存在时，设置key的值

incr <key>

将key中存储的数字值增1

智能对数字值操作，如果为空新增为1

Dear <key>

将key中存储的数字值减1

智能对数字值操作，如果为空新增为-1





Incrby/decrby <key> <步长>将key中存储的数字的值增减。自定义步长

原子性：不会被线程调度机制打断的操作

所谓原子操作是指不会被线程调度机制打断的操作；+

这种操作一旦开始，就一直运行到结束，中间不会有任何 context switch（切换到另一个线程）。，

（1）在单线程中 ，能够在单条指令中完成的操作都可以认为是。“原子操作”，因为中断只能发生于指令之间。。

（2）在多线程中 ，不能被其它进程 （线程）打断的操作就叫原子操作。。

Redis 单命令的原子性主要得益于 Redis 的单线程。



Mset <key1><value1><key2><value2>....

同时设置一个或多个key-value对

mget <key1><key2>...

同时获取一个或多个value

msetnx <key1><value1><key2><value2>....

同时设置1个或多个key-value对，当且仅当多有给定key都不存在

原子性，有一个失败则都失败

Getrange <key><起始位置><value>

获取范围的值，类似java中的substring，前包，后包

Strange <key><起始位置><value>

用<value>覆写<key>所存储的字符串值，从<起始位置>开始（索引从0开始）

Setex <key><过期时间><value>

设置键值的同时，设置过期时间，单位秒

Getset <key><value>

以新换旧，设置了新值同时获得旧值

数据结构

String的数据结构为简单动态字符串（SDS）是可以修改的字符串，内部结构实现上类似于java的Arraylist，采用预分配冗余空间的方式来减少内存的频繁分配

内部为当前字符串实际分配的空间capacity一般要高于实际字符串长度len，当字符串长度小于1M时，扩容都是加倍现有的空间，如果超过1M，扩容时一次只会多扩容1M的空间。需要注意的是字符串最大长度是512M





#### list列表

**简介**

单键多值。

Redis 列表是简单的字符串列表，按照插入顺序排序。你可以添加一个元素到列表的头部（左边）或者尾部（右边）。

它的底层实际是个双向链表，对两端的操作性能很高，通过索引下标的操作中间的节点性能会较差。

**常用命令**

lputh/gpush skey ><value1><valuez><value3>…从左边/右边插入一个或多个值。。

pop/rpop <key>从左边/右边吐出一个值。值在键在，值光健亡

rpoplpush <key1><key2>从<key1>列表右边吐出一个值，插到<key2>列表左边。。

Irange <key> <start> <stop>

lrange key 0 -1

按照素引下标获得元素(从左到右)

lindex <key ><index>按照索引下标获得元素(从左到有)

llen <key>获得列表长度。

linsert <key＞before <value> <newvalue>在<value>的前面插入<newvalue>插入值

lrem <key><n><value>从左边删除n个value(从左到右)

Iset<key><index><value>将列表 key 下标为 index的值替换成 value

**数据结构**

List 的数据结构为快速链表 quickList。 +

首先在列表元素较少的情况下会使用一块连续的内存存储，这个结构是 ziplist ，也即是压缩列表。

它将所有的元素紧挨着一起存储，分配的是一块连续的内存。

当数据量比较多的时候才会改成 quicklist。 

因为普通的链表需要的附加指针空间太大，会比较浪费空间。比如这个列表里存的只是int 类型的数据，结构上还需要两个额外的指针 prer 和 next.

Redis 将錠表和 ziplist結合起来成了 quicklist。地就是将多个 ziplist使用双向指

针串起来使用。这样既满足了快速的插入删除性能，又不会出现太大的空间元余。



#### set集合

**常用命令**

sadd <key ><value1> <value2> ....

将一个或多不 member 元素加入到集合 key 中，已经存在的 member 元素将被忽略。

smembers <key>取出该集合的所有值。。

sismember <key ><value>判断集合<key>是否为含有该<value>值，有1，没有0

scard <key>返回该集合的元素个数。

srem <key><value1><value2>....删除集合中的某个元素。

spop ＜key>随机从该集合中吐出一个值。。

srandmember <key><n>随机从该集合中取出 n个值。不会从集合中删除。。

smove <source> <destination>value 把集合中一个值从一个集合移动到另一个集合，

sinter <key1> <key2>返回两个集合的交集元素。

sunion <key1> <key2>返回两个集合的井集元素。

sdiff<key1> <key2>返回两个集合的差集元素（key1 中的、不包合key2中的）



数据结构

Java中Hashset的内部实现使用的是 Hasthap，只不过所有的value都指向同一个对象。

Redis 的set 结构也是一样，它的内部也使用hash结构，所有的value 都指向同一个内

部值

#### hash哈希

Redis hash 是一个键值对集合。。

Redis hash 是一个 string 类型的 field 和 value 的映射表，hash 特別造合于存储対象。

类似 Java 里面的 Map<String. Object>

用户1D为查找的key，存储的value 用户对象包合姓名，年齡，生日等信息，如果用

普通的key/value 结构来存储

**常用命令**

hset <key><field><value>给(key>集合中的 <field>键赋值<value>

hget <key1><field> 从<key1>集合<field>取出 value

hmset <keyl><fieldl><valuel><field2><value2>...批量设置 hash 的值

hexists <keyI><field>查看哈希表key中，给定域field是否存在。

hkeys <key>列出 hash 集合的所有 field

hvals <key>列出核 hash 集合的所有 value

hinerby <key><field><increment>为哈希表key 中的域 field 的値加上増量 1 -1,可以的设置要加上的值

hsetnx  <key><field><value>将哈希表 key 中的域field 的值设置为 value，当且仅当域

field 不存在

**数据结构**

Hash 类型对应的数据结构是两种：ziplist（压缩列表)，hashtable（哈希表)。当

field-value 长度较短且个数较少时，使用ziplist，否则使用 hashtable。

#### Zset有序集合

Redis 有序集合 zset 与普通集合 set 非常相似，是一个没有重复元素的字符串集合。

不同之处是有序集合的每个成员都关联了一个评分（score），这个评分(score）被用来按照从最低分到最高分的方式排序集合中的成员。集合的成员是唯一的，但是评分可以是重复了。

因为元素是有序的，所以你也可以很快的根据评分（score）或者次序（position ） 来获

取一个范国的元素。

访问有序集合的中间元素也是非常快的,因此你能够使用有序集合作为一个没有重复成员的智能列表。

**常用命令**

zadd <key><scorel><valuel><scorez><value2>

将一个或多个member 元素及其score值加入到有序集 key 当中

zrange <key><start><stop> [WITHSCORES]

返回有序集 key 中，下标在<start><stop>之间的元素

带 WITHSCORES，可以让分数一起和值返回到结果集

zrangebyscore key min max [withscores] [limit offset count]

返回有序集 key 中，所有score 值介于 min 和max之间(包括等于min 或max）的成员。

有序集成员按 score 值递增(从小到大次序排列。

zrevrangebyscore key maxmin [withscores] [limit offset count]

同上，改为从大到小排列。。

zincrby <key > <increment> <value>

为元素的score 加上增量

zrem <key><value>删除该集合下，指定值的元素，

zcount <key><min><max>统计该集合，分数区间内的元素个数。

zrank <key><value>返回该值在集合中的排名，从0开始。。

**数据结构**

Sortedset (zset)是 Redis 提供的一个非常特别的数据结构，一方面它等价于 Jaxa

的数据结构Ma西<String, Double》，可以给每一个元素 vlue 赋子一个权重 score，另一方面它又类似于 TseeSet，内部的元素会按照权重 score 进行排序，可以得到每元素的名次，还可以通过 score 的范国来获取元素的列表。。

zset 底层使用了两个数据结构。

(1）hash ,hash 的作用就是关联元素 value 和权重 score，保障元素 value 的唯一性，可以通过元素 value 找到相应的 score 值。。

(2）跳跃表，跳跃表的目的在于给元素 value 排序，根据 score 的范围获取元素

列表。

3.6.4.

1、 简介

有序集合在生活中比较常见，例如根据成绩对学生排名，根据得分对玩家排名等。对于有序集合的底层实现，可以用数组、平衡树、链表等。数组不便元素的插入、删除；平衡树或红黑树星然效率高但结构复杂；链表查询需要遍历所有效率低。Redis

采用的是跳出表。跳跃表效车雄士七红黑树 ，夹现远比红黑树简单。

2、实例

对比有序链表和跳跃表，从链表中查询出 51。

（1）有序链表。



## Redis6配置文件详解

第一部分单位设置，不区分大小写，只支持byte

![截屏2023-07-17 14.08.26](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.08.26.png)

第二部分，包含部分，可以包含其他文件中内容

![截屏2023-07-17 14.08.59](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.08.59.png)

第三部分，网络部分

![截屏2023-07-17 14.11.25](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.11.25.png)

![截屏2023-07-17 14.11.38](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.11.38.png)

![截屏2023-07-17 14.12.16](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.12.16.png)





开启保护模式

只能本机访问，不能远程访问



端口号

![截屏2023-07-17 14.13.38](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.13.38.png)



![截屏2023-07-17 14.13.47](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.13.47.png)

![截屏2023-07-17 14.15.23](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.15.23.png)

太久没有操作，过来时间需要重新连接

0，用不超时

以秒为单位

![截屏2023-07-17 14.16.35](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.16.35.png)

很长时间没有操作，这个是心跳时间，检查是否还在操作，检测周期为300

![截屏2023-07-17 14.18.29](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.18.29.png)

后台启动

![截屏2023-07-17 14.18.44](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.18.44.png)

把每次的进程号保存到文件中



![截屏2023-07-17 14.19.16](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.19.16.png)

设置日志级别

debug能看到更详细的信息

verbose一些有用的信息

notice生产环境用

warning显示重要的信息

![截屏2023-07-17 14.20.49](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.20.49.png)



设置文件的输出路径![截屏2023-07-17 14.21.14](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.21.14.png)

默认16个库



![截屏2023-07-17 14.22.30](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.22.30.png)

![截屏2023-07-17 14.22.39](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.22.39.png)







![截屏2023-07-17 14.22.45](/Users/alan/Library/Application Support/typora-user-images/截屏2023-07-17 14.22.45.png)



































































## Redis6的发布和订阅

## Redis6新数据类型

## Jedis操作Redis6

## Redis6与Springboot整合

## Redis6的事物操作

## Redis6持久化之RDB

## Redis6持久化之AOF

## Redis6的主从复制

## Redis6集群

## Redis6应用问题解决

## Redis6新功能

