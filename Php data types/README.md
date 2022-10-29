## PHP Data Types

**String**:

Any text inside quotes

**Integer**:

At least one digit, no decimal point

Integers can be specified in: 
- decimal (base 10), 
- hexadecimal (base 16), 
- octal (base 8), 
- binary (base 2) notation

## Float

a number with a decimal point or a number in exponential form

## Boolean

## Array

The PHP var_dump() function returns the data type and value:

```php
$cars = array("Volvo","BMW","Toyota");
var_dump($cars);
// array(3) { [0]=> string(5) "Volvo" [1]=> string(3) "BMW" [2]=> string(6) "Toyota" }
```
## Object

```php
Syntax
    class Car {
    public $color;
    public $model;
    public function __construct($color, $model) {
      $this->color = $color;
      $this->model = $model;
    }
    public function message() {
      return "My car is a " . $this->color . " " . $this->model . "!";
    }
    }
    $myCar = new Car("Black", "BMW");
    echo $myCar -> message();
    //! this will not work, echo $myCar.message();
```

## NULL Value

Null is a special data type which can have only one value: NULL.

A variable of data type NULL is a variable that has no value assigned to it.

> **_NOTE:_** If a variable is created without a value, it is automatically assigned a value of NULL.
Variables can also be emptied by setting the value to NULL

## PHP Resource

Its not a data type, but storing of functions refrences and other ressources external to PHP