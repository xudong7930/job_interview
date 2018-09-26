#redis面试题 #

# 
1. 使用Redis有哪些好处？
答： 
	速度快，因为数据存在内存中
	支持丰富数据类型，支持string，list，set，sorted set，hash
	支持事务，操作都是原子性，所谓的原子性就是对数据的更改要么全部执行，要么全部不执行
	丰富的特性：可用于缓存，消息，按key设置过期时间，过期后将会自动删除

2. redis相比memcached有哪些优势？
答：
	1. memcached支持字符串，redis支持更加能丰富的数据类型
	2. redis的速度比memcached快很多
	3. redis可以持久化其数据


3. redis常见性能问题和解决方案
答：
	(1) Master最好不要做任何持久化工作，如RDB内存快照和AOF日志文件
	(2) 如果数据比较重要，某个Slave开启AOF备份数据，策略设置为每秒同步一次
	(3) 为了主从复制的速度和连接的稳定性，Master和Slave最好在同一个局域网内
	(4) 尽量避免在压力很大的主库上增加从库
	(5) 主从复制不要用图状结构，用单向链表结构更为稳定。 即：Master <- Slave1 <- Slave2 <- Slave3...
这样的结构方便解决单点故障问题，实现Slave对Master的替换。如果Master挂了，可以立刻启用Slave1做Master，其他不变


4. reids的5种数据类型
	答： Redis支持五种数据类型：string（字符串），hash（哈希），list（列表），set（集合）及zset(sorted set：有序集合)。

		key键: 一个键最大能存储512MB


5. Memcache与Redis的区别都有哪些？
答： 
	1)、存储方式
		Memecache把数据全部存在内存之中，断电后会挂掉，数据不能超过内存大小。
		Redis有部份存在硬盘上，这样能保证数据的持久性。

	2)、数据支持类型
		Memcache对数据类型支持相对简单。
		Redis有复杂的数据类型。
	
	3)、使用底层模型不同
		它们之间底层实现方式 以及与客户端之间通信的应用协议不一样。
		Redis直接自己构建了VM机制 

	4），value大小
		redis最大可以达到1GB，而memcache只有1MB

6. redis最适合的场景?
	1.会话缓存（Session Cache）
	2.全页缓存（FPC）
	3.队列
	4.排行榜/计数器
	5.发布/订阅


7. MySQL里有2000w数据，redis中只存20w的数据，如何保证redis中的数据都是热点数据

	限定 Redis 占用的内存，Redis 会根据自身数据淘汰策略，加载热数据到内存。所以，计算一下 20W 数据大约占用的内存，然后设置一下 Redis 内存限制即可。
