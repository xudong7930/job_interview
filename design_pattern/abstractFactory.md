抽象工厂模式(Abstract Factory Pattern)
====================================

```php
<?php
Interface Shape 
{
    public function draw();
}

Interface Color
{
    public function fill();
}

class Rectangle implements Shape
{
    public function draw()
    {
        echo 'Rectangle::draw() !!!'.PHP_EOL;
    }
}

Class RedColor implements Color
{
    public function fill()
    {
        echo 'Red::fill() !!!'.PHP_EOL;
    }
}


Abstract Class AbstractFactory
{
    Abstract function getShape(String $shape);
    Abstract function getColor(String $color);
}


/**
*  ShapeFactory
*/
class ShapeFactory extends AbstractFactory
{
    public function getShape(String $shape)
    {
        switch ($shape) {
            case 'RECTANGLE':
                return new Rectangle();
                break;

            default:
                return null;
                break;
        }
    }

    public function getColor(String $color)
    {
        return null;
    }
}

class ColorFactory extends AbstractFactory
{
    public function getColor(String $color)
    {
        switch ($color) {
            case 'RED':
                return new RedColor();
                break;

            default:
                return null;
                break;
        }
    }

    public function getShape(String $shape)
    {
        return null;
    }
}


class FactoryProducer
{
    public function getFactory(String $name)
    {
        switch ($name) {
            case 'SHAPE':
                return new ShapeFactory();
                break;
            
            case 'COLOR':
                return new ColorFactory();
                break;

            default:
                return null;
                break;
        }
    }
}

class User
{
    public function index()
    {
        $fp = new FactoryProducer();
        $shape = $fp->getFactory('SHAPE');
        $rk = $shape->getShape('RECTANGLE');
        $rk->draw();

        $color = $fp->getFactory('COLOR');
        $red = $color->getColor('RED');
        $red->fill();
    }
}

$u = new User;
$u->index();
```
