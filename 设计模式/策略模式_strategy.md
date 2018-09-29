策略模式(strategy)
====================

>  定义一系列算法，将每一个算法封装起来，并让它们可以相互替换。策略模式让算法独立于使用它的客户而变化，也称为政策模式(Policy)。

```php
abstract class Strategy
{
    // 去上班
    abstract function gotowork();
}

class WalkStrategy extends Strategy
{
    public function gotowork()
    {
        echo '走路去上班的策略'.PHP_EOL;
    }
}
class DriveStrategy extends Strategy
{
    public function gotowork()
    {
        echo '开车去上班的策略'.PHP_EOL;
    }
}

//环境角色
class Context
{
    protected $strategy;

    public function __construct(Strategy $strategy)
    {
        $this->strategy = $strategy;
    }

    public function request()
    {
        $this->strategy->gotowork();
    }
}

// 开车去上班，无论怎样目的都是去上班，至于怎样上班的，就是用策略来实现的：走路(WalkStrategy)，开车(DriveStrategy)
$context = new Context(new DriveStrategy);
$context->request();
```