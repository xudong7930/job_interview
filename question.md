
## MyISAM 和 InnoDB的区别?
区别主要有以下几个:
1. 构成上，MyISAM 的表在磁盘中有三个文件组成，分别是表定义文件( .frm)、数据文件(.MYD)、索引文件(.MYI),而 InnoDB 的表由 数据和日志文件组成。
2. 安全方面，MyISAM 强调的是性能，其查询效率较高，但不支持事务和外键等安全性方面的功能，而 InnoDB 支持事务和外键等高级功能，查 
3. 对锁的支持，MyISAM 支持表锁，而 InnoDB 支持行锁。

## php 访问数据库有哪几步?
1. 连接数据库服务器:mysql_connect('host','user','password');
2. 选择数据库:mysql_select_db(数据库名);
3. 设置从数据库提取数据的字符集:mysql_query("set names utf8"); 4. 执行 sql 语句:mysql_query(sql 语句);
5. 处理结果集
6. 关闭结果集，释放资源:mysql_free_result($result); 
7. 关闭与数据库服务器的连接:mysql_close($link);

## 简述项目中优化SQL语句效率的方法?
1. 尽量选择较小的列
2. 将where中用的比较频繁的字段建立索引
3. select子句中避免使用‘*’
4. 避免在索引列上使用计算、not in 和<>等操作 5. 当只需要一行数据的时候使用limit 1
6. 保证单表数据不超过200W，适时分割表。

## sql语句应该考虑的安全性?
* 防止SQL注入, 对特殊字符进行转义,过滤或者使用预编译SQL绑定变量
* 最小权限原则, 不用root用户, 为不同的类型的动作或者组建使用不同的账户
* 当sql出错时, 不要把数据库输出返回给用户.

## 简述TCP协议的3次握手过程
* TCP是主机对主机层的传输控制协议，提供可靠的连接服务，采用三次握手确认建立一个连接: 第一次握手:建立连接时，客户端发送syn包(syn=j)到服务器，并进入SYN_SEND状态，等待服务器确认; 
* 第二次握手:服务器收到syn包，必须确认客户的SYN(ack=j+1)，同时自己也发送一个SYN包(syn=k)，即SYN+ACK包 SYN_RECV状态; 
* 第三次握手:客户端收到服务器的SYN+ACK包，向服务器发送确认包ACK(ack=k+1)，此包发送完毕，客户端和服务器进入E 次握手。
* 完成三次握手，客户端与服务器开始传送数据。


## PHP如何实现页面跳转?
1.header
```php
header('Location: http://url.com');
```

2.meta
```php
echo '<meta http­equiv=refresh content='0;url=http://url.com' />'
```

## 编写一个函数实现无限分类
```php
function tree($arr, $pid=0, $level=0)
{
    static $list = [];
    foreach ($arr as $item) {
        if ($item['pid'] == $pid) {
            $item['level'] = $level;
            $list[] = $item;
            tree($arr, $item['id'], $level+1);
        }
    }
    return $list;
}
```


## 写一个函数遍历指定文件夹下的文件和子文件夹?
```php
function read_dir($path)
{
    $files = [];
    $sep = DIRECTORY_SEPARATOR;
    if (is_dir($path)) {
        if ($handle = opendir($path)) {
            while ($subdir = readdir($handle)) {
                if (!in_array($subdir, ['.', '..'])) {
                    if (is_dir($path.$sep.$subdir)) {
                        $files[$subdir] = read_dir($path.$sep.$subdir);
                    } else {
                        $files[] = $path.$sep.$subdir;
                    }
                }
            }
            closedir($handle);
            return $files;
        }
    }
}
$path = __dir__;
$files = read_dir($path);
echo json_encode($files);
```

## 取得文件的扩展名, 至少5中方法
```php
$file = '/abc/de/fg.ff.jpg';

// way1
$ext = explode('.', basename($file));
echo $ext[count($ext)-1];

// way2
echo substr(strrchr($file,"."), 1);

// way3
echo pathinfo($file, PATHINFO_EXTENSION);

// way4
echo substr($file, strrpos($file, '.')+1);
```


## 请写一段PHP代码，确保多个进程同时写入同一个文件成功
```php
<?php
$fp = fopen('filename.txt', 'w+');
if (flock($fp, LOCK_EX)) {
    fwrite($fp, "hello");
    flock($fp, LOCK_UN);
} else {
    echo 'file is locking. standby';
}
fclose($fp);
```

## PHP的垃圾回收机制
PHP可以自动进行内存管理，清除不再需要的对象。
PHP使用了引用计数(reference counting)这种单纯的垃圾回收(garbage collection)机制。每个对象都内含一个引用计数器，每新增一个对象，计数器加1。当reference离开生存空间或被设为NULL，计数器减1。当某个对象的引用计数器为零时，PHP将释放对象所占的内存空间。


## 写出一个创建多级目录的函数
```php
$path = __dir__.'/a/b/c';
if (is_dir($path)) {
    echo 'exist';
} else {
    if (mkdir($path, 0777, true)) {
        echo 'ok';
    } else {
        echo 'fail';
    }
}
```
