## redis-command

`by enginning 191207`



### installation

```shell
# mac: make and link
brew install redis
```



### serve

```shell
redis-server
redis-cli
```



### intruduction



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

 一个 k-v 对**集合**， string 类型的 field 和 value 的**映射表**

```shell
# 每个 hash 可以存储 2^32 -1 个键值对 
HMSET key field1 value1 filed2 value2 ...
HGET key fieldn
```



#### List

简单的**双向字符串列表**，按照插入顺序排序

```shell
# 每个列表最多可存储 2^32 - 1 元素
lpush list_name value
```



#### Set

Set 是 **string** 类型的**无序集合**

集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)

```shell
# 添加一个 string 元素到 key 对应的 set 集合中，成功返回 1，如果集合中存在返回 0
sadd key member
# 列出
smembers key
```

