## redis-command

`by enginning 191207`

> ref：<a href="https://www.runoob.com/redis/redis-tutorial.html" target="_blank">redis命令参考</a>



### command

#### String

```shell
# string
# 可以包含任何数据，每个键最大存512MB数据

# 设置 key 的值
set key value
# 获取 key 的值
get key
# 查看此 key 是否存在
exists key 
# 查看所有的 key
keys *
# 消除所有的 key
flushall
# 删除 key
del key
```



#### Hash

 一个 k-v 对**集合**， string 类型的 field 和 value 的**映射表(Map)**

使用场景：存储、读取、修改用户属性

```shell
# 每个 hash 可以存储 2^32 -1 个键值对 
HMSET key field1 value1 filed2 value2 ...
HGET key fieldn
```



#### List

简单的**字符串列表(双向链表)**，按照插入顺序排序，提供了操作某一段元素的API

使用场景：最新消息排行、消息队列

```shell
# 每个列表最多可存储 2^32 - 1 元素
lpush list_name value
```



#### Set

Set 是 **string** 类型的**无序集合**

集合是通过**哈希表实现**的，所以添加，删除，查找的复杂度都是 O(1)，为集合提供了求交、并、差等操作

使用场景：共同好友 、利用唯一性，统计访问网站的所有独立ip 、好友推荐时，根据tag求交集



原文中说，**集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是O(1)**其实不太准确。

其实在redis sorted sets里面当items内容大于64的时候同时使用了hash和skiplist两种设计实现。这也会为了排序和查找性能做的优化。所以如上可知： 

添加和删除都需要修改skiplist，所以复杂度为O(log(n))。 

但是如果仅仅是查找元素的话可以直接使用hash，其复杂度为O(1) 

其他的range操作复杂度一般为O(log(n))

当然如果是小于64的时候，因为是采用了ziplist的设计，其时间复杂度为O(n)

```shell
# 添加一个 string 元素到 key 对应的 set 集合中，成功返回 1，如果集合中存在返回 0
sadd key member
# 列出
smembers key
```



#### Zset

zset(**sorted** set)是**string**类型元素的**有序集合**

与**set**不同的是，每个元素都会关联一个double类型的分数(可重复)，按该分数从小到大进行排序

使用场景：排行榜 、带权重的消息队列

```shell
# 添加元素到集合，元素在集合中存在则更新对应score
zadd key score member
```





### installation

```shell
# mac: make and link
brew install redis
```



### serve

```shell
redis-server
redis-cli
# 有时候会有中文乱码，加上raw可以避免中文乱码
redis-cli --raw
# 在远程服务上执行命令
redis-cli -h host -p port -a password
```



### intruduction

