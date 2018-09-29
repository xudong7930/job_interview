工厂模式 (Factory)
==================

> 工厂方法模式可以允许系统在不修改工厂角色的情况下引进新产品

```php
Interface Shape 
{
    public function draw();
}

class Rectangle implements Shape
{
    public function draw()
    {
        echo 'Rectangle::draw() !!!'.PHP_EOL;
    }
}

class Circle implements Shape
{
    public function draw()
    {
        echo 'Circle::draw() !!!'.PHP_EOL;
    }
}

/**
*  ShapeFactory
*/
class ShapeFactory
{
    public function getShape(String $shape)
    {
        switch ($shape) {
            case 'RECTANGLE':
                return new Rectangle();
                break;
            
            case 'SQUARE':
                return new Square();
                break;

            case 'CIRCLE':
                return new Circle();
                break;

            default:
                return null;
                break;
        }
    }
}

$f = new ShapeFactory();
$shape = $f->getShape('RECTANGLE');
$shape->draw();
```
