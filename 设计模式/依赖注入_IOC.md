依赖注入（IOC）
==============

#使用IOC
```php
/**
 * 当有了IoC/DI的容器后,a类依赖c实例注入的示例
 */
class c
{
    public function say()
    {
        echo 'hello';
    }
}

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
