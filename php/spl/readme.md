#1. 什么是SPL？
```
SPL是Standard PHP Library（PHP标准库）
目前在使用中，SPL更多地被看作是一种使object（物体）模仿array（数组）行为的interfaces和classes
```

#2. 什么是Iterator？
```
SPL的核心概念就是Iterator
通俗地说，Iterator能够使许多不同的数据结构，都能有统一的操作界面，比如一个数据库的结果集、同一个目录中的文件集、或者一个文本中每一行构成的集合


遍历mysql结果集:
$result = mysql_query("select * from users;");
while( $row = mysql_fetch_array($result)) {
	// ....
}

遍历目录:
$dh = opendir("/home/sbjsw");
while($file = readdir($dh)) {
	// ...
}

读取文件内容:
$fh = fopen("/home/doc.txt");
while(!feof($fh)) {
	$line = fgets($fh);
	// ...
}

上面三段代码，虽然处理的是不同的resource（资源），但是功能都是遍历结果集（loop over contents），因此Iterator的基本思想，就是将这三种不同的操作统一起来，用同样的命令界面，处理不同的资源。
```



#3.SPL Interface
Iterator： 
实现Iterator的类可以使用foreach遍历
实现Iterator的类必须实现current(),key(),next(),rewind(), valid()方法
```

```

ArrayAccess:
实现ArrayAccess的类可以将object像array那样操作
实现ArrayAccess的类必须实现offsetExists($offset), offsetGet($offset), offsetSet($offset, $value), offsetUnset($offset)
```
```



IteratorAggregate:
实现IteratorAggregate的类可以将object像array那样遍历
实现IteratorAggregate的类必须实现getIterator()
```
```


RecursiveIterator:
实现IteratorAggregate的类可以遍历多层数据
```
```

SeekableIterator:
```
```


Countable:
实现IteratorAggregate的类必须实现count()
```
```

#4.SPL Class
查看所有的spl内置类:
```php
foreach (spl_classes() as $key => $item) {
	echo $key . "=>" . $item . PHP_EOL;
}
```

DirectoryIterator类:
```php
$dit = new DirectoryIterator('/Users/xudong7930/Desktop/job_interview');

while ($dit->valid()) {
	$filename = $dit->getFilename();
	
	if ($dit->isDir()) {
		echo $dit->key().' <=> '.$dit->current() . PHP_EOL;
	}
	
	$dit->next();
}
```


ArrayObject类:
将array转为object
```php
$data = ["kolad", "kangaroo", "wombat"];
$obj = new ArrayObject($data);
for ($iterator=$obj->getIterator(); $iterator->valid(); $iterator->next()) { 
	echo $iterator->key() . "<=>" . $iterator->current() . PHP_EOL;
}

$obj->append('dingo');
$obj->natcasesort();
$obj->count();
$obj->offsetUnset(5);
$obj->offsetExists(3);
$obj->offsetSet(5, "galah"); //更新值
$obj->offsetGet(4); //指定索引的值
```

ArrayIterator:





























