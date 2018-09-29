#排行榜统计 sql
```
订单表有如下字段 id 自增id user_id 购买者id product_id 商品id time 购买时间 price 订单总价 找出销量大于1000的商品，按销量倒序 和 找出消费最多的10个用户

select product_id,count(*) s from orders group by product_id order by s having s>1000;

select user_id,sum(price) s from orders group by user_id order by s desc limit 10;
```

#sql注入是什么及如何预防sql注入？
```
1.占位符的方式，就是对sql语句进行预处理，然后执行sql语句
2、通过addslashes或者mysql_real_escape_string这两个函数对用户输入的值进行转义处理，把一些特殊的字符转义掉。
```

#3.MYSQL主从服务器，如果主服务器是innodb引擎,从服务器是myisam引擎，在实际应用中，会遇到什么问题？
```
完全没有经验……
```


#4.两台mysql服务器，其中一台挂了，怎么让业务端无感切换，并保证正常情况下讲台服务器的数据是一致的
```

```

#5.锁是怎么形成的呢？
```
比如有两个文件：a.php和b.php
a.php的操作是：先锁定A记录，然后再锁定B记录，只有锁住B记录才会释放A记录的锁
b.php的操作是：先锁定B记录，然后再锁定A记录，只有锁住A记录才会释放B记录的锁

此时a.php锁定了A记录、b.php锁定了B记录
当a.php处理完A记录后，想去锁定B记录，结果发现B记录被锁了，所以无法释放加在A记录上的锁
b记录也因为无法锁定A记录而无法释放B记录的锁
这样就形成了死锁

怎么解决：
a.php和b.php都要改成一样的加锁顺序
a.php先锁A再锁B，那b.php也要先锁A再锁B
```


#6.数据库如果出现了死锁,你怎么排查,怎么判断出现了死锁?
```
SELECT * FROM INFORMATION_SCHEMA.INNODB_TRX;
SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCK_WAITS;  
SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCKS;  

SHOW processlist;
SHOW ENGINE INNODB STATUS;
```

##7.主从复制，从服务器会读取到主服务器正在回滚的数据吗？主数据库写成功，从服务器因为一些原因写失败，最后会出现什么情况？主从复制如果键冲突怎么办？
```

```


##8.mysql中的字符集，客户端与数据库不一致，怎么办?
```
#way 1
vim my.ini
    default-character-set = utf8
    character_set_server = utf8

#way 2
SET character_set_client = utf8 ;
SET character_set_connection = utf8 ;
SET character_set_database = utf8 ;
SET character_set_results = utf8 ;
SET character_set_server = utf8 ;
SET collation_connection = utf8 ;
SET collation_database = utf8 ;
SET collation_server = utf8 ;
```

##9.数据库中的字符集是latin1,你现在将utf8的字符串存到latin1字符集的数据库表,你能将utf8的字符串存进去吗？
```
默认情况下（如客户端、连接等字符都是utf8）：
    英文数字和符号可以，但中文不行。
    insert into latin1(data) values('123abc!@#');        //成功，显示正常
    insert into latin1(data) values('中文123abc!@#');     //失败，1366错误
    
    因为：
        latin1是单字节
        utf8是三字节
        中文需要2个字节来存储
    
特殊情况（客户端字符集设置与表字符集一致，比如都是utf8）：
    此时中英文都能插入成功
    insert into latin1(data) values('123abc!@#');         //成功，显示正常
    insert into latin1(data) values('中文123abc!@#');      //成功，显示乱码
```

## 10.mysql中字段类型各占几个字节：smallint、int、bigint、datetime、varchar(8)
```
• TINYINT——一个微小的整数，支持 -128到127(SIGNED)，0到255(UNSIGNED)，需要1个字节存储 
• BIT——同TINYINT(1) 
• BOOL——同TINYINT(1) 
• SMALLINT——一个小整数，支持 -32768到32767(SIGNED)，0到65535(UNSIGNED)，需要2个字节存储 MEDIUMINT——一个中等整数，支持 -8388608到8388607(SIGNED)，0到16777215(UNSIGNED)，需要3个字节存储 
• INT——一个整数，支持 -2147493648到2147493647(SIGNED)，0到4294967295(UNSIGNED)，需要4个字节存储 
• INTEGER——同INT 
• BIGINT——一个大整数，支持 -9223372036854775808到9223372036854775807(SIGNED)，0到18446744073709551615(UNSIGNED)，需要8个字节存储 
• FLOAT(precision)——一个浮点数。precision<=24用于单精度浮点数；precision在25和53之间，用于又精度 浮点数。FLOAT(X)与相诮的FLOAT和DOUBLE类型有差相同的范围，但是没有定义显示尺寸和小数位数。在MySQL3.23之前，这不是一个 真的浮点值，且总是有两位小数。MySQL中的所有计算都用双精度，所以这会带来一些意想不到的问题。 
• FLOAT——一个小的菜单精度浮点数。支持 -3.402823466E+38到-1.175494351E-38，0和1.175494351E-38 to 3.402823466E+38，需要4个字节存储。如果是UNSIGNED，正数的范围保持不变，但负数是不允许的。 
• DOUBLE——一个双精度浮点数。支持 -1.7976931348623157E+308到-2.2250738585072014E-308，0和2.2250738585072014E- 308到1.7976931348623157E+308。如果是FLOAT，UNSIGNED不会改变正数范围，但负数是不允许的。 
• DOUBLE PRECISION——同DOUBLE 
• REAL——同DOUBLE 
• DECIMAL——将一个数像字符串那样存储，每个字符占一个字节 
• DEC——同DECIMAL 
• NUMERIC——同DECIMAL 

字符串列类型:char、varchar、nvarchar 
字符串列类型用于存储任何类型的字符数据，如名字、地址或者报纸文章。下面是MySQL中可用的字符串列类型 
• CHAR——字符。固定长度的字串，在右边补齐空格，达到指定的长度。支持从0到155个字符。搜索值时，后缀的空格将被删除。 
• VARCHAR——可变长的字符。一个可变长度的字串，其中的后缀空格在存储值时被删除。支持从0到255字符 
• TINYBLOB——微小的二进制对象。支持255个字符。需要长度+1字节的存储。与TINYTEXT一样，只不过搜索时是区分大小写的。(0.25KB) 
• TINYTEXT——支持255个字符。要求长度+1字节的存储。与TINYBLOB一样，只不过搜索时会忽略大小写。(0.25KB) 
• BLOB——二进制对象。支持65535个字符。需要长度+2字节的存储。 (64KB) 
• TEXT——支持65535个字符。要求长度+2字节的存储。 (64KB) 
• MEDIUMBLOB——中等大小的二进制对象。支持16777215个字符。需要长度+3字节的存储。 (16M) 
• MEDIUMTEXT——支持16777215个字符。需要长度+3字节的存储。 (16M) 
• LONGBLOB——大的的二进制对象。支持4294967295个字符。需要长度+4字节的存储。 (4G) 
• LONGTEXT——支持4294967295个字符。需要长度+4字节的存储。(4G) 
• ENUM——枚举。只能有一个指定的值，即NULL或""，最大有65535个值 
• SET——一个集合。可以有0到64个值，均来自于指定清单. 

日期和时间列类型 
　日期和时间列类型用于处理时间数据，可以存储当日的时间或出生日期这样的数据。格式的规定：Y表示年、M（前M）表示月、D表示日、H表示小时、M（后M）表示分钟、S表示秒。下面是MySQL中可用的日期和时间列类型 
• DATETIME——格式：'YYYY-MM-DD HH:MM:SS'，范围：'1000-01-01 00:00:00'到'9999-12-31 23:59:59' 
• DATE——格式：'YYYY-MM-DD'，范围：'1000-01-01'到'9999-12-31' 
• TIMESTAMP——格式：'YYYYMMDDHHMMSS'、'YYMMDDHHMMSS'、'YYYYMMDD'、'YYMMDD'，范围：'1970-01-01 00:00:00'到'2037-01-01 00:00:00' 
• TIME——格式：'HH:MM:SS' 
• YEAR——格式：'YYYY，范围：'1901'到'2155'
```


# 11.myisam和innodb的区别，为什么myisam比innodb快，myisam和innodb的索引数据结构是什么样的?innodb主键索引和非主键索引的区别?其索引上存放的数据是什么样的？
```
聚簇索引（聚集索引），B+Tree：

    仅仅出现在innodb引擎的主键索引上。
    聚簇：innodb的主键索引关键字，与 记录 是存储在一起的
    
    导致的结果： 
    记录依据主键顺序排序
    记录的真实位置会改变。随着主键索引关键字的改变而改变
    那么innodb表上的非主键索引（二级索引）：存储的是：关键字与主键值的对应关系（而不是关键字与记录位置的对应关系）
    导致：innodb的非主键索引：都是二次查找。
    1关键字确定主键值。
    2主键值确定记录
    
    在数据结构层面上：
    在原来的B-Tree结构上，做了一定的改动，改动后的这个聚簇（聚集）结构称之为 B+Tree

查询速度快：
    INNODB在做SELECT的时候，要维护的东西比MYISAM引擎多很多:
    1）数据块，INNODB要缓存，MYISAM只缓存索引块，  这中间还有换进换出的减少
    2）innodb寻址要映射到块，再到行，MYISAM记录的直接是文件的OFFSET，定位比INNODB要快
    3）INNODB还需要维护MVCC一致；虽然你的场景没有，但他还是需要去检查和维护
    MVCC (Multi-Version Concurrency Control)多版本并发控制 
    
    注释：
    InnoDB：通过为每一行记录添加两个额外的隐藏的值来实现MVCC，这两个值一个记录这行数据何时被创建，另外一个记录这行数据何时过期（或者被删除）。但是InnoDB并不存储这些事件发生时的实际时间，相反它只存储这些事件发生时的系统版本号。这是一个随着事务的创建而不断增长的数字。每个事务在事务开始时会记录它自己的系统版本号。每个查询必须去检查每行数据的版本号与事务的版本号是否相同。让我们来看看当隔离级别是REPEATABLEREAD时这种策略是如何应用到特定的操作的：
    　　SELECT InnoDB必须每行数据来保证它符合两个条件：
    　　1、InnoDB必须找到一个行的版本，它至少要和事务的版本一样老(也即它的版本号不大于事务的版本号)。这保证了不管是事务开始之前，或者事务创建时，或者修改了这行数据的时候，这行数据是存在的。
    　　2、这行数据的删除版本必须是未定义的或者比事务版本要大。这可以保证在事务开始之前这行数据没有被删除
```

#12.应用中我们经常会遇到在user表随机调取10条数据来展示的情况
```
select * from user where rand() limit 10;
```
#13.权限如何设计?
```
user-用户表, role-角色表, perm-权限表
user_role-用户角色表,
role_perm-角色权限表
```
