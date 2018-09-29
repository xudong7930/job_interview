建造者模式(builder)
=====================

> 可以把繁锁的操作封装在一起，并且可以使调用者无需关心构建的细节

## code

* 把大象放进冰箱，要分几步？1.打开冰箱，2.把大象放进去，3.关上冰箱门

```php
class PushDaxiang
{
    protected function openFridge()
    {
        echo "打开冰箱".PHP_EOL;
    }

    protected function pushElephant()
    {
        echo "把大象放进去".PHP_EOL;
    }

    protected function closeFridge()
    {
        echo "关上冰箱门".PHP_EOL;
    }

    //只是把一些常规操作，进行了简单的封装。我们把这种封装叫做构建者模式
    public function push()
    {
        $this->openFridge();
        $this->pushElephant();
        $this->closeFridge();
    }
}

(new PushDaxiang)->push();
```

