# Redis

[TOC]

> REmote DIctionary Server(Redis) 是一个由Salvatore Sanfilippo写的key-value存储系统。
>
> Redis是一个开源的使用ANSI C语言编写、遵守BSD协议、支持网络、可基于内存亦可持久化的日志型、Key-Value数据库，并提供多种语言的API。
>
> 它通常被称为**数据结构服务器**，因为值（value）可以是 字符串(String), 哈希(Hash), 列表(list), 集合(sets) 和 有序集合(sorted sets)等类型。



#### 命令

**在redis客户端，输入命令都会在后面进行提示，关键字为命令的第一个单词**

- redis-server.exe

  启动服务，配置redis-cli.exe -h 127.0.0.1 -p 6379

- $ redis-cli

  使用客户端，远程服务器上运行：$ redis-cli -h host -p port -a password	

- **config get */loglevel**

​	获取配置信息

- config set loglevel "内容"

  设置配置信息，本质上是修改` redis.conf `文件内容

- del key [key ...] 删除key

- exists key [key ...] 是否存在key

- dump key 序列化key，并返回被序列化的值

  ```
  127.0.0.1:6379> set dump1 v1
  OK
  127.0.0.1:6379> dump dump1
  "\x00\x02v1\a\x00\xa0\xd7e\xad\xc3\x9a\xacA"
  ```

- expire key seconds：设置key过期时间

- expireat key timestamp：以时间戳的形式设置过期时间

- persist key：移除过期

- RENAME key newkey ：重命名key

- type key：获得类型

  更多命令，参考[runoob.com](http://www.runoob.com/redis/redis-commands.html)



#### 数据类型

String， hash，list，set，sorted set有序集合

**String**

关键字：set / get

```
# 通过set来设置，key和value是变的
set key value [EX seconds] [PX milliseconds] [NX|XX]
get key # 获取key的值
```

**Hash**

关键字： hset / hmset / hget / hmset，适合用于存储对象。为一个Key一次设置多个哈希键/值

```
hset key field value
hget key field
一次设置多个
hmset key field value [field value ...]
hmget key field [field ...]
```

**List**

关键字：lpush /lrange，重复了会覆盖

```
# 一个key后面可以添加多个值
lpush key value [value ...]
# 遍历key，需要指定开始和结束的索引，默认从0开始
lrange key start stop
```

**Set**

集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是O(1)。

关键字：sadd / smembers，如果有重复则忽略不插入

```
sadd key member [member ...]
smembers key
```

**zset**

sorted set有序集合

关键字： zadd /zrange，**如果要插入的下标有数据了，则插入到尾部，**如果遍历的index超出了范围则会自动打印全部

```
# score member 下标	
zadd key [NX|XX] [CH] [INCR] score member [score member ...]
例如：
zadd k 0 v1
zadd k 1 v2
zadd key 下标 value

```





