工厂模式 (Factory Pattern)
===============

```php
<?php
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

class Square implements Shape
{
    public function draw()
    {
        echo 'Square::draw() !!!'.PHP_EOL;
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


class User
{
    public function index()
    {
        $f = new ShapeFactory();
        // $shape = $f->getShape('CIRCLE');
        // $shape = $f->getShape('SQUARE');
        $shape = $f->getShape('RECTANGLE');
        $shape->draw();
    }
}

$u = new User;
$u->index();

```
