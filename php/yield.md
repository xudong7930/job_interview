php yield生成器
================

* https://segmentfault.com/a/1190000012334856

```php
function readTxt()
{
    # code...
    $handle = fopen("./test.txt", 'rb');

    while (feof($handle)===false) {
        # code...
        yield fgets($handle);
    }

    fclose($handle);
}

foreach (readTxt() as $key => $value) {
    # code...
    echo $value.PHP_EOL;
}

```

```
yield读取超大文件
背后的代码执行规则却一点儿也不一样。使用生成器读取文件，第一次读取了第一行，第二次读取了第二行，以此类推，每次被加载到内存中的文字只有一行，大大的减小了内存的使用。
这样，即使读取上G的文本也不用担心，完全可以像读取很小文件一样编写代码
```



