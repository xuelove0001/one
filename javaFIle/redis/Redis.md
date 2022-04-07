Redis 

Nosql概述
我们现在处于

特点：解耦

1.方便扩展(数据之间没有关系,很好扩展)

2.大数据量高性能(Redis一秒写8万次，读取11万次)

3.数据类型是多样型的！（不需要事先设计数据库！随去随用！如果设计数据量十分大的表，无法设计了）

4，不仅仅是数据，没有固定的查询语言，键值对存储，列存储，文档存储，图形数据库(社交关系)

redis能干嘛？

1.内存存储、持久化、内存中是断电即失，所有说持久化很重要(rdb、aof)

2.效率高，可以用于高速缓存

3.发布订阅

4.地图信息分析

5.计时器，计数器(浏览量！！1)

特性

1、多样的数据类型

2、持久化

3、集群

4、事务

Redis的实现单线程：明白Redis是很快的，官方是基于内存操作，cpu不是Redis性能瓶颈、Redis的瓶颈是根据机器的内存和网络带宽、既然可以使用单线程来实现、就使用单线程了！所有就使用了单线程了

三：Redis 命令

​	1.expire name 10 设置10秒销毁name;

​	2.ttl name 可以查看 name 的剩余的时间

```xml
key* 查看所有的 key 
exists name 查看当前的key是否存在。
move name 1 移除当前的key 
type name  查看当前的类型 
flushdb 清空设置
```

四：String

```bash
append key value 追加一个字符串
strlen key       获取字符串的长度
incr key         可以自动加一
decr key		可以自动减一
incrby key int   直接加值
indecr key int   直接减值
getrange key 0  length 可以获取0到length的长度范围
setrange key 1 xx 可以把字符串为1的位置替换为xx
setex(set with expire) #设置过期时间
setnx(set if not exist) #不存在在设置(在分布式锁中会常常使用！）
mset key1 v1 k2 v2 k3 v3 可以设置多个值
mget k1 k2 k3            获取多个值
msetnx      			是一个原子性的操作,要么一起成功，一起失败
#对象
set user:1 {name:zhangsan,age:3}	#设置一个user:1对象值为json字符来保存一个对象！
getset db 	redis					#如果不存在值,则返回nil
get db 								#
getset db mongodb					#如果存在值、获取原来的值、并设置新的值
get db								#获取get的值
```

List

```bash
基本的数据类型、列表
在redis里面、我们可以把list玩成、栈、队列、阻塞队列！
lpush list one					#将一个值或者多个值,插入到列表头部(左)
Rpush list value 				#将一个值或多个值，插入到列表的尾部右边
LRANGE list 0 -1 				#取值范围（0 -1）
Lpop							#移除列表的第一个元素
Rpop							#移除列表的最后一个元素
lindex list	1							#通过下标的获取得list中的某一个值！
Llen list								#获取List中的长度
Lrem list 1 							#移除指定的值
```

