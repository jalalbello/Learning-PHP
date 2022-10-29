# Note : even if 4 * 2.5 is 10, the result is stored as float, because one of the operands is a float (2.5).

## is_int(), checks if its an int

## PHP NaN

## PHP Numerical Strings

he function returns true if the variable is a number or a numeric string, false otherwise.

```php
$x = 5985;
var_dump(is_numeric($x));
// True
$x = "5985";
var_dump(is_numeric($x));
// True
$x = "59.85" + 100;
var_dump(is_numeric($x));
// True
$x = "Hello";
var_dump(is_numeric($x));
// True
```

## Php converting STR and FLOAT **TO** INT

```php
$x = 23465.768;
$int_cast = (int)$x;
echo $int_cast;
// Cast string to int
$x = "23465.768";
$int_cast = (int)$x;
echo $int_cast;
```