php trait
==========

> Traits是横向扩展一个类，从而实现代码复用

* Trait应用中的优先级如下:
1.来自当前类的成员覆盖了 trait 的方法
2.trait 覆盖了被继承的方法

* https://segmentfault.com/a/1190000008009455

```php
trait Log
{
    public function some()
    {
        // do some output...
    }
}
```










