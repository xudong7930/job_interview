
#不使用IOC
```php
<?php
/**
 * 没有IoC/DI的时候，常规的A类使用C类的示例
 */

/**
 * Class c
 */
class c
{
    public function say()
    {
        echo 'hello';
    }
}

/**
 * Class a
 */
class a
{
    private $c;
    public function __construct()
    {
        $this->c = new C(); // 实例化创建C类
    }

    public function sayC()
    {
        echo $this->c->say(); // 调用C类中的方法
    }
}

$a = new a();
$a->sayC();
```


#使用IOC
```php
<?php
/**
 * 当有了IoC/DI的容器后,a类依赖c实例注入的示例
 */

/**
 * Class c
 */
class c
{
    public function say()
    {
        echo 'hello';
    }
}

/**
 * Class a
 */
class a
{
    private $c;
    public function setC(C $c)
    {
        $this->c = $c; // 实例化创建C类
    }

    public function sayC()
    {
        echo $this->c->say(); // 调用C类中的方法
    }
}

$c = new C();
$a = new a();
$a->setC($c);
$a->sayC();
```