#1.在php中定义常量时，const和define的区别？

```
使用const使得代码简单易读，const本身就是一个语言结构，而define是一个函数。另外const在编译时要比define快很多。

1、const用于类成员变量的定义，一经定义，不可修改。Define不可以用于类成员变量的定义，可用于全局常量。

2、Const可在类中使用，define不能

3、Const不能再条件语句中定义常量

```

#2.如何保证代码质量?
```
可读性，可维护性，可变更性 
代码质量评价：低耦合，高内聚
https://segmentfault.com/a/1190000004355331
```


#3.学习PHP的渠道?
```
php.net
sf,stackover
google
《Modern PHP》,《PHP核心技术和最佳实践》,《PHP the right way》 
```


#4.php的魔术方法,并说明用途
```
__construct()， 
__destruct()， unset的时候调用
__call()， 
__callStatic()， 
__get()， 
__set()， 
__isset()， 
__unset()， 
__sleep()， 
__wakeup()， 
__toString()，
__invoke()， 
__set_state()， 
__clone(),
__debugInfo(),
__autoload(): 我们在使用一个类时，如果发现这个类没有加载，就会自动运行 __autoload() 函数
```


#5.抽象类和接口的区别，分别在什么场景使用?
```
抽象类可以实现的功能，接口也可以实现。 
抽象类的接口的区别，不在于编程实现，而在于程序设计模式的不同。 
一般来讲，抽象用于不同的事物，而接口用于事物的行为
```

# 6.array_merge 和 + 的区别?
```php
$a = [0,1,2,3];
$b = [2,3,4,5,6];

$c = array_merge($a, $b); // [0,1,2,3,2,3,4,5]
$d = $a + $b; // [0,1,2,3,6] 相同位置存在则去掉，不存在加上
```

#7.封装，继承，多态
```php
#封装

#继承
class Log {}
class FileLog extends Log {}

#多态
interface Log { public function log(); }
class FileLog implements Log {
    public function log()
    {
        // do some log...
    }
}

class DBLog implements Log {
    public function log()
    {
        // do another log...
    }
}
```


#8.PHP 的垃圾收集机制是怎样的?

* PHP内存管理 垃圾回收: https://www.jianshu.com/p/63a381a7f70c

```
php作为脚本语言是页面结束即释放变量所占内存的。 当一个 PHP线程结束时，当前占用的所有内存空间都会被销毁，当前程序中所有对象同时被销毁。GC进程一般都跟着每起一个SESSION而开始运行的.gc目的是为了在session文件过期以后自动销毁删除这些文件.在PHP中，没有任何变量指向这个对象时，这个对象就成为垃圾。PHP会将其在内存中销毁；这是PHP的GC垃圾处理机制，防止内存溢出。 执行这些函数也可以起到回收作用__destruct /unset/mysql_close /fclose php对session有明确的gc处理时间设定session.gc_maxlifetime 如果说有垃圾，那就是整体的程序在框架使用中，会多次调用同一文件等等造成的非单件模式等。
```

#9.cgi、fastcgi、php-fpm
```
cgi 早期的web server只可以处理简单的静态web文件，但是随着技术的发展出现动态语言如PHP，Python。PHP语言交给PHP解析器进行处理，但是处理之后如何和web server进行通信呢？ 为了解决不同的语言处理器与web server之间的通讯，出现了CGI协议。只要按照CGI协议编写程序，就可以实现与语言解析器与web server之间的通讯。 CGI协议虽然解决了语言解析器和seb server之间通讯的问题，但是它的效率很低。因为web server每收到一个请求都会创建一个CGI进程，PHP解析器都会解析php.ini文件，初始化环境，请求结束的时候再关闭进程。对于每一个创建的CGI进程都会执行这些操作。所以效率很低。

FastCGI FastCGI是用来提高CGI性能的，FastCGI每次处理完请求之后不会关闭掉进程。而是保留这个进程，使这个进程可以处理多个请求。这样的话每个请求都不用再重新创建一个进程了。大大提升了处理效率。

PHP-FPM PHP-FPM(FastCGI Process Manager：FastCGI进程管理器)是一个实现了Fastcgi的程序，并且提供进程管理的功能。进程包括master进程和worker进程。master进程只有一个，负责监听端口，接受来自web server的请求。worker进程一般会有多个，每个进程中会嵌入一个PHP解析器，进程PHP代码的处理。
```

#10.include(), include_once(), require, require_once的差别
```
require函数通常放在PHP程序的最前面，在PHP程序执行之前，就会先读取require指定引入的文件，使它变成PHP程序网页的一部分。
include函数一般是放在流程控制的处理部分中。PHP程序在读到include的文件时，才将它读进来，这种方式可以把程序执行时的流程简单化。

他们两个的用途是一样的，不一定非要哪个放在最前面哪个放在中间，他们最根本的区别在于错误处理的方式不一样。

require一个文件存在错误的话，那么程序就会中断执行，并显示致命错误;而include一个文件存在错误的话，那么程序不会中断，会继续执行，并显示一个警告的错误。
include有返回值，而require没有。
```

#11.PHP的变量类型
```
四种标量类型:
boolean （布尔型）：这是最简单的类型，只有两种取值，可以为 TRUE/true 或 FALSE/false ，不区分大小写。详细请查看：PHP布尔类型（boolean）
integer （整型）：在32 位操作系统中它的有效范围是：-2 147 483 648~+2 147 483 647。整型值可以使用十进制，十六进制或八进制表示，前面可以加上可选的符号（- 或者 +）。八进制表示数字前必须加上 0（零），十六进制表示数字前必须加上 0x。
float （浮点型, 也称作 double)
string （字符串）：字符型变量不同于其他编程语言有字符与字符串之分，在PHP 中，统一使用字符型变量来定义字符或者字符串。

两种复合类型:
array （数组）：数组型变量是一种比较特殊的变量类型，将在后续章节中详细说明。
object （对象）：对象也是一种特殊的数据类型。要创建object变量，请使用 new 关键字。详细请查看：PHP对象类型（object）

两种特殊类型：
resource（资源）：源是一种特殊变量，保存了到外部资源的一个引用。资源是通过专门的函数来建立和使用的。详情请查看：PHP资源类型（resource）

NULL（NULL）：表示一个变量没有值。NULL 类型唯一可能的值就是 NULL。
```

#12.php的优化?

* PHP优化 https://www.awaimai.com/1050.html

# 13.下面的输出?
```php
isset(null); false
isset(false); true
empty(null); true
empty(false); true
```

#14.echo、print、print_r的区别?
```
print_r是函数，echo、print是结构语言。
```

#15.PHP的错误类型有哪些?
```
E_ERROR,
E_WARNING
E_PARSE,
E_ALL,
E_NOTICE....
```

#16.static, $this, self的区别?

* https://blog.csdn.net/lamp_yang_3533/article/details/79912453

```
self 对当前类的静态引用，可以访问类的静态属性，静态方法，常量
$this 指向实际调用的对象，不能访问类的静态属性和常量，不能存在于静态方法中
static 声明类的静态成员和方法，还可以静态绑定
```


#17.模板引擎是什么，解决什么问题,实现原理?
```
实现数据生成和数据展示的分离,让前后端更好的分工协作

Smarty、Twig、Blade
```

#18.PHP框架
```
ThinkPHP（TP）、CodeIgniter（CI）、Zend（非 OOP 系列）
Yaf、Phalcon（C 扩展系）
Yii、Laravel、Symfony（纯 OOP 系列）
Swoole、Workerman （网络编程框架）
```






















































