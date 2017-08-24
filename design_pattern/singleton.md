单例模式(SingleTon)
=================

## 代码
```php
<?php
class SingleTon
{
    private static $instance;

    private function __construct()
    {
    }

    private function __clone()
    {   
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
