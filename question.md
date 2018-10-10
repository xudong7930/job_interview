## 最常见的PHP面试题
1. 高级PHP面试题1
http://blog.csdn.net/s1070/article/details/51174710
http://blog.csdn.net/s1070/article/details/51174725
http://blog.csdn.net/s1070/article/details/51174733
http://blog.csdn.net/s1070/article/details/51174698

2. PHP中的HereDoc技术?
答:
$str = <<<EOF
HEREW,
FAEFWE
FEAFA,
FEWAF,
DFSSD
EOF;

1. 写出一些php魔幻方法?
答：
    __construct()
    __desctruct()
    
    __call()
    __callStatic()
    
    __get()
    __set()
    
    __isset()
    __unset()
    __sleep()
    __wakeup()
    __toString()
    __invoke()
    __set_state()
    __clone()
    __debugInfo()
    __autoload

3. posix和perl标准的正则表达式区别?
答：PHP同时支持两套标准。
    定界符：
    posix兼容的正则没有定界符
    perl兼容的正则使用非字母，数字，反斜线作为定界符
    
    修饰符:
    posix兼容的正则没有修饰符
    perl兼容的正则使用i,m,s,x

4. MySQL数据库作发布系统的存储，一天五万条以上的增量，预计运维三年,怎么优化？
答：  
    优化应该不仅仅是数据库方面
    使用高性能的服务器
    多使用缓存
    页面服务器、数据库服务器、图片服务器、上传下载服务器分离
    数据库集群，表分割（水平分割和垂直分割）和表散列
    负载均衡
    重视每个代码开发细节，特别是大循环，多请求和SQL语句复杂的时候

5. 对于大流量的网站,您采用什么样的方法来解决各页面访问量统计问题
    答：
    1.首先，确认服务器硬件是否足够支持当前的流量。
    2.其次，优化数据库访问，缓存技术。
    3.第三，禁止外部的盗链。
    4.第四，控制大文件的下载。
    5.第五，使用不同主机分流主要流量
    6.第六，使用流量分析统计软件


6. 大型的论坛/新闻文章系统/SNS网站在性能优化上有什么区别?
    答: 
        新闻媒体注意细览页的性能优化，比如图片、结构，保持清爽；
        SNS注意交互、页面JS、ajxa、动态内容大小；
        严格控制大小、减少定向、压缩图片、降低CSS加载速度，利用好缓存，这是通的


1. php是什么？
答：超文本处理器，用于构建WEB的动态语言脚本

2. 什么是mvc？
答：全名是model/view/controller 是一种软件架构思想，将软件按照模型，视图，控制器来划分

3. 在页面中引用css有几种方式？
答: link引入，style标签，html标签的style属性

4. php支持多继承吗？
答: 单继承

5. php中echo和print有什么区别？
答: echo不是函数，没有返回值，更快
    print有返回值的函数，打印字符串
    print_r打印符合数据类型

6. get和post方法有什么区别？
答: get从服务器上获取数据
    post把数据提交给服务器
    传输的数据size有限制

7. php中获取图像尺寸大小的方法是什么？

8. php中的pear是什么？
答：pear是php的包管理器，现在都使用composer了

9. 如何用php和mysql上传视频？
答: 保留上传的路径

10. php中的错误类型有哪些？
答: E_ALL, E_NOTICE, E_WARNING, E_STRICT

11. 如何在php中定义常量？
答: define('CONSTRNAME',"CONSTVALUE");

12. 如何不使用submit按钮来提交表单？
答: <a href="javascript: document.form.submit()">submit</a>

13. mysql_fetch_row() 和mysql_fetch_array之间有什么区别? 
14. 对于大流量的网站,您采用什么样的方法来解决访问量问题?

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
