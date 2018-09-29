单例模式(SingleTon)
===================

> 通过单例模式可以保证系统中一个类只有一个实例

## 代码
```php
class SingleTon
{
    //创建静态私有的变量保存该类对象
    private static $instance;

    // 防止直接创建对象
    private function __construct(){

    }

    // 防止克隆对象
    private function __clone(){

    }

    public static function getInstance()
    {
        if (self::$instance == null) {
            self::$instance = new self();
        }
        return self::$instance;
    }

    public function show()
    {
        echo "hello";
    }
}

$s = SingleTon::getInstance();
$s->show();
```
